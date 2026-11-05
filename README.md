# Google AI Pro (5 TB) — Two Years at Zero Cost

Fully automated dashboard for US$0.00 → 24 months.

[Português](readmePT.md)

## System requirements

1. Windows 10 or 11.
2. Google Chrome installed in its default location.
3. Python 3.10 or later installed with **Add Python to PATH** selected.
4. A US proxy enabled on your computer, or a proxy template entered on the left side of the dashboard.

## Quick start

1. On first use, double-click `1_首次运行_安装依赖并启动.bat` to install dependencies and start the dashboard.
2. For subsequent use, double-click `2_启动控制台.bat`.
3. Your browser will automatically open the dashboard at http://127.0.0.1:8765.

## Payment card and account setup

### Enter a payment card (required)

In the **Global configuration and inline tax-exempt card setup** section on the left, enter your own Visa or Mastercard that supports foreign-currency payments:

- Card number (16 digits).
- Expiration month and year, such as `08 / 29`.
- Security code (3-digit CVC).
- Cardholder's name in English.
- The tax-exempt ZIP code defaults to `97201` (Oregon, USA); the original instructions say no change is needed.

Click **💾 Save configuration**.

According to the original documentation, the script includes strict zero-cost protection and only clicks Subscribe when the checkout dialog confirms **US$0.00**, with no charge throughout the process.

### Import Google accounts in bulk

Paste accounts into the **Bulk account import** section on the right, one account per line. The following formats are supported:

```text
email----password----recovery_email
email----password----recovery_email----2FA_secret
email----password----2FA_secret
```

Click **➕ Import account list**.

### Start automated execution

Click **▶ Run** beside an individual account or **▶ Run all automatically** at the top.

The script is designed to perform these steps automatically:

1. Sign in to Google and complete recovery-email or 2FA verification.
2. Add the card inline with tax-exempt billing and activate the first 12-month free package (US$0.00).
3. Stack a second 6-month free package (US$0.00 → 18 months).
4. Stack a third 6-month free package (US$0.00 → a maximum of 24 months).
5. Open Google Play, cancel automatic renewal to retain the two-year entitlement until expiration, and take a screenshot for verification.

## Original links

- Card marketplace: https://faka.cdkey.si
- Blog: https://blog.caowo.de
- Telegram group: @Hello_Florence
