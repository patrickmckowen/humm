# Humm

iOS app that guides users through science-backed humming to relieve sinus congestion. Real-time mic input drives a Metal shader for ambient visual feedback — no clinical meters or numbers.

Full product strategy: [docs/HUMM.md](docs/HUMM.md)

## Architecture

- **Workspace + SPM package** — `Humm.xcworkspace` wraps a thin app shell and `HummPackage`
- **All feature code goes in `HummPackage/Sources/HummFeature/`** — the app target (`Humm/`) is just the entry point, don't add code there
- **MV pattern, not MVVM** — no ViewModels. Use @State, @Observable, @Environment, @Binding directly in views. Business logic lives in services/clients, not view models
- **Swift 6.1+ strict concurrency** — async/await, actors, @MainActor. No GCD
- **iOS 17.0+**, iPhone only (v1)

## Domain Context

- Humming at ~130 Hz increases nasal nitric oxide 15x — this is the target frequency
- **Phase 1:** 4 days, ~1 hour/day of "good hum time" (in acceptable pitch + amplitude range)
- **Phase 2:** Ongoing, ~10 min/day maintenance
- Shader feedback: pitch → shape (blobby=low, balanced=zone, spiky=high), amplitude → size
- Sessions can run up to 1 hour — performance and battery drain matter

## Testing

Use **Swift Testing** framework (not XCTest). Tests live in `HummPackage/Tests/HummFeatureTests/`.

```swift
@Test func example() async throws {
    #expect(value == expected)
}
```

## Build & Run

Prefer **XcodeBuildMCP tools** over raw xcodebuild CLI when available. The workspace is `Humm.xcworkspace`, scheme is `Humm`.

## Key Paths

| What | Where |
|------|-------|
| App entry point | `Humm/HummApp.swift` |
| All feature code | `HummPackage/Sources/HummFeature/` |
| Tests | `HummPackage/Tests/HummFeatureTests/` |
| Build configs | `Config/*.xcconfig` |
| Entitlements | `Config/Humm.entitlements` (edit XML directly to add capabilities) |
| Product strategy | `docs/HUMM.md` |
