# Humm

iOS app that guides users through science-backed humming to relieve sinus congestion. Real-time mic input drives a Metal shader for ambient visual feedback — no clinical meters or numbers.

Full product strategy: [docs/HUMM.md](docs/HUMM.md)

## Architecture

- **Standard Xcode project** — `Humm.xcodeproj` with 3 targets (app, unit tests, UI tests)
- **All code lives in `Humm/`** — organized by role (Models/, Views/, Components/, Design/)
- **MV pattern, not MVVM** — no ViewModels. Use @State, @Observable, @Environment, @Binding directly in views. Business logic lives in services/clients, not view models
- **Swift 6 with approachable concurrency** — async/await, @MainActor by default, @concurrent for background work. No GCD
- **iOS 26+**, iPhone only (v1)

## Domain Context

- Humming at ~130 Hz increases nasal nitric oxide 15x — this is the target frequency
- **Phase 1:** 4 days, ~1 hour/day of "good hum time" (in acceptable pitch + amplitude range)
- **Phase 2:** Ongoing, ~10 min/day maintenance
- Shader feedback: pitch → shape (blobby=low, balanced=zone, spiky=high), amplitude → size
- Sessions can run up to 1 hour — performance and battery drain matter

## Testing

Use **Swift Testing** framework (not XCTest) for unit tests. UI tests use XCTest/XCUITest.

```swift
@Test func example() async throws {
    #expect(value == expected)
}
```

## Build & Run

Prefer **XcodeBuildMCP tools** over raw xcodebuild CLI when available. Open `Humm.xcodeproj` directly (no workspace needed).

## Key Paths

| What | Where |
|------|-------|
| App entry point | `Humm/HummApp.swift` |
| Root view | `Humm/ContentView.swift` |
| Data models & services | `Humm/Models/` |
| Feature views | `Humm/Views/` |
| Reusable UI components | `Humm/Components/` |
| Design tokens & modifiers | `Humm/Design/` |
| Unit tests | `HummTests/` |
| UI tests | `HummUITests/` |
| Build configs | `Config/*.xcconfig` |
| Entitlements | `Humm/Humm.entitlements` |
| Product strategy | `docs/HUMM.md` |
