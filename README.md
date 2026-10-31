# NoVazhe | نوواژه

A Kotlin Multiplatform learning app with child profiles, vocabulary activities, mini-games, and a Ktor backend.

## Overview

NoVazhe combines child profiles, vocabulary content, custom words, and learning activities in a Kotlin Multiplatform project. The repository includes a shared Compose UI, Android and iOS entry points, and a Ktor server for authentication, content, and progress.

## Highlights

- Parent and child flows with individual child profiles.
- Custom vocabulary with image and audio interfaces.
- Quiz, memory, color-sorting, shadow-matching, and face-game code.
- Server-side progress tracking.
- Shared networking and models across platform targets.

**Stack:** Kotlin · Compose Multiplatform · Ktor · Koin · Exposed · H2 / PostgreSQL

## Project structure

| Module | Responsibility |
| --- | --- |
| `composeApp/` | Shared Compose UI and platform integrations |
| `shared/` | Models, repositories, and HTTP client |
| `iosApp/` | iOS application entry point |
| `server/` | Ktor API, persistence, and content serving |

## Getting started

Clone the default development branch:

```bash
git clone --branch new https://github.com/imhmdrz/novazhe.git
cd novazhe
```

### Android

Use Android Studio with JDK 17 and Android SDK 36. The app targets devices running API 24 or newer.

```bash
./gradlew :composeApp:assembleDebug
```

Run the app from Android Studio after Gradle sync. On Windows, use `gradlew.bat`.

### Server

On macOS or Linux:

```bash
export JWT_SECRET="$(openssl rand -hex 32)"
./gradlew :server:run
```

For Windows, set a nonempty `JWT_SECRET` environment variable before running `gradlew.bat :server:run`.

The server defaults to a local H2 database. PostgreSQL configuration is available in `server/src/main/kotlin/mohaamadreza/saemipour/no/vazheh/database/DatabaseConfig.kt` and is selected with `USE_POSTGRES=true`.

Review the platform implementation of `getBaseUrl()` when connecting a device to your server. An Android emulator typically reaches the host at `http://10.0.2.2:8080`; an iOS simulator can use `http://localhost:8080`. A physical device needs a reachable host address.

Content files and their public URLs are configured separately. Follow [the content setup guide](server/content/README.md) for `CONTENT_DIR`, `CONTENT_BASE_URL`, and seeding details.

### iOS

Use macOS and Xcode. Open the project under `iosApp/`, configure signing for your development team if needed, and run an iOS target.

Platform targets are configured in the build files; runtime behavior should be checked separately on each platform.
