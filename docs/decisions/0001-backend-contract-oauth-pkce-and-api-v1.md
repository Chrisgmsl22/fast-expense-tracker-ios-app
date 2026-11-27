# ADR-0001: The app logs in with OAuth 2.1 and PKCE and reads data from `/api/v1`

Date: 2026-11-27
Status: Accepted
Follows: FET [ADR-0028](https://github.com/Chrisgmsl22/fast-expense-tracker/blob/main/docs/decisions/0028-native-clients-use-oauth-with-pkce.md) and FET [spec 0009](https://github.com/Chrisgmsl22/fast-expense-tracker/blob/main/docs/specs/0009-auth-module-better-auth.md)

## Context

The FET backend already decided how a native client connects. This repo is that client, so
the decision binds it. This ADR records the client side and the state of the backend on
2026-11-27.

## Decision

1. Login opens the FET `/login` page in the system browser sheet
   (`ASWebAuthenticationSession`). The app never shows its own password field and never
   sees the password. No embedded web view.
2. The app is a public OAuth client. It has no client secret. It uses the authorization
   code flow with PKCE and a private-use redirect URI.
3. The app stores the tokens in the Keychain only.
4. The app calls the versioned JSON API at `/api/v1` with a Bearer access token. It
   refreshes the token on expiry. A refused refresh ends the session and shows the
   "Session ended" screen.
5. The Swift API client comes from the OpenAPI document that FET publishes. We do not
   hand-write request and response types.
6. The server owns every money rule. The app shows `actualExpenditure` and never computes
   it.

## Consequences

- The app depends on 2 FET work items that are not built yet. See
  [`backend-contract.md`](../reference/backend-contract.md) for the live state.
- Screens can be built first on mock data that follows the contract. A slice that does this
  says so in its Plan block.
- Old app builds stay on phones, so a breaking API change needs `/api/v2`, not an edit.
- Sign in with Apple becomes required only if the app adds a third-party login (App Store
  guideline 4.8, as FET ADR-0028 notes). FET spec 0013 drafts Google sign-in, so this needs
  a check before that feature reaches the app.

## Open

- Which OAuth client library, or none. FET spec 0009 names AppAuth-iOS and asks if it is
  still maintained. [ADR-0004](./0004-tech-stack.md) decides.
