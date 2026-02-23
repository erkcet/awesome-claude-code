# CLAUDE.md — Mobile App Template

<!-- Copy this file to your project root as CLAUDE.md and customize it. -->
<!-- This template covers React Native. For Flutter, adjust commands and structure. -->

## Project Overview

- **Name:** <!-- Your app name -->
- **Description:** <!-- One-liner about what this app does -->
- **Framework:** React Native 0.74+ <!-- or Flutter -->
- **Platforms:** iOS, Android
- **Language:** TypeScript
- **Navigation:** React Navigation 6 <!-- or Expo Router -->
- **State management:** Zustand <!-- or Redux Toolkit, Jotai, MobX -->

## Commands

| Action | Command |
|--------|---------|
| Install deps | `npm install` |
| Start Metro | `npm start` |
| Run iOS | `npm run ios` |
| Run Android | `npm run android` |
| Run tests | `npm test` |
| Lint | `npm run lint` |
| Type check | `npx tsc --noEmit` |
| Install iOS pods | `cd ios && pod install && cd ..` |
| Clean build (iOS) | `cd ios && xcodebuild clean && cd ..` |
| Clean build (Android) | `cd android && ./gradlew clean && cd ..` |
| Build release (iOS) | `npx react-native run-ios --mode Release` |
| Build release (Android) | `cd android && ./gradlew assembleRelease` |

## Project Structure

```
src/
├── app/                  # App entry, providers, navigation
│   ├── App.tsx
│   └── navigation/       # Navigation stacks and tabs
├── screens/              # Screen components (one per route)
│   ├── HomeScreen.tsx
│   ├── ProfileScreen.tsx
│   └── SettingsScreen.tsx
├── components/           # Reusable UI components
│   ├── ui/               # Primitives (Button, Input, Card)
│   └── features/         # Feature-specific components
├── hooks/                # Custom React hooks
├── services/             # API calls and external integrations
├── store/                # State management (Zustand stores)
├── utils/                # Helper functions
├── types/                # Shared TypeScript types
├── constants/            # App constants, theme, colors
└── assets/               # Images, fonts, icons
ios/                      # Native iOS project (Xcode)
android/                  # Native Android project (Gradle)
__tests__/                # Test files
```

## Conventions

- Use functional components with hooks — no class components.
- Screen components live in `src/screens/`, named `*Screen.tsx`.
- Use `PascalCase` for components, `camelCase` for functions/hooks, `UPPER_CASE` for constants.
- Keep platform-specific code in `*.ios.tsx` / `*.android.tsx` files when needed.
- Use `StyleSheet.create()` for styles — avoid inline style objects.
- Navigation params are typed via `RootStackParamList` in `src/types/navigation.ts`.
- API layer in `src/services/` — never call APIs directly from components.
- Test files colocated as `__tests__/ComponentName.test.tsx`.

## Platform-Specific Notes

### iOS
- Minimum deployment target: iOS 15.0
- Xcode workspace: `ios/YourApp.xcworkspace`
- Run `pod install` after adding native dependencies.

### Android
- Minimum SDK: 24 (Android 7.0)
- Build variant: debug / release
- Signing config in `android/app/build.gradle`.

## Environment Variables

<!-- Use react-native-config or expo-constants for env vars -->

| Variable | Required | Description |
|----------|----------|-------------|
| `API_URL` | Yes | Backend API base URL |
| `GOOGLE_MAPS_KEY` | No | Google Maps API key |
| `SENTRY_DSN` | No | Sentry error reporting DSN |

## Known Issues / Notes

<!-- Add anything Claude should know: native module issues, build gotchas, etc. -->
- Run `npx react-native doctor` to diagnose environment issues.
- After native dep changes, rebuild with `npm run ios` / `npm run android`.
