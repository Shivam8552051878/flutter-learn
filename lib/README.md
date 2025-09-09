Absolutely — here's the **rewritten and polished `lib/README.md`** that:

* ✅ Fully explains all three layers: `core/`, `features/`, `shared/`
* ✅ Uses correct GitHub-compatible folder tree formatting (no broken indentation)
* ✅ Is clean, copy-paste ready
* ✅ Includes working Dart examples
* ✅ Avoids broken nested code blocks

---

# 📖 `lib/README.md`

````markdown
# 📂 Flutter `lib/` Folder Structure Guide

This guide explains the source code structure inside the `lib/` directory.  
We follow a **feature-first architecture** designed to be **scalable, modular, and maintainable**.

---

## 🚀 Overview

The codebase is organized into three main layers:

- `core/` – Global configs (routing, themes, constants, utils)
- `features/` – Feature-specific modules (auth, home, etc.)
- `shared/` – Reusable components shared across features

---

## 📂 Folder Structure

```text
lib/
├── main.dart                     # App entry point
│
├── core/                         # Global modules (used across features)
│   ├── router.dart               # Centralized navigation
│   ├── theme/                    # Theme, typography, styles
│   ├── constants/                # Global constants (colors, strings, configs)
│   └── utils/                    # Utility functions (helpers, formatters)
│
├── features/                     # Feature-first modules
│   ├── auth/                     # Authentication
│   │   └── presentation/
│   │       ├── screens/          # UI Screens (Login, Signup)
│   │       └── routes.dart       # Auth routes
│   │
│   └── home/                     # Home dashboard
│       └── presentation/
│           ├── screens/          # UI Screens (Home)
│           └── routes.dart       # Home routes
│
└── shared/                       # Reusable shared components
    ├── widgets/                  # UI widgets (buttons, cards, etc.)
    └── extensions/               # Dart/Flutter extensions
````

---

## 🏁 Entry Point

### `main.dart`

Initializes the app and sets up the global router and theme.

```dart
import 'package:flutter/material.dart';
import 'core/router.dart';
import 'core/theme/app_theme.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      title: 'Flutter Template',
      theme: AppTheme.light,
      routerConfig: router,
    );
  }
}
```

---

## 🏛️ Core Layer

This is the **foundation of the app** — global code accessible by all features.

### 📌 `core/router.dart`

Centralized routing using `GoRouter`. Each feature registers its own routes.

```dart
import 'package:go_router/go_router.dart';
import '../features/auth/presentation/routes.dart';
import '../features/home/presentation/routes.dart';

final router = GoRouter(
  initialLocation: AuthRoutes.login,
  routes: [
    ...AuthRoutes.routes,
    ...HomeRoutes.routes,
  ],
);
```

---

### 📌 `core/theme/`

Defines app-wide theming (light/dark modes, color schemes).

```dart
import 'package:flutter/material.dart';
import '../constants/app_colors.dart';

class AppTheme {
  static ThemeData get light => ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: AppColors.primary),
        useMaterial3: true,
      );
}
```

---

### 📌 `core/constants/`

Global constants (colors, strings, sizes, etc.)

```dart
import 'package:flutter/material.dart';

class AppColors {
  static const primary = Colors.blue;
  static const secondary = Colors.green;
}
```

---

### 📌 `core/utils/`

General helper functions and utilities.

```dart
class Validators {
  static String? email(String? value) {
    if (value == null || value.isEmpty) return 'Email is required';
    if (!value.contains('@')) return 'Enter a valid email';
    return null;
  }
}
```

---

## 🧩 Features Layer

Each feature is **self-contained**: it owns its own UI, logic, routes, and possibly state management.

### Example: `features/auth/`

```text
features/auth/
└── presentation/
    ├── screens/
    │   ├── login_screen.dart
    │   └── signup_screen.dart
    └── routes.dart
```

---

### 📌 `routes.dart`

Defines routes for the auth feature.

```dart
import 'package:go_router/go_router.dart';
import 'screens/login_screen.dart';
import 'screens/signup_screen.dart';

class AuthRoutes {
  static const login = '/login';
  static const signup = '/signup';

  static List<GoRoute> routes = [
    GoRoute(
      path: login,
      builder: (context, state) => const LoginScreen(),
    ),
    GoRoute(
      path: signup,
      builder: (context, state) => const SignupScreen(),
    ),
  ];
}
```

---

### 📌 `login_screen.dart`

Example login UI navigating to the home screen.

```dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';
import '../../../home/presentation/routes.dart';

class LoginScreen extends StatelessWidget {
  const LoginScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Login')),
      body: Center(
        child: ElevatedButton(
          onPressed: () => context.go(HomeRoutes.home),
          child: const Text('Login → Home'),
        ),
      ),
    );
  }
}
```

---

## 🖼️ Shared Layer

Holds **reusable components** that are not feature-specific.

### 📌 `shared/widgets/`

Reusable UI components.

```dart
import 'package:flutter/material.dart';

class AppButton extends StatelessWidget {
  final String label;
  final VoidCallback onPressed;

  const AppButton({super.key, required this.label, required this.onPressed});

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      style: ElevatedButton.styleFrom(
        padding: const EdgeInsets.symmetric(horizontal: 24, vertical: 12),
      ),
      onPressed: onPressed,
      child: Text(label),
    );
  }
}
```

Usage:

```dart
AppButton(
  label: 'Sign In',
  onPressed: () => context.go('/home'),
)
```

---

### 📌 `shared/extensions/`

Extension methods to simplify code.

```dart
import 'package:flutter/material.dart';

extension ContextExtensions on BuildContext {
  void showSnack(String message) {
    ScaffoldMessenger.of(this).showSnackBar(
      SnackBar(content: Text(message)),
    );
  }
}
```

Usage:

```dart
context.showSnack('Login successful!');
```

---

## ✅ Best Practices

* ✅ **Feature-first**: Keep logic/screens/routes grouped by feature
* ✅ **Shared layer**: Only for reusable components
* ✅ **Core layer**: Global configuration only (router, theme, constants)
* ✅ **Routing**:

  * Each feature defines its own `routes.dart`
  * Global router (`core/router.dart`) aggregates them
* ✅ **Scalability**: Structure works for small projects and scales to large apps

---

📌 With this structure, your Flutter project is **modular, easy to navigate, and scalable** for growth.

```

---

Would you like me to:
- Create a matching `docs/architecture.md` to explain the reasoning and onboarding for new devs?
- Or generate a wiki page version for GitHub?

Let me know how far you want to take the documentation.
```
