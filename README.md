# COD Verifier for WooCommerce - Multi-Country Edition

A comprehensive WordPress plugin that adds multi-country OTP and token payment verification for Cash on Delivery (COD) orders in WooCommerce with Twilio SMS integration.

## 🌍 New Multi-Country Features

### Supported Countries
- **🇮🇳 India (+91)** - Existing functionality preserved
- **🇺🇸 USA (+1)** - New support added
- **🇬🇧 UK (+44)** - New support added

### Key Enhancements
- **Country Code Dropdown**: Users select country before entering phone number
- **30-Second OTP Timer**: Prevents spam with visual countdown and button state changes
- **Regional Restrictions**: Admin can limit allowed countries (Global, India, USA, UK)
- **Enhanced Validation**: E.164 format validation for all countries
- **Improved UX**: Better error messages and user guidance

## 🚀 Features

### Core Functionality
- **Multi-Country OTP Verification**: Phone number verification via Twilio SMS for India, USA, and UK
- **Token Payment**: ₹1 payment verification to prevent fake orders
- **Test & Production Modes**: Easy testing before going live
- **Twilio Integration**: Reliable SMS delivery for OTP across countries
- **Razorpay Integration**: Secure payment processing
- **Mobile Responsive**: Works on all devices
- **Easy Configuration**: Simple admin settings with country restrictions

### New Timer Features
- **30-Second Cooldown**: Prevents OTP spam with configurable timer
- **Visual Feedback**: Button color changes during cooldown period
- **Countdown Display**: Shows remaining time before resend is allowed
- **Auto-Reset**: Timer clears when OTP is successfully verified

## 📁 File Structure

```
/cod-verifier
├── cod-verifier.php                ← Main plugin file (updated)
├── /includes
│   ├── settings-page.php          ← Admin settings with multi-country config
│   ├── ajax-handlers.php          ← Enhanced OTP/Token logic with country support
│   └── /twilio-sdk                 ← Twilio SDK directory (manual install)
│       └── /src/Twilio/            ← Twilio PHP SDK files
├── /assets
│   ├── script.js                  ← Enhanced frontend JavaScript with timer
│   └── cod-verifier.css           ← Updated styles with country dropdown
├── /templates
│   └── otp-box.php               ← Updated UI template with country selector
├── /languages
│   └── cod-verifier.pot          ← Translation file
└── README.md                     ← This file (updated)
```

## 📦 Installation

### Step 1: Upload Plugin
1. Download/create the `cod-verifier` folder with all files
2. **Install Twilio SDK** (see Step 1.5 below)
3. Zip the entire `cod-verifier` folder
4. Go to WordPress Admin → Plugins → Add New → Upload Plugin
5. Upload the zip file and activate the plugin

### Step 1.5: Install Twilio SDK (CRITICAL)
1. Download Twilio PHP SDK from: https://github.com/twilio/twilio-php
2. Extract and copy the `src/Twilio/` folder to `includes/twilio-sdk/src/Twilio/`
3. Ensure this file exists: `includes/twilio-sdk/src/Twilio/autoload.php`

### Step 2: Configure Multi-Country Settings
1. Go to **WooCommerce → COD Verifier** in admin menu
2. **Enable Test Mode** (recommended for initial setup)
3. **Choose Allowed Regions**:
   - 🌍 Global (India, USA, UK)
   - 🇮🇳 India Only
   - 🇺🇸 USA Only
   - 🇬🇧 UK Only
4. **Set OTP Timer Duration**: Default 30 seconds (15-120 seconds allowed)
5. Configure Twilio Settings:
   - Account SID (from Twilio Console)
   - Auth Token (from Twilio Console)
   - Twilio Phone Number (must support your selected regions)
6. Choose verification options:
   - ✅ Enable OTP Verification
   - ✅ Enable Token Payment
7. Save settings

