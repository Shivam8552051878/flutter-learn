## Lib File Structure
---

## 📂 Recommended `lib/` Structure

```
lib/
│── main.dart              # App entry point
│
│── core/                  # App-wide configs & utilities
│   ├── constants/         # App constants (colors, strings, etc.)
│   ├── theme/             # Theme & styles
│   ├── utils/             # Helpers (formatters, validators, etc.)
│   └── router.dart        # App navigation setup
│
│── data/                  # Data layer
│   ├── models/            # Data models
│   ├── services/          # API, local storage, firebase, etc.
│   └── repositories/      # Business logic/data access
│
│── features/              # Feature-based folders
│   ├── auth/              # Example feature: Authentication
│   │   ├── presentation/  # UI (screens, widgets)
│   │   ├── application/   # State management (Bloc, Provider, Riverpod)
│   │   └── domain/        # Entities & logic
│   └── home/              # Example feature: Home screen
│
│── shared/                # Shared widgets/components
│   ├── widgets/           # Reusable UI components
│   └── extensions/        # Dart/Flutter extensions
```

This is **feature-first** (scalable for big apps).

---

## 📖 `lib/README.md`

```markdown
# 📂 Flutter `lib/` Folder Structure

This document explains how the source code inside `lib/` is organized.

---

## 🚀 Entry Point
- **`main.dart`** → The app entry point.  
  - Initializes dependencies.
  - Runs the root `App` widget.

---

## 🏛️ Core (Global Configs)
- **`core/constants/`** → App-wide constants (colors, strings, sizes).
- **`core/theme/`** → Theme, typography, light/dark mode configs.
- **`core/utils/`** → Utility functions and helpers.
- **`core/router.dart`** → Centralized app navigation (e.g., `GoRouter` or `Navigator 2.0`).

---

## 🗄️ Data Layer
- **`data/models/`** → Data models (e.g., `User`, `Product`).
- **`data/services/`** → External services (REST APIs, Firebase, local storage).
- **`data/repositories/`** → Repositories for managing business logic and abstracting data sources.

---

## 🧩 Features
Each **feature** has its own folder containing:
- **`presentation/`** → Screens, pages, and UI widgets.
- **`application/`** → State management (Bloc, Provider, Riverpod, etc.).
- **`domain/`** → Business logic, entities, and use cases.

Example:
```

features/auth/
│── presentation/  # LoginScreen, SignupScreen
│── application/   # AuthBloc, AuthProvider
│── domain/        # UserEntity, AuthUseCase

```

---

## 🖼️ Shared
- **`shared/widgets/`** → Common reusable UI components (buttons, inputs, loaders).
- **`shared/extensions/`** → Dart and Flutter extension methods for cleaner code.

---

## ✅ Guidelines
- Follow **feature-first structure** (group code by functionality, not type).  
- Keep **shared/ minimal** → only truly reusable components belong here.  
- Each feature should be **self-contained** (easy to move or delete).  

---

📌 This structure is designed to scale from small apps to large enterprise-level apps.
```

---

👉 Do you want me to also create a **pre-filled `lib/` skeleton with sample Dart files** (like `app_theme.dart`, `router.dart`, `auth_bloc.dart`, etc.) so your template repo is plug-and-play?

