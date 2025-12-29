# Nte9asmoCh9a — Family Tasks & Reports

A modern React Native app to organize family tasks, track time and progress, and view clear analytics with multilingual support.

## Highlights

- Family task management: assign, complete, and time‑track activities.
- Insights & analytics: daily, weekly, and overall reports with charts.
- Gamification: points and achievements to motivate participation.
- Multilingual UX: Arabic (RTL) and French, with runtime language switching.
- Notifications: push reminders for due tasks and updates.
- Offline‑aware: helpful network guard and graceful degradation.

## Screenshots

Below are sample screens from the application.

<p align="center">
  <img alt="App Screen 1" src="Screenshots/1.jpeg" width="150" />
  <img alt="App Screen 2" src="Screenshots/2.jpeg" width="150" />
  <img alt="App Screen 3" src="Screenshots/3.jpeg" width="150" />
  <img alt="App Screen 4" src="Screenshots/4.jpeg" width="150" />
  <img alt="App Screen 5" src="Screenshots/5.jpeg" width="150" />
</p>

## Tech Stack

- React Native + Expo
- Navigation: `@react-navigation/native`, `native-stack`
- Charts: `react-native-gifted-charts`
- i18n: `i18next`, `react-i18next`
- Notifications: `expo-notifications` (client) and Firebase configuration
- Storage: `@react-native-async-storage/async-storage`

## What the App Does

- Create and manage family tasks and activities.
- Assign tasks to family members and track completion.
- Track time spent on activities (where applicable).
- Generate clear reports and analytics (daily / weekly / overall).
- Support Arabic (RTL) and French with runtime language switching.
- Send reminders and updates via push notifications.
- Handle offline scenarios with a friendly fallback screen.

## Project Structure

High-level overview:

```text
app/
├─ Screenshots/           # Public screenshots (gallery)
├─ android/               # Android project (Gradle)
├─ ios/                   # iOS project (Xcode)
├─ assets/                # Static assets
└─ src/
   ├─ components/         # Reusable UI blocks
   ├─ config/             # App configuration & notifications bootstrap
   ├─ hooks/              # Data fetching, storage, notifications, online status
   ├─ lang/               # i18n configuration and locales (Arabic/French)
   ├─ navigation/         # Navigation helpers and setup
   ├─ screens/            # Route-level screens (auth, dashboard, network guard)
   ├─ state/              # Lightweight event bus (e.g., auth flows)
   └─ utils/              # Pure functions for reports and helpers
```

## Getting Started

### Prerequisites

- Node.js LTS
- Android Studio (SDK + emulator) for Android builds
- Xcode (macOS) for iOS builds

### Install & Run (Development)

```bash
# Install dependencies
npm install

# Start the Expo dev server
npm run start

# Launch on Android (device/emulator)
npm run android

# Launch on iOS (macOS only)
npm run ios
```

## Minimal Configuration (Non-sensitive)

- Backend base URL: update `src/hooks/ApiBaseUrl.js` to point to your API.
- Firebase client config: ensure `google-services.json` exists for Android (do not commit secrets publicly).
- App settings and theme: adjust `src/config/app.js`.

## Internationalization (i18n)

- Configuration: `src/lang/i18n.js`
- Resources: `src/lang/locales/ar/`, `src/lang/locales/fr/`
- RTL support: Arabic layout direction handled via `useAppDirection` and theming.

## Notifications

- Client setup: `src/config/notifications-handler.js`
- Device registration: `src/utils/registerPushToken.js`
- Uses Expo Notifications client APIs; server-side delivery should be implemented in your backend (not included here).

## Offline & Network Guard

- Online status: `src/hooks/useOnline.js`
- Guarded flows: `src/hooks/useOnlineGuard.js`
- Friendly fallback screen: `src/screens/NotNetWorkScreen.js`
