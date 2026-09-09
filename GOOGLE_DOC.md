# T3N ADK community challenge — crumb-inbox

Paste this file into a public Google Doc. Superteam listing: [t3n-agent-build-challenge](https://superteam.fun/earn/listing/t3n-agent-build-challenge/). Deadline 16 Sep 2026 15:59 UTC. 2nd/3rd place = 50 USDC.

## Agent

**Repo:** https://github.com/HaydernCenterpoint/t3n-crumb-inbox

Enterprise agent that triages untrusted COOK / crumb / on-chain payment-request mail. It quotes claimed amounts and addresses. **It never sends funds.** Payment is a human Nightly / Crumbs handoff. T3N member-delegation is the enforcement: outbound HTTP and wallet effects need a user grant, not mail text.

Pairs with:

- Mermail skill PR: https://github.com/Nudgen-Marketing/mermail-skills/pull/212
- Crumbs cApp: https://hayderncenterpoint.github.io/crumbs-cookie-chain/

Handover: **pass this repo + operator DID to Terminal 3 to host.** We do not want to keep running it after the challenge.

## How to run (screenshots)

1. SSO: https://go.terminal3.io/adk-community — copy the API key (shown once) and DID.
2. `export T3N_API_KEY=...`
3. `npx tsx quickstart.ts` in this repo.
4. Screenshot the `did:t3n:...` line. Paste it below.

**DID:** _(paste here)_

**Screenshot:** _(paste here)_

The agent DID must be a **second** key from the same claim page. Reusing the tenant key is the usual `InsufficientCreditError`.

## Bugs found while following the docs

Source: https://docs.terminal3.io/developers/adk/get-started/quickstart and https://docs.terminal3.io/developers/adk/support/ai-coding-assistants

1. **Skill sample duplicates `fetchTrustedManifest` and `trustAnchor`.** The AI-assistant skill `quickstart.ts` imports `fetchTrustedManifest` twice and sets `trustAnchor` twice on `T3nClient`. The manual quickstart page is cleaner.
2. **WASM loading fails under Next.js / Vite / Webpack.** Docs already warn. Workaround: run `tsx quickstart.ts` as a plain Node script first.
3. **Agent DID credits start at zero.** Authenticating the tenant key and treating that DID as the agent hits `InsufficientCreditError`. The agent needs its own claim-page key. This belongs on the first success-path checklist.
4. **`trustAnchor` is required and throws at construction.** Omitting it does not fail later at handshake. The copy-paste sample still needs the field on the first try.
5. **SSO is the remaining gate.** Claim page is https://go.terminal3.io/adk-community.

## Maintainability

- No custom wallet code. T3N grants are the allowlist.
- Connection is one `quickstart.ts` (docs require keeping `t3n` / `tenantDid` in the same running script).
- ESM (`"type": "module"`) so the SDK top-level `await` samples parse.

## Superteam fields

- Email: _(paste)_
- DID generated from the page: _(paste)_
- Continue running? **Hand over to Terminal 3 to maintain**, with this repo as the handover pack.
- Google Doc: this document (public).
