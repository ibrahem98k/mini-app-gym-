# Infinity Gym Mini App 🏋️‍♂️

A premium gym subscription management mini-app designed for the **SUPERQI** super app ecosystem. Built with SvelteKit and Tailwind CSS.

## 📱 SUPERQI Integration

This mini app is fully integrated with the **SUPERQI** JSAPI bridge (`hylid-bridge`).

### Core Integrations:
- **Authentication**: Uses `my.getAuthCode` with `auth_base` and `USER_ID` scopes to allow seamless login for SUPERQI users.
- **QR Scanning**: Integrates `my.scan` in the main dashboard for scanning gym access or equipment codes.
- **Payments**: Uses `my.tradePay` for processing gym membership subscriptions directly within SUPERQI.
- **Native UI**: Utilizes `my.alert` for platform-native notifications and dialogs.

## ✨ Features

- **Welcome/Splash Screen**: A premium entry point that handles SUPERQI authorization on first load.
- **Subscription Management**: Browse and select from Monthly, Quarterly, or Yearly membership plans.
- **Real-time Status**: View your active subscription, progress bars, and renewal dates with a glassmorphism design.
- **Baghdad Location**: Localized for Baghdad, Iraq, featuring integrated Google Maps and QR directions.
- **Checkout Experience**: One-tap payment flow utilizing the SUPERQI payment gateway.

## 🛠️ Technical Stack

- **Frontend**: SvelteKit
- **Styling**: Tailwind CSS (Premium Dark/Red theme)
- **Bridge**: Hylid Bridge SDK (v2.10.0)
- **Storage**: `sessionStorage` for entrance logic and `localStorage` for auth tokens.

## 🌐 API Endpoints

The app communicates with the following backend services:
- **Auth**: `https://its.mouamle.space/api/auth-with-superQi`
- **Payment**: `https://its.mouamle.space/api/payment`

## 🚀 Development

```bash
# Install dependencies
npm install

# Run dev server with HMR
npm run dev
```

### Development Mode
When running outside of the SUPERQI environment, the app includes smart fallbacks for all native APIs (`my.*`), allowing for full UI development and testing in standard browsers.

---
*Created for the SUPERQI Mini App Ecosystem.*
