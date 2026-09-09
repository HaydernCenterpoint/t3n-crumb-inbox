# Docs / SDK bugs found while following the T3N ADK quickstart

Source: https://docs.terminal3.io/developers/adk/get-started/quickstart and the published AI skill at https://docs.terminal3.io/developers/adk/support/ai-coding-assistants

## 1. Skill sample duplicates `fetchTrustedManifest` and `trustAnchor`

**Still live 2026-09-09T15:01Z.** The AI-assistant skill's `quickstart.ts` (docs accordion) imports `fetchTrustedManifest` twice and sets `trustAnchor` twice on `T3nClient`. A first-timer following the skill literally gets a confusing duplicate. The manual quickstart page is cleaner.

## 2. WASM loading fails under Next.js / Vite / Webpack

Docs already warn: the SDK loads a WASM component and some bundlers parse it incorrectly. Confirmed as a known rough edge. Workaround: run `tsx quickstart.ts` as a plain Node script before putting the SDK in a bundled app.

## 3. Agent DID credits start at zero

If you authenticate the tenant key and then treat that DID as the agent, outbound/agent calls hit `InsufficientCreditError`. The agent needs its own claim-page key. Easy to miss; should be in the first success-path checklist, not only the pitfalls table.

## 4. `trustAnchor` is required and throws at construction

Omitting it does not fail later at handshake — `T3nClient` throws immediately. The skill file documents this; the copy-paste sample still needs the field on the first try.

## 5. Could not finish a live DID in this session

The claim page is SSO (`https://go.terminal3.io/adk-community`). This repo is the maintainable agent; the operator still has to mint the DID and paste it on Superteam (HUMAN_ONLY listing).
