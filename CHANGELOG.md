# Changelog

All notable changes to Hajj Sonar are documented here. This release is the
"Sonar total rebuilt" — the app's screens, words, safety copy, and flows were
rebuilt as one coherent pass.

## v0.1-alpha.15.5 — 2026-10-18

### Dark mode matches the light scheme
- Dark theme is now a true dark-tone of the same sand/teal/gold palette as
  light mode (deep-teal base, gold accent), instead of a generic gray theme.
- Call screen, encrypted bubbles, and disabled states aligned to the new dark
  tokens; all text pairs verified against WCAG AA contrast.

### RTL and language
- Back/chevron arrows flip correctly in Arabic (RTL).
- In-app language toggle (English/Arabic) added above Appearance in Settings.
- Technical values (keys, sats, fingerprints) always render left-to-right.

### Payments and wallet
- Send flow shows a review screen before any money moves; no optimistic
  success state; legacy-wallet path keeps pending checks before spending.
- Scan sheet classifies destination QRs and shows a review sheet; unsupported
  codes show a clear unsupported state.
- Wallet activity shows signed amounts, pending states that never guess, and
  mint status.

### Security and privacy
- Reconnect failures no longer leak raw error messages into public toasts.
- Relay benchmark reflects the current run only (no stale success carryover).
- No contact upload, no analytics, no third-party SDKs in the message path.

### Release engineering
- First-launch crash fixed (splash theme parent).
- Breez release gate removed so release builds ship without a Breez key;
  Lightning wallet renders Unavailable until you add your own key
  (breez.apiKey in local.properties, never committed).
- Signed with a local debug signature (not a store key) — install via
  "Install unknown apps".

## v0.1-alpha.15.4 — 2026-10-18

### A new look, everywhere
- Rebuilt the whole visual identity: dark-first Sonar theme, custom typography,
  consistent cards and spacing across every screen.
- Motion is now a first-class concern: animations respect your system-wide
  "reduce motion" setting, and the splash no longer flashes the wrong theme.
- Technical values (keys, fingerprints, sats amounts) always render
  left-to-right, even inside Arabic text.

### English and Arabic, fully
- Every user-facing string moved into a single translation catalog
  (352 keys, English + Modern Standard Arabic) with a generator and its own
  test suite, so screens can't silently ship raw untranslated text.
- Fresh installs launch Arabic-first; both languages are complete and the app
  supports right-to-left layouts, font scaling to 200%, and per-locale app
  language.

### Chats and contacts
- Redesigned chat and message rows on the shared design tokens.
- Microphone-off states during calls are localized and labeled for screen
  readers.
- Sticker packs and direct-message media sheets were reworked with proper
  loading/removing states.
- Contact profiles now show the full safety-verification sentence: compare
  security numbers in person or on a call, and nobody can sit in the middle.
  Deleting a contact says plainly what is removed locally and what that
  consequence is.

### Groups
- Group info was rebuilt: member verification status, mute controls, and a
  leave flow with an honest confirmation that names the group and what leaving
  does, with safe default focus on Cancel.
- Join requests show clear, named actions.

### Calls
- The call screen is always dark with high-contrast text for readability.
- The mute control exposes a precise accessibility name ("Mute microphone")
  while keeping simple visible Mute/Unmute labels.
- End call is visually separated from other controls and keeps a large,
  comfortable touch target.
- Reduced motion stops decorative pulse effects without touching controls.

### Settings, profile, and backup
- Settings got clean toggle semantics, precise diagnostics wording, and
  destructive actions that name their scope before you confirm.
- Your profile uses shared identity cards: key, fingerprint, QR, and payment
  address with copy/share actions that return the raw value; handle claim
  shows its loading, failure, and success states; the nickname is edited
  separately from your secure identity.
- Backup speaks honestly: scope, destination, last success, and limits are
  visible; encryption explains that phones hold the data rather than claiming
  a serverless fantasy; a dry run says exactly "no changes"; destructive
  actions name their effect; auto-backup network and cellular rules are
  preserved.

### Relay and security
- Reconnect failures no longer leak raw technical error text into public
  toasts — you get fixed, human copy while diagnostics stay in logs.
- Relay speed-test results now reflect only the current run; a previously
  good relay can no longer mask a changed, failing one.

### Wallet and payments
- Wallet activity was rebuilt with a clear balance/activity/receive
  hierarchy, signed amounts, distinct empty and offline states, and pending
  items that never guess whether funds are yours.
- Sending payment now shows a review step before any confirm; money only
  moves on your explicit confirm tap, and legacy-wallet payments check
  dependencies and pending state first.
- Payment statuses render with left-to-right amount styling.
- Scanning a payment QR opens a review sheet that classifies the destination
  and only continues on a clearly named action; the viewfinder is functional
  and respects motion settings.

### Performance and privacy fundamentals
- Chat lists and transcripts still paint from local storage first; sync runs
  in the background, so opening a chat never waits on the network.
- Performance-sensitive screens kept their efficient list recycling and
  derived state; nothing in the redesign slowed launch, send, or scroll.
- No contact upload, no analytics, no third-party SDKs in the message path.

### Release engineering
- First launch on Android 12+ no longer crashes (the splash theme's parent
  was the wrong platform base — fixed).
- Release builds are produced, zipaligned, and signed; the signed APK
  (arm64-v8a / armeabi-v7a) is attached to this release and was installed and
  smoke-tested on a physical device.
- The Lightning wallet ships inactive by default: add your own free
  [Breez API key](https://breez.technology/request-api-key/) to
  `apps/sonar/local.properties` (`breez.apiKey=…`) to enable it.

### Notes
- Alpha: behaviors may change; verify backups. Desktop and Apple surfaces are
  not in this build yet.
