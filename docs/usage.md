# Using ReachSocial

Base URL: `https://reachsocial.dev`

Public paid REST calls use USDC on Base through x402. You need an
x402-compatible client and wallet, with a spending limit you choose.

## 1. Choose an API

Discovery is free:

```bash
curl https://reachsocial.dev/v1/services
```

Use the service IDs and input fields returned by discovery.
See [available APIs and prices](https://reachsocial.dev/catalog).

## 2. Request a payment quote

Replace the example profile URL with the public profile you want.
Generate a new request key for each new task and keep it for recovery.

```bash
REQUEST_KEY="$(python3 -c 'import uuid; print(uuid.uuid4())')"

curl -i https://reachsocial.dev/v1/services/instagram.profile/execute \
  -H 'Content-Type: application/json' \
  -H "Idempotency-Key: $REQUEST_KEY" \
  --data '{"input":{"url":"https://www.instagram.com/example/"}}'
```

This unsigned request does not pay. When the service is available, it returns
HTTP `402` with a `PAYMENT-REQUIRED` header. Your x402 client checks the
service, amount, recipient, network, and token before authorizing payment.
It then resends the same input and key with a `PAYMENT-SIGNATURE` header.

Keep wallet secrets in your wallet integration, outside API inputs and chat.
Use the [agent guide](https://reachsocial.dev/agent.md) to help configure a client.

## 3. Use or recover the result

A successful request returns JSON with public metadata and source media links.
ReachSocial does not host the media files.

If a paid response goes missing, recover it within 30 days using the
original request key and unchanged input:

```bash
curl https://reachsocial.dev/v1/payments/recover/instagram.profile \
  -H 'Content-Type: application/json' \
  -H "Idempotency-Key: $REQUEST_KEY" \
  --data '{"input":{"url":"https://www.instagram.com/example/"}}'
```

Recovery returns the stored result without another payment. Keep the original
key private. If the outcome is uncertain, check recovery or contact support
before authorizing another payment.

[Full API docs](https://reachsocial.dev/docs/api) ·
[Support](https://reachsocial.dev/contact)
