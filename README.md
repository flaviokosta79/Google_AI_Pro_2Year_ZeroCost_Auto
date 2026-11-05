# Google AI Pro (5 TB) — Two Years at Zero Cost

Fully automated dashboard for US$0.00 → 24 months.

[Português](README_Portuguese.md)

## What the application does, end to end

The application combines a local FastAPI dashboard (`app.py`) with a Playwright browser automation engine (`automation_engine.py`). Its intended result is to activate and stack Google AI promotional offers, then optionally cancel automatic renewal and record the subscription status.

1. **Configure the session.** The dashboard saves the target region, plan, automatic-renewal cancellation preference, proxy template and payment card in `config.json`.
2. **Load accounts.** Import Google credentials, optionally including a recovery email, a TOTP secret and an account-specific proxy. Existing accounts are updated when a matching normalized email is found. New accounts enter the pending queue.
3. **Choose execution.** Run one account or a sequential batch. The backend also accepts a starting step to skip earlier stages. The dashboard exposes logs, current steps, status and screenshots; accounts can be reset or removed, and stop requests are checked between pipeline stages.
4. **Prepare an isolated browser profile.** The engine validates required card fields, opens Chrome with a persistent profile per account, connects through Playwright and applies the selected proxy when configured. It attempts to identify the browser's outgoing IP and country before continuing.
5. **Sign in.** The engine fills Google login fields and attempts supported recovery-email, password and TOTP challenges using the imported account data.
6. **Attempt the promotional sequence.** It inspects Google Play subscriptions and attempts a 12-month offer followed by two 6-month offers, aiming for 24 months in total. The offer payloads also include a YouTube Premium trial add-on. The code modifies Google One page requests using embedded offer identifiers, handles payment-card entry and checks checkout text for a zero-cost amount. It uses existing subscription information to skip some stages and retries certain checkout attempts.
7. **Handle renewal and collect evidence.** If automatic cancellation is enabled, it attempts to cancel renewal in Google Play. It then revisits subscriptions, captures a final screenshot, extracts an expiration date when recognized, and records the detected plan and completion status.
8. **Keep the result available.** Account updates and results are written back to `config.json`; browser profiles remain in `profiles/`, and screenshots in `screenshots/`. Runtime logs are kept in memory. Exceptions handled by the pipeline are reported as account errors.

### Scope and current limitations

This describes the implemented flow, not a verified entitlement or guarantee of free service. Offer availability, eligibility, checkout behavior and the final expiration date depend on Google. The script contains fixed 2027/2028 date checks and page-text selectors, so its completion status and screenshots should be checked against the actual subscription page.

The full browser workflow currently targets Windows: Chrome discovery and process-management commands are Windows-specific. During cloud onboarding, only dependency installation and the Linux dashboard/API were validated; Google sign-in, checkout, offer stacking and cancellation were not executed.

## System requirements

1. Windows 10 or 11.
2. Google Chrome installed in its default location.
3. Python 3.10 or later installed with **Add Python to PATH** selected.
4. A US proxy enabled on your computer, or a proxy template entered on the left side of the dashboard.

## Quick start

1. On first use, double-click `1_install_dependencies_and_start.bat` to install dependencies and start the dashboard.
2. For subsequent use, double-click `2_start_dashboard.bat`.
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
