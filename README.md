# Humm

iOS app that guides users through science-backed humming to relieve sinus congestion.

## Project Setup

- **Xcode 26+**, Swift 6, iOS 26
- **iPhone only** (v1)
- Open `Humm.xcodeproj` directly

### Targets

| Target | Type | Framework |
|--------|------|-----------|
| `Humm` | App | SwiftUI |
| `HummTests` | Unit tests | Swift Testing |
| `HummUITests` | UI tests | XCTest/XCUITest |

### Build Settings

- **Concurrency:** Approachable mode, default `@MainActor` isolation
- **Code signing:** Automatic
- **Info.plist:** Auto-generated
- **Build configs:** `Config/*.xcconfig`

### Directory Layout

```
Humm/
├── Humm.xcodeproj/
├── Humm/
│   ├── HummApp.swift          # @main entry
│   ├── ContentView.swift      # Root view
│   ├── Humm.entitlements
│   ├── Assets.xcassets/
│   ├── Models/                # Data models, services
│   ├── Views/                 # Feature views
│   ├── Components/            # Reusable UI components
│   └── Design/                # Design tokens, modifiers
├── HummTests/                 # Unit tests (Swift Testing)
├── HummUITests/               # UI tests (XCUITest)
└── Config/                    # xcconfig build settings
```

## AI Assistant Rules

- **Claude Code**: `CLAUDE.md`
- **Cursor**: `.cursor/*.mdc`
- **GitHub Copilot**: `.github/copilot-instructions.md`
