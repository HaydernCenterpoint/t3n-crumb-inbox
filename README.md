# t3n-crumb-inbox

Enterprise agent for [Terminal 3](https://terminal3.io) / Superteam listing [Try out new docs to build a trusted agent with T3N](https://superteam.fun/earn/listing/t3n-agent-build-challenge/).

## What it does

Triages untrusted COOK / crumb / on-chain payment-request mail. Quotes claimed amounts and addresses. **Never sends funds.** Payment stays a human Nightly / Crumbs handoff. T3N member-delegation is the enforcement: outbound HTTP and wallet effects require a user grant, not mail text.

Pairs with:

- Mermail skill PR: https://github.com/Nudgen-Marketing/mermail-skills/pull/212
- Crumbs cApp: https://hayderncenterpoint.github.io/crumbs-cookie-chain/

## Why this is maintainable after the challenge

- No custom wallet code. T3N grants are the allowlist.
- Connection is one `quickstart.ts` file (docs require keeping `t3n` / `tenantDid` in the same running script).
- ESM (`"type": "module"`) so the SDK top-level `await` samples parse.
- Handover: pass the GitHub repo + operator DID. We would hand this to Terminal 3 to host.

## How to run

1. Claim a key (shown once): https://docs.terminal3.io/developers/adk/get-started/prerequisites/request-test-tokens
2. `npm install`
3. `export T3N_API_KEY=...`
4. `npx tsx quickstart.ts` — expect `did:t3n:...`

The agent DID must be a **second** key from the same claim page. Reusing the tenant key is the usual `InsufficientCreditError`.

## Bugs found in the docs (for the bounty)

See [BUGS.md](./BUGS.md).

## Superteam fields (human)

Paste [GOOGLE_DOC.md](./GOOGLE_DOC.md) into a public Google Doc, add the DID screenshot, then submit.

- Email
- DID from `quickstart.ts` output
- Continue running? **Hand over to Terminal 3 to maintain**, with this repo as the handover pack.
