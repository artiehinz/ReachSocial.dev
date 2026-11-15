# Using ReachSocial

Base URL: `https://reachsocial.dev`

## Start free

Open the [workspace](https://reachsocial.dev/app), enter your email, and paste
the verification code on the same page. Save the API key when it appears.
Your account gets 100 successful calls once, shared across all 15 public APIs.
No wallet or card is required.

To let an agent set this up, give it the [agent guide](https://reachsocial.dev/agent.txt).
It needs HTTP tools and private credential storage. Never put keys in chat.

## Use your API key

Discover APIs and inputs with `GET /v1/services` and `GET /v1/services/{service_id}`.
Use `Authorization: Bearer YOUR_API_KEY` in your client's protected settings.
For curl, the examples use an owner-only config file containing that header:

```text
header = "Authorization: Bearer YOUR_API_KEY"
```

Keep the file private and replace the path below. Generate and save a random
request key before each new task:

```bash
REACHSOCIAL_REQUEST_KEY="$(python3 -c 'import uuid; print(uuid.uuid4())')"

curl --config /path/to/private/reachsocial-curl.conf \
  https://reachsocial.dev/v1/account/execute/instagram.profile \
  -H 'Content-Type: application/json' \
  -H 'X-Maximum-Credits: 0' \
  -H "Idempotency-Key: $REACHSOCIAL_REQUEST_KEY" \
  --data '{"url":"https://www.instagram.com/nasa/"}'
```

`X-Maximum-Credits: 0` allows Free calls and stops before spending purchased
credits. After approving paid usage, set it to `1` for a single request.
One successful call uses one credit, including a cache hit or a bounded feed.
Invalid inputs, definite failures, and recovery consume no additional credit.

The same key works across Instagram profile/post/feed/highlight, X profile/post/feed,
TikTok profile/feed/video, YouTube channel/feed/video, Facebook profile, and Reddit post.
Private and on-hold services are excluded. Manage key scopes, limits, rotation,
and revocation in the workspace.

## Credit packs and batches

Buy Starter ($10 / 10 USDC for 1,000 calls), Growth ($50 / 50 USDC for 10,000),
or Scale ($100 / 100 USDC for 25,000) inside the workspace. Card payments are
processed by InstaGet. Purchased credit never expires; no automatic top-ups.
Anonymous USDC packs save a private spending/recovery capability before payment
and work across APIs without signup.

Mixed batches support 1–1,000 items within a 1 MiB request. Quote with
`POST /v1/batches/quote`, submit with `POST /v1/batches`, then poll progress,
paginate results or download NDJSON. Set `maximum_credits=0` for Free-only batches.
Direct keyless USDC batches cost 0.05 USDC per item with one quoted payment.
Cancellation stops undispatched items and preserves reusable unused value.
See [typed batch contracts](https://reachsocial.dev/openapi.json).

## Keyless USDC calls

An x402-compatible client and wallet can pay **0.05 native USDC on Base** per call,
without an account or API key. Save a different request key for each new task:

```bash
REACHSOCIAL_REQUEST_KEY="$(python3 -c 'import uuid; print(uuid.uuid4())')"

curl -i https://reachsocial.dev/v1/services/instagram.profile/execute \
  -H 'Content-Type: application/json' \
  -H "Idempotency-Key: $REACHSOCIAL_REQUEST_KEY" \
  --data '{"input":{"url":"https://www.instagram.com/nasa/"}}'
```

This unsigned request does not pay. When available, the service returns HTTP
402 with a `PAYMENT-REQUIRED` header. Your x402 client checks the service, exact
amount, recipient, network, and token before authorizing payment, then resends
the unchanged input and key with its payment proof. Keep wallet secrets private.

## Recover results

Account-key calls use `POST /v1/account/requests/recover`, authenticated with the
same API key and original `Idempotency-Key`. Batches use `POST /v1/batches/recover`.
For keyless single calls, use `POST /v1/payments/recover/{service_id}` with the
original key and unchanged `{"input":{...}}` body.

Recovery never starts another payment. Keep original keys and anonymous credit
capabilities private. If settlement or dispatch is uncertain, recover the
original task or contact support before authorizing another payment.
Results are retained for 30 days; unused credit outlives result expiry.

Results contain provider-accessible public metadata and source media links.
Cache windows vary; data is not guaranteed real-time and media URLs can expire.
X feeds are not guaranteed chronological. ReachSocial does not host media files.

[Full API docs](https://reachsocial.dev/docs/api) | [Support](https://reachsocial.dev/contact)
