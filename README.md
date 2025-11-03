# Expensify

Expensify is a cross-platform expense tracker built with Flutter that helps individuals keep their spending in check. The app pairs a polished UI with Firebase-backed data storage so you can securely log, review, and analyze your income and expenses on the go.

## Features
- **Secure authentication**: Firebase Authentication ensures only registered users can access their personal finance data.
- **Expense management**: Add, edit, and delete transactions with detailed descriptions and amounts from `HomeScreen` via `ExpenseController`.
- **Income and earnings insights**: Review totals on the dedicated `EarnedScreen`, aggregating positive entries from Firestore in real time.
- **Spending overview**: Track outflows through the `SpentScreen` and view categorized lists rendered with smooth animations.
- **Interactive analytics**: Visualize trends with charts powered by `fl_chart`, enabling quick comparison of spending patterns.
- **Offline-ready caching**: Cloud Firestore persistence keeps data accessible even when the device temporarily loses connectivity.
- **Modern UX**: Lottie animations, custom widgets, and GetX-based navigation provide an engaging, responsive experience.

## Tech Stack
- **Framework**: Flutter
- **State Management & Navigation**: GetX (`GetMaterialApp`, bindings, controllers)
- **Backend**: Firebase (Authentication, Cloud Firestore)
- **UI Enhancements**: Lottie, `fl_chart`
- **Language**: Dart

## Architecture Overview
- **GetX bindings and controllers** in `lib/app/pages/**/controller/` organize presentation logic and dependency injection.
- **Reusable widgets** in `lib/app/pages/**/widget/` encapsulate UI components (e.g., `ExpenseHeader`, `HomeListItem`).
- **FirestoreService** in `lib/firebase/firestore/firestore.dart` centralizes all Firestore CRUD operations.
- **Routing** in `lib/routes/routes.dart` defines the navigation map, with each screen registered as a `GetPage`.

## Project Structure
```
lib/
  app/
    common/           # Shared UI elements such as the navigation drawer
    pages/
      splash_screen/  # Startup flow and Firebase initialization
      login_screen/   # Authentication UX and controller
      register_screen/
      home_screen/    # Dashboard, expense list, floating action button
      earned_screen/  # Income summary and positive transaction list
      spent_screen/   # Expense focus and negative transaction list
      graph_screen/   # Analytics with charts
      profile_screen/ # User profile & account management
  firebase/
    firestore/        # FirestoreService abstraction
  routes/             # GetX route declarations
  firebase_options.dart
```

## Getting Started
- **Prerequisites**
  - **Flutter SDK**: Version `^3.8.0-265.0.dev` (matching the `pubspec.yaml` constraint)
  - **Firebase project** configured for Android, iOS, and optional web targets
  - **Dart** tooling bundled with Flutter

- **Setup**
  1. **Clone the repository**
     ```bash
     git clone https://github.com/<your-org>/expensify.git
     cd expensify
     ```
  2. **Install dependencies**
     ```bash
     flutter pub get
     ```
  3. **Configure Firebase**
     - Create a Firebase project and enable Authentication (Email/Password) and Cloud Firestore.
     - Run `flutterfire configure` to regenerate `lib/firebase_options.dart` for your project IDs.
     - For manual setup, ensure platform-specific configuration files (`google-services.json`, `GoogleService-Info.plist`, `firebase-app-id.json`) are added to the respective directories.
  4. **Provision Firestore rules** (sample)
     ```txt
     rules_version = '2';
     service cloud.firestore {
       match /databases/{database}/documents {
         match /users/{userId}/expenses/{document=**} {
           allow read, write: if request.auth != null && request.auth.uid == userId;
         }
       }
     }
     ```

## Running the App
- **Debug build**
  ```bash
  flutter run
  ```
- **Target a specific platform** (example)
  ```bash
  flutter run -d android
  flutter run -d ios
  flutter run -d chrome
  ```

## Testing
- **Widget tests**: Add tests under `test/` and run with
  ```bash
  flutter test
  ```
  (No automated tests are committed yet; contributions are welcome.)

## Roadmap
- **[ ]** Add budget categories and tagging.
- **[ ]** Export transactions to CSV or PDF.
- **[ ]** Automated recurring transaction scheduling.
- **[ ]** Push notifications for spending alerts.

## Contributing
- **Fork & branch**: Create feature branches from `main`.
- **Follow style**: Adhere to `analysis_options.yaml` rules and GetX best practices.
- **Pull requests**: Include screenshots or screen recordings for UI-facing changes.

## License
This project does not yet specify an open-source license. Please contact the maintainers before using the code in production or distributing modified versions.

## Contact
- **Product**: Expensify – Personal Expense Tracker
- **Maintainer**: Replace with your team or owner details (email, LinkedIn, etc.)
