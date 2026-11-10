# James Build APK — Cloud Edition

A starter project for an Android app that submits Android Studio project ZIPs to a cloud build service.

## What is included
- `android-app/`: Kotlin + Jetpack Compose Android client (ZIP picker, upload, build status, APK download).
- `server/`: Node.js/Express API scaffold for receiving projects and coordinating GitHub Actions.
- `worker/`: GitHub Actions workflow template for Gradle builds.
- `.env.example`: server configuration template.

## Important
This is a **starter source project**, not a prebuilt APK or a deployed cloud service. A real cloud build requires:
1. A GitHub repository containing this project.
2. A deployed backend with persistent file storage and HTTPS.
3. A GitHub token stored as a backend secret (never put it in the Android app).
4. Configure the Android app's `BASE_URL` to your deployed backend.
5. Complete the callback/artifact storage configuration before public use.

The backend intentionally refuses to start build requests until the required GitHub configuration is present.

## API contract
- `POST /api/builds` — multipart upload, field name `projectZip`
- `GET /api/builds/:id` — build state and log tail
- `GET /api/builds/:id/apk` — download completed APK

## Android build
Open `android-app/` in Android Studio, let Gradle sync, then run on an Android device.
Set `BASE_URL` in `android-app/app/build.gradle.kts` to your backend HTTPS URL.

## Backend local development
```bash
cd server
cp .env.example .env
npm install
npm start
```

The local backend can accept uploads for testing, but cloud dispatch needs GitHub configuration and publicly reachable persistent storage. See `server/README.md`.
