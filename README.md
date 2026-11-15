<a href="https://reachsocial.dev/">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/logo.svg">
    <img src="assets/logo-light.svg" alt="ReachSocial" width="72" height="72">
  </picture>
</a>

# ReachSocial

[![Glama MCP connector](https://img.shields.io/badge/Glama-MCP%20connector-6D4AFF)](https://glama.ai/mcp/connectors/dev.reachsocial/reach-social-one-api-for-social-media-data)
[![Official MCP Registry](https://img.shields.io/badge/MCP%20Registry-listed-0f766e)](https://registry.modelcontextprotocol.io/?q=dev.reachsocial%2Fsocial-data)

**One API for social media data.**

Get public profiles, posts, and feeds from Instagram, X, TikTok, YouTube, Facebook, and Reddit.
Connect once and get JSON your app or AI agent can use.

**Start with 100 successful calls free.** Verify your email and get one API key for all 15 public APIs. No card or wallet is needed to start.

| Credit pack | Card or native USDC on Base | Successful calls |
|---|---|---:|
| Starter | $10 / 10 USDC | 1,000 |
| Growth | $50 / 50 USDC | 10,000 |
| Scale | $100 / 100 USDC | 25,000 |

Purchased credits never expire. No subscriptions or automatic top-ups.
Keyless x402 calls cost **0.05 USDC each**, with no account or API key.

[**Start free**](https://reachsocial.dev/app) | [Available APIs](https://reachsocial.dev/catalog) | [Pricing](https://reachsocial.dev/pricing) | [API docs](https://reachsocial.dev/docs/api)

### Give your agent the link

Copy this into your AI agent:

```text
Read https://reachsocial.dev/agent.txt and help me get public social data.
Check signup availability first. Reuse my existing access, or guide me through
email verification when available and save my API key securely without showing it.
Ask for my email only if needed, and ask which URL/data I need. Use Free credits only.
Briefly explain current credit packs and optional USDC pay-per-call access.
Get my approval before spending paid credits or USDC. Keep replies short,
preserve request keys for recovery, and keep secrets out of chat.
```

Email-first setup needs HTTP tools and private credential storage. Agents check
current signup availability and offers at `/v1/billing/packs`.
A compatible wallet/signer is needed only for keyless USDC payments.
REST and MCP support managed API keys; OAuth prepaid spending requires explicit consent.

[API tutorial](docs/usage.md) | [OpenAPI](https://reachsocial.dev/openapi.json) | [Documentation license](LICENSE)
