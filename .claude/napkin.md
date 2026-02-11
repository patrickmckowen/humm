# Napkin

## Corrections
| Date | Source | What Went Wrong | What To Do Instead |
|------|--------|----------------|-------------------|
| 2026-02-11 | user | XcodeBuildMCP scaffolded project as workspace+SPM package | Humm is a simple iOS app — use standard Xcode project structure, no SPM wrapper |
| 2026-02-11 | self | Assumed iOS 26 wasn't released yet | iOS 26 is current — check dates before making claims about release status |

## User Preferences
- Prefers standard Xcode project structure over workspace+SPM for simple apps
- Uses BabyTime as reference architecture for iOS projects
- Wants iOS 26 as deployment target
- iPhone only for v1
- Approachable concurrency with default @MainActor isolation

## Patterns That Work
- Standard xcodeproj with 3 targets (app, unit tests, UI tests) — no workspace needed
- Directory layout: Models/, Views/, Components/, Design/ inside app target
- xcconfig files in Config/ for build settings (Shared/Debug/Release/Tests)
- Entitlements inside app target directory (Humm/Humm.entitlements)
- File system synchronized groups (buildable folders) — no manual file refs
- Swift Testing for unit tests, XCTest for UI tests
- XcodeBuild MCP CLI needs `mcp` subcommand for stdio server: `npx -y xcodebuildmcp@latest mcp`

## Patterns That Don't Work
- SPM package wrapper for a simple iOS app (unnecessary complexity, public access modifiers everywhere)
- Workspace wrapping xcodeproj + local package for single-app projects

## Domain Notes
- Target humming frequency: ~130 Hz (sinus cavity resonance)
- Audio input: AVAudioEngine for real-time pitch detection + amplitude
- Shader: Metal-based cymatic mesh gradient, inspired by Apple Mindfulness
- Feedback encoding: pitch -> shape (blobby=low, balanced=zone, spiky=high), amplitude -> size
- "Good hum time" accumulates only when user is in acceptable pitch+amplitude range
- Phase 1: 4 days x ~1hr/day, Phase 2: ongoing ~10min/day
- No prescribed inhale/exhale cadence — users find their own rhythm
- Sessions can run up to 1 hour — performance and battery matter

## Architecture Notes
- All code in Humm/ — organized by role
- MV pattern (no ViewModels) — @State, @Observable, @Environment
- iOS 26 deployment target, iPhone only
- Swift 6 with approachable concurrency, default @MainActor
- Build configs in Config/*.xcconfig
