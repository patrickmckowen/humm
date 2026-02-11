# Napkin

## Corrections
| Date | Source | What Went Wrong | What To Do Instead |
|------|--------|----------------|-------------------|

## User Preferences
- (accumulate here as you learn them)

## Patterns That Work
- XcodeBuild MCP scaffold creates workspace + SPM package architecture — use this structure, all feature code in HummPackage/
- XcodeBuild MCP CLI needs `mcp` subcommand for stdio server: `npx -y xcodebuildmcp@latest mcp`

## Patterns That Don't Work
- (approaches that failed and why)

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
- All feature code in HummPackage/Sources/HummFeature/
- App shell (Humm/HummApp.swift) is thin wrapper only
- MV pattern (no ViewModels) — @State, @Observable, @Environment
- iOS 17.0 deployment target
- Swift 6.1+ with strict concurrency
- Entitlements in Config/Humm.entitlements (declarative, AI-editable)
- Build configs in Config/*.xcconfig
