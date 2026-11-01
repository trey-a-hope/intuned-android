# inTuned (Android)

The Android client for inTuned, a 2016 social music app where people share "vibes": songs from their phone tagged with how they make them feel. It has a home timeline of shared songs, a notifications tab, user profiles with photo upload, and sign-up and login, all backed by Firebase. There's a separate [iOS prototype](https://github.com/trey-a-hope/intuned.ios).

## Features

- **Login and register** (`app/src/main/java/com/intuned/app/authentication/`) with Firebase Auth, with the signed-in user kept by `SessionManager`.
- **Home** (`home/HomeController.java`): tabs for the **Timeline** of vibes and **Notifications** (`TimeLineFragmentController`, `NotificationsFragmentController`), using sticky-header RecyclerViews.
- **Vibes**: each song carries title, artist, album, duration, file path and an MP3 download URL (`Models/DomainModels/Song.java`), plus an emotion (`Enums/Emotion.java`): happy, sad, angry, fearful or disgusted, each with its own color.
- **Profile** (`profile/ProfileController.java`): view and edit your profile and upload a photo to Firebase Storage.
- **Options** (`options/OptionsController.java`): app settings.
- Helpers for reading audio file headers (`Miscellaneous/WAVHeader.java`, `MP4Header.java`, `SoundFile.java`), images, dates and network checks, with "no internet" and "no results" views.

## How it works

User records and vibes live in the Firebase Realtime Database at the URL in `app/src/main/java/Configuration/AppConfig.java`, and profile images go to Firebase Storage under `Images/Users/<uid>`. Screens are plain Activities and Fragments ("Controllers"), with Volley and Gson for HTTP and JSON and Picasso for images.

## Tech stack

- Java, min SDK 16, target SDK 23 (Android Support Library 22/23, Gradle `compile` dependencies)
- Firebase: legacy `firebase-client-android` 2.5 (Realtime Database), Firebase Auth 9 and Storage
- Volley, Gson, Picasso, Joda-Time, Caldroid, CircleImageView, ObservableScrollView, DroidParts

## Getting started

Open the project in Android Studio. It was last built in 2016, so expect to update the Gradle plugin, replace `compile` with `implementation`, and migrate the support libraries to AndroidX before it builds on current tools. `local.properties` is committed with the original machine's SDK path, and Android Studio will rewrite it.
