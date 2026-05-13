# 6Valley Zender Gateway

![Status](https://img.shields.io/badge/STATUS-RELEASED-success?style=for-the-badge)

🛠 Free Zender WhatsApp & SMS OTP integration for 6Valley v16.2 with admin panel support.

---

## Features

- WhatsApp OTP support using Zender
- SMS OTP support using Android devices
- SMS Gateway / Credits mode support
- Dynamic admin panel configuration
- Integrated directly into 6Valley SMS settings
- OTP template support
- SIM slot selection support
- Compatible with 6Valley v16.2
- Laravel based integration
- No external package required

---

## What is 6Valley?

6Valley is a multi-vendor eCommerce platform where you can manage multiple stores such as fashion, digital products, electronics, sports, home & living, health & beauty, and many more in one system.

6Valley includes:

- Laravel backend & admin panel
- Website frontend
- Flutter mobile app for Android & iOS

---

## Product URL

https://6amtech.com/

---

# ⚠ IMPORTANT

Before making any changes, you MUST take a full backup of:

1. All modified project files
2. The complete database

Recommended backup:

- Full website files backup
- Full MySQL database export

This modification changes core SMS gateway functionality. A backup is strongly recommended before installation.

---

## Installation

This modification is very easy to install.

### Step 1

Download the latest release ZIP file.

---

### Step 2

Upload the contents of the `install` folder to the root directory of your 6Valley project.

Example:

```text
/public_html/
/var/www/html/
/www/wwwroot/domain.com/

Overwrite existing files if asked.

Step 3

Import:

sql/zender_gateway.sql

into your 6Valley database using phpMyAdmin or MySQL CLI.

Required Manual Changes
1) Edit SMSModuleController.php

Open:

app/Http/Controllers/Admin/ThirdParty/SMSModuleController.php

Find:

foreach (['releans', 'twilio', 'nexmo', '2factor', 'msg91', 'hubtel', 'paradox', 'signal_wire', '019_sms', 'viatech', 'global_sms', 'akandit_sms', 'sms_to', 'alphanet_sms'] as $gateway) {

Replace with:

foreach (['releans', 'twilio', 'nexmo', '2factor', 'msg91', 'hubtel', 'paradox', 'signal_wire', '019_sms', 'viatech', 'global_sms', 'akandit_sms', 'sms_to', 'alphanet_sms', 'zender_gateway'] as $gateway) {

Save the file.

2) Edit GlobalConstant.php

Open:

app/Enums/GlobalConstant.php

Search:

DEFAULT_SMS_GATEWAYS

You will see:

'alphanet_sms',

Add below it:

'zender_gateway',

Save the file.

3) Clear Laravel Cache

Run:

php artisan optimize:clear
Admin Panel Configuration

Go to:

Admin Panel → 3rd Party → SMS Module

Enable:

Zender Gateway
Configuration Fields
Field	Description
Site URL	Your SenderGate / Zender URL
API Key	Your Zender API Secret
Service	1 = WhatsApp OTP, 0 = Mobile SMS
WhatsApp	WhatsApp account ID
Device	Android Device ID
Gateway ID	SMS Gateway ID
Slot	SIM Slot
OTP Template	OTP message template
Test Configuration
https://sendergate.com
WhatsApp Mode

Set:

Service = 1

Required:

API Key
WhatsApp Account ID

API Endpoint used:

/api/send/whatsapp
SMS Device Mode

Set:

Service = 0

Required:

Device ID
SIM Slot

API Endpoint used:

/api/send/sms
Android Requirements

For SMS mode:

Set SenderGate as default SMS app
Disable battery optimization
Enable background activity
Enable auto-start
Allow SMS permissions

Recommended for:

Samsung
Pixel
Motorola

Some Xiaomi/Redmi/HyperOS devices may restrict SMS verification.

Updating

Updating is very easy.

Step 1

Download latest release ZIP.

Step 2

Upload updated files to your 6Valley root directory.

Step 3

Run:

php artisan optimize:clear

Done.

Troubleshooting
SMS Failed But API Sent = Yes

This usually means Android blocked SMS verification.

Check:

SMS permissions
Default SMS app
Battery restrictions
Background permissions
WhatsApp OTP Not Sending

Check:

WhatsApp account ID
API Key
SenderGate connection
WhatsApp session status
Laravel Cache Issues

Run:

php artisan optimize:clear
Tested On
6Valley v16.2
PHP 8.2 / 8.3
Laravel
SenderGate
Android 12 / 13 / 14 / 15
Disclaimer

This project is not affiliated with 6amTech or the official 6Valley developers.

Use this modification at your own risk.

Always keep backups before installation or updating.

License

MIT License
