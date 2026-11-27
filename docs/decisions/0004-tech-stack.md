# ADR-0004: Tech stack

Date: 2026-11-27
Status: Proposed

This ADR is a list of questions for Christian. No Swift code starts until it is Accepted.
Slice 0.3 resolves it.

## Context

The repo has no code. The machine has Xcode 26.5, Swift 6.3 and XcodeGen. It has no
SwiftLint and no SwiftFormat. The app is one iPhone target that talks to one backend.

## Proposal

| Area | Proposal | Why |
| --- | --- | --- |
| UI | SwiftUI | The designs use standard iOS sheets, lists and navigation |
| Project file | XcodeGen, `project.yml` committed, `.xcodeproj` generated | A text file that agents can edit and review. No merge conflicts in a project file |
| API client | Generated from FET's OpenAPI document | ADR-0001 item 5 |
| Tests | Swift Testing for units, XCTest UI tests for flows | Both ship with Xcode |
| Lint and format | SwiftLint and SwiftFormat, run in CI | Not installed yet. Needs sign-off as dependencies |
| CI | GitHub Actions on a macOS runner: build and test | The repo is public, so runner minutes are free |

## Open questions

1. **Minimum iOS version.** It decides which SwiftUI and Observation APIs we can use.
2. **OAuth client.** AppAuth-iOS, another maintained library, or our own small PKCE code on
   `ASWebAuthenticationSession`. FET spec 0009 asks if AppAuth-iOS is still maintained. That
   needs a check, not a guess.
3. **App architecture.** How views, state and the API client are layered, and where the
   test seams are. This becomes `docs/conventions/architecture.md`.
4. **Offline behavior.** The designs show optimistic rows and an offline state (Brief 4).
   That needs a local store or a request queue. Which one, and in which phase.
5. **Apple Developer account.** A paid account is needed for TestFlight and for a real
   device past 7 days. Which team id and bundle id.
6. **Languages.** FET has English and Spanish. Does the app ship both from the start.

## Consequences

Written when the ADR is accepted.