### Step 3: Test Multi-Country Functionality
1. Go to your WooCommerce checkout page
2. Add any product to cart and proceed to checkout
3. Select **"Cash on Delivery"** as payment method
4. **Verification box should appear** with country dropdown
5. Test Different Countries:
   - **India**: Select 🇮🇳 +91, enter 10-digit number like `7039940998`
   - **USA**: Select 🇺🇸 +1, enter 10-digit number like `2125551234`
   - **UK**: Select 🇬🇧 +44, enter 10-digit number like `7700900123`
6. Test OTP Timer:
   - Click "Send OTP"
   - **In test mode, OTP will be shown in alert popup**
   - **Button should be disabled for 30 seconds with countdown**
   - Enter the OTP and verify
7. Test Token Payment:
   - Click "Pay ₹1 Token"
   - **In test mode, payment is simulated**
   - Check the confirmation checkbox
8. Place order - should complete successfully

## 🔧 Production Setup

### Multi-Country Twilio Configuration
1. Sign up at [Twilio](https://www.twilio.com/try-twilio)
2. **Get phone numbers for each region you want to support**:
   - For India: Get an Indian number or international number with India SMS capability
   - For USA: Get a US number
   - For UK: Get a UK number or international number with UK SMS capability
3. **Verify your Twilio phone number supports your target countries**
4. Copy Account SID, Auth Token, and Phone Number to plugin settings
5. Test SMS delivery in Test Mode first for each country

### Regional Restrictions
- **Global**: Allows all supported countries (India, USA, UK)
- **India Only**: Restricts to +91 numbers only (preserves existing functionality)
- **USA Only**: Restricts to +1 numbers only
- **UK Only**: Restricts to +44 numbers only

### Switch to Production
1. Add all API keys in settings
2. **Ensure Twilio number supports your allowed regions**
3. **Disable Test Mode**
4. Save settings
5. Test complete flow with real SMS and payment for each country

## 🧪 Testing Guide

### Multi-Country Test Mode Features
- **OTP Display**: OTP shown in JavaScript alert for all countries
- **SMS Simulation**: No real SMS sent regardless of country
- **Payment Simulation**: No real money charged
- **Timer Functionality**: 30-second countdown works in test mode
- **All Functionality**: Complete verification flow for all countries

### Testing Steps by Country

#### 🇮🇳 India Testing (Existing Users)
1. **Enable Test Mode** in settings
2. Set allowed regions to "India Only" or "Global"
3. Go to checkout and select COD
4. **Verify country dropdown shows 🇮🇳 +91**
5. **Test OTP Flow**:
   - Enter phone: `7039940998`
   - Click "Send OTP"
   - **Button should disable for 30 seconds**
   - Check alert for OTP code
   - Enter OTP and verify
   - Should show "✓ Verified"
6. Complete order successfully

#### 🇺🇸 USA Testing (New)
1. Set allowed regions to "USA Only" or "Global"
2. Go to checkout and select COD
3. **Verify country dropdown shows 🇺🇸 +1**
4. **Test OTP Flow**:
   - Enter phone: `2125551234`
   - Click "Send OTP"
   - **Button should disable with countdown**
   - Check alert for OTP code
   - Enter OTP and verify
5. Complete order successfully

#### 🇬🇧 UK Testing (New)
1. Set allowed regions to "UK Only" or "Global"
2. Go to checkout and select COD
3. **Verify country dropdown shows 🇬🇧 +44**
4. **Test OTP Flow**:
   - Enter phone: `7700900123`
   - Click "Send OTP"
   - **Button should disable with countdown**
   - Check alert for OTP code
   - Enter OTP and verify
5. Complete order successfully

### Timer Testing
1. **Send OTP for any country**
2. **Verify button changes**:
   - Text changes to "Resend in 30s", "Resend in 29s", etc.
   - Button becomes gray/disabled
   - Button cannot be clicked during countdown
3. **Wait for timer completion**:
   - After 30 seconds, button should re-enable
   - Text should return to "Send OTP"
   - Button should be clickable again
4. **Test timer reset on verification**:
   - Send OTP and start timer
   - Verify OTP successfully
   - Timer should clear immediately

### Troubleshooting

#### Country Dropdown Not Showing
- Check allowed regions setting in admin
- Ensure verification box is appearing
- Clear cache if using caching plugins

#### Wrong Country Options
- Verify allowed regions setting matches your needs
- Check if Global mode is enabled when you want all countries

#### Timer Not Working
- Check browser console for JavaScript errors
- Ensure jQuery is loaded
- Verify OTP timer duration setting in admin

#### Phone Validation Errors
- **India**: Must be 10 digits starting with 6-9
- **USA**: Must be 10 digits starting with 2-9
- **UK**: Must be 10 digits starting with 7
- Ensure country code matches phone number format

#### Twilio Multi-Country Issues
- Verify Twilio number supports target countries
- Check Twilio console for delivery reports
- Ensure sufficient Twilio balance for international SMS
- Test with Twilio's phone number lookup API

## 🔒 Security Features

- **Nonce Verification**: All AJAX requests secured
- **Session Management**: Secure session handling
- **Input Sanitization**: All inputs properly sanitized
- **OTP Expiration**: OTP expires after 5 minutes
- **Rate Limiting**: 30-second cooldown prevents spam requests
- **Region Validation**: Server-side validation of allowed countries
- **E.164 Format**: Proper international phone number formatting

## 🎨 Customization

### Styling
Edit `assets/cod-verifier.css` to customize appearance:
- Country dropdown styling
- Timer button states
- Colors and themes
- Layout and spacing
- Mobile responsiveness

### Timer Configuration
- Default: 30 seconds
- Range: 15-120 seconds
- Configurable via admin settings
- Applies to all countries

### Country Support
To add more countries:
1. Update validation rules in `ajax-handlers.php`
2. Add country option in `settings-page.php`
3. Update frontend validation in `script.js`
4. Add CSS flags and styling

## 📞 Support

### Common Multi-Country Issues
1. **Country not available**: Check allowed regions setting
2. **Timer not working**: Verify JavaScript console for errors
3. **Wrong validation**: Ensure phone format matches country
4. **Twilio errors**: Check international SMS capabilities
5. **Session issues**: Check PHP session configuration

### Debug Mode
Enable WordPress debug mode in `wp-config.php`:
```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
```

Check `/wp-content/debug.log` for errors.

## 📝 Changelog

### Version 1.2.0 (Multi-Country Edition)
- **NEW**: Multi-country support (India, USA, UK)
- **NEW**: Country code dropdown with flags
- **NEW**: 30-second OTP resend timer with visual feedback
- **NEW**: Regional restrictions (Global, India, USA, UK)
- **NEW**: Enhanced phone number validation for all countries
- **NEW**: E.164 format support
- **IMPROVED**: Better error messages and user guidance
- **IMPROVED**: Enhanced Twilio integration for international SMS
- **IMPROVED**: Mobile responsive design for country selector
- **PRESERVED**: All existing Indian functionality remains intact

### Version 1.1.0
- **BREAKING**: Migrated from Fast2SMS to Twilio
- Added Twilio SDK integration
- Improved error handling and logging
- Enhanced admin configuration notices
- Better production readiness checks

### Version 1.0.0
- Initial release
- OTP verification via Fast2SMS (deprecated)
- Token payment via Razorpay
- Test and production modes
- Mobile responsive design
- WordPress security standards

## 📄 License

This plugin is licensed under GPL v2 or later.

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Make changes
4. Test thoroughly with all supported countries
5. Submit pull request

---

**Ready to sell fake-order-free COD products globally?** 🌍🚀

Test the plugin thoroughly in Test Mode with all supported countries, then switch to Production Mode with your Twilio and Razorpay credentials for real international customers!

### ⚠️ Important Notes for Existing Users

- **Backward Compatibility**: All existing Indian users will continue to work without any changes
- **Default Settings**: Plugin defaults to "India Only" mode to preserve existing functionality
- **Gradual Migration**: You can enable multi-country support when ready
- **No Breaking Changes**: Existing OTP logic and validation rules for India remain unchanged