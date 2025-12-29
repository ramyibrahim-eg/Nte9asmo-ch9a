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

## Architecture Overview

The project follows a clean, modular structure with clear separation of concerns:

- Components: Reusable UI elements and feature blocks
  - `src/components/*` (e.g., reports cards, modals, profile blocks)
- Screens: Route-level views for auth and dashboard experiences
  - Auth: `src/screens/Auth/*` (Login, Verify OTP, Reset Password)
  - Dashboard: `src/screens/dashboard/*` (Notifications, Change Password)
  - Utilities: `src/screens/NotNetWorkScreen.js` (offline guard)
- Hooks: Data access and app mechanics
  - `src/hooks/useTasks.js`, `src/hooks/useFamilies.js`, `src/hooks/useReportsUserStats.js`
  - `src/hooks/useNotifications.js` (client push), `src/hooks/useAuthStorage.js`
  - `src/hooks/ApiBaseUrl.js` (backend base URL abstraction)
- Localization: Language configuration and resources
  - `src/lang/i18n.js` with `src/lang/locales/ar/` and `src/lang/locales/fr/`
- Navigation: Central navigation ref for programmatic routing
  - `src/navigation/navigationRef.js`
- State & Events: Lightweight bus for auth-related flows
  - `src/state/authBus.js`
- Utilities: Pure functions for analytics and time computations
  - `src/utils/computeReportsFromFamilies.js`
  - `src/utils/computeTimeReportsFromFamilies.js`
- Config & Notifications
  - `src/config/app.js` (UI/theme and app settings)
  - `src/config/notifications-handler.js` (client-side notifications setup)

This layout aims to keep business logic within hooks and utilities, UI within components/screens, and side effects isolated (notifications, storage, network).

## Project Structure

High-level overview (no internal file references):

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

## How It Works

- App bootstraps providers and navigation at startup.
- Authentication flow handles login, OTP verification, and password reset.
- Hooks encapsulate data access, storage, notifications, and connectivity.
- Reporting logic uses pure utilities to compute daily/weekly/overall stats.
- Internationalization supports Arabic (RTL) and French with dynamic switching.
- Notifications register device tokens and receive task reminders.
- Network guard detects offline state and shows a friendly fallback screen.

## Module Guide (Responsibilities)

- Components: UI-only, stateless where possible; accept data via props.
- Hooks: encapsulate fetching, storage, notifications; return data + actions.
- Utils: pure functions for stats/time calculations; easy to test.
- Screens: orchestrate hooks + components at the route level.
- Config: theming, app options, and notifications bootstrap.
- Lang: i18n setup and translation resources.
- Navigation: programmatic navigation helpers.

## Presentation Guide (How to explain to companies)

- Start with the problem: family task coordination and progress visibility.
- Demo the flow: assign tasks → track time → see reports → notifications.
- Walk through architecture: components, hooks, screens, utils, i18n, navigation.
- Highlight quality: separation of concerns, reusable hooks, pure utils, RTL/i18n.
- Show maintainability: clear folder naming, modular responsibilities, typed setup where applicable.
- Conclude with roadmap: performance, accessibility, additional locales, CI builds.

## Clean Code Practices

- Separation of concerns: UI, logic, and side effects live in distinct modules.
- Descriptive naming: Components, hooks, and utils are named by intent.
- Reusable hooks: Data fetching and persistence handled via composable hooks.
- Pure utilities: Reporting and time calculations are pure and unit-friendly.
- Localization-first: All user strings reside in i18n resources, enabling RTL.
- Defensive coding: Network guards and predictable error surfaces.

## Configuration Overview

- Backend base URL: set in your app settings.
- Android services: include the appropriate Google services configuration.
- App settings: adjust theme and general options as needed.

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

### Minimal Configuration (Non-sensitive)

- Backend base URL: update `src/hooks/ApiBaseUrl.js` to point to your API.
- Firebase client config: ensure `google-services.json` exists for Android (do not commit secrets publicly).
- App settings and theme: adjust `src/config/app.js`.

### Optional: EAS Build (Cloud CI)

If you use Expo Application Services (EAS), configure profiles in `eas.json` and run:

```bash
# Log in to Expo (interactive)
npx expo login

# Build for Android (choose a profile defined in eas.json)
npx eas build -p android --profile preview

# Build for iOS (requires macOS/Apple Developer setup)
npx eas build -p ios --profile preview
```

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
