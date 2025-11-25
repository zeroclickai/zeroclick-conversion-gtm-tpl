# ZeroClick Conversion Tag - Google Tag Manager Template

Track conversions on your website using ZeroClick's advertising platform through Google Tag Manager.

## Overview

The ZeroClick Conversion Tag is a custom Google Tag Manager template that enables conversion tracking for ZeroClick advertising campaigns. Install this tag on your conversion pages (e.g., purchase confirmation, signup completion) to track successful conversions and optimize your advertising performance.

## Features

- **Simple Setup**: Configure with just your ZeroClick Pixel ID
- **Automatic Tracking**: Automatically retrieves stored visitor IDs from cookies or localStorage
- **Flexible Event Tracking**: Support for custom event names and conversion data
- **Optional Parameters**: Track order IDs, conversion values, and currencies
- **Privacy-Focused**: Only tracks conversions when a valid ZeroClick visitor ID exists
- **Server-Side Pixel**: Sends conversion data to ZeroClick's tracking endpoint

## Installation

### 1. Import the Template to GTM

1. Download [template.tpl](template.tpl) from this repository
2. In Google Tag Manager, navigate to **Templates** → **Tag Templates**
3. Click **New** → **Import**
4. Select the downloaded `template.tpl` file
5. Click **Save**

### 2. Create a New Tag

1. Navigate to **Tags** → **New**
2. Click **Tag Configuration**
3. Select **ZeroClick conversion tag** from the Custom templates section
4. Configure the tag parameters (see Configuration section below)
5. Set up a trigger to fire on your conversion page (e.g., "Purchase Complete" page view)
6. Save and publish your container

## Configuration

### Required Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| **Pixel ID** | Your unique ZeroClick Advertising Pixel ID (format: `ZC` followed by 13 alphanumeric characters) | `ZCa1b234567890c` |

### Optional Parameters

| Parameter | Description | Example |
|-----------|-------------|---------|
| **Event Name** | Name of the conversion event being tracked | `purchase`, `signup`, `lead` |
| **Order ID** | Unique identifier for the transaction | `ORDER-12345` |
| **Conversion Value** | Monetary value of the conversion | `99.99` |
| **Conversion Currency Code** | ISO 4217 currency code | `USD`, `EUR`, `GBP` |

## How It Works

1. **Visitor Identification**: The tag retrieves the stored ZeroClick visitor ID (`_zcId`) from:
   - Browser cookies (first priority)
   - localStorage (fallback)

2. **Conversion Tracking**: When a conversion occurs, the tag sends a tracking pixel to:
   ```
   https://mcp.zeroclick.ai/api/v1/offers/cv
   ```

3. **Data Transmission**: The following data is sent:
   - Pixel ID (required)
   - ZeroClick visitor ID (if available)
   - Event name (optional)
   - Order ID (optional)
   - Conversion value (optional)
   - Conversion currency (optional)
   - Timestamp

## Example GTM Configuration

### Basic Configuration (Conversion Tracking Only)

```
Tag Type: ZeroClick conversion tag
Pixel ID: ZCa1b234567890c
Event Name: purchase
Trigger: Purchase Complete - Page View
```

### Advanced Configuration (With Dynamic Values)

Use GTM variables to pass dynamic values:

```
Tag Type: ZeroClick conversion tag
Pixel ID: ZCa1b234567890c
Event Name: purchase
Order ID: {{Transaction ID}}
Conversion Value: {{Transaction Revenue}}
Conversion Currency Code: {{Transaction Currency}}
Trigger: Purchase Complete - Page View
```

## Setting Up GTM Variables

To pass dynamic conversion data, create these GTM variables:

1. **Transaction ID**: Variable Type: Data Layer Variable, Name: `transactionId`
2. **Transaction Revenue**: Variable Type: Data Layer Variable, Name: `transactionRevenue`
3. **Transaction Currency**: Variable Type: Data Layer Variable, Name: `transactionCurrency`

Then push data to the dataLayer on your conversion page:

```javascript
dataLayer.push({
  'event': 'purchase',
  'transactionId': 'ORDER-12345',
  'transactionRevenue': '99.99',
  'transactionCurrency': 'USD'
});
```

## Testing

### GTM Preview Mode

1. Enable **Preview** mode in Google Tag Manager
2. Navigate to your conversion page
3. Verify the ZeroClick conversion tag fires correctly
4. Check the tag's debug output for any errors

### Browser Developer Tools

1. Open your browser's Developer Tools (F12)
2. Go to the **Network** tab
3. Navigate to your conversion page
4. Look for a request to `mcp.zeroclick.ai/api/v1/offers/cv`
5. Verify the URL parameters include your Pixel ID and other data

### Console Logging

The tag logs errors to the browser console if:
- Pixel ID is missing
- Pixel ID format is invalid

Check the console for any error messages starting with `ZeroClick Error:`

## Pixel ID Format

Your Pixel ID must follow this format:
- Starts with `ZC`
- Followed by exactly 13 alphanumeric characters
- Example: `ZCa1b234567890c`

The tag will validate the format and fail if it's incorrect.

## Browser Compatibility

This tag is compatible with all modern browsers that support:
- Cookies
- localStorage
- Image pixel tracking

## Privacy & Data Collection

The ZeroClick conversion tag only fires when:
1. A valid ZeroClick Pixel ID is configured
2. A ZeroClick visitor ID exists (from a previous ad click)

No personally identifiable information (PII) is collected. Only conversion events and associated metadata are tracked.

## Troubleshooting

### Tag Not Firing

- Verify the tag's trigger is configured correctly
- Check that the trigger fires on your conversion page
- Enable GTM Preview mode to debug

### No Conversion Data Appearing

- Ensure users have clicked a ZeroClick ad (creating a `_zcId` cookie/localStorage entry)
- Verify your Pixel ID is correct
- Check that the ZeroClick visitor ID exists in cookies or localStorage

### Invalid Pixel ID Error

- Verify your Pixel ID format: `ZC` + 13 alphanumeric characters
- Check for typos or extra spaces
- Confirm you're using the Pixel ID from your ZeroClick account

## Additional Resources

- **ZeroClick Homepage**: [https://zeroclick.ai](https://zeroclick.ai)
- **Documentation**: [https://zeroclick.ai/documentation-conversion-tag](https://zeroclick.ai/documentation-conversion-tag)

## Repository Files

- `template.tpl` - Google Tag Manager custom template
- `metadata.yaml` - Template metadata and versioning
- `LICENSE` - Apache License 2.0

## License

Apache License 2.0 - See [LICENSE](LICENSE) file for details

## Support

For support or questions about the ZeroClick Conversion Tag:
- Visit [https://zeroclick.ai](https://zeroclick.ai)
- Check the official documentation at [https://zeroclick.ai/documentation-conversion-tag](https://zeroclick.ai/documentation-conversion-tag)

## Version History

See [metadata.yaml](metadata.yaml) for version history and change notes.

---

**Made for ZeroClick Advertising Platform** | [zeroclick.ai](https://zeroclick.ai)
