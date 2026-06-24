# TODO

## Security (before launching on app.industrialtreasures.com)
- [ ] **Replace the front-end login with real authentication.**
  The current login (`industrial` / `123` in `index.html`) is a UI gate only — the
  credentials are visible in page source and anyone can still POST directly to the
  `…/dev/ingest` endpoint with curl. It is NOT real security.
  - Protect the API itself, not just the UI. Options:
    - API Gateway + **Amazon Cognito** user pool (proper login, tokens).
    - Or, minimum viable: an **API key / Lambda authorizer** on the API Gateway route
      so the endpoint rejects unauthenticated requests.
  - Once the API is protected, the front end sends the auth token with each request.

## Backend correctness (CORS)
- [ ] **Add `Access-Control-Allow-Origin` to the Lambda's error return paths.**
  Success (200) responses include it, but the 404 ("SKU not found") and 400 paths do
  not — so the browser blocks them and the frontend can't read the real status.
  Add the header to every `return` in the Lambda, then redeploy.
- [ ] **Preflight allowed-methods.** `OPTIONS` response currently returns
  `Access-Control-Allow-Methods: OPTIONS` only — should be `OPTIONS,POST`. Update the
  OPTIONS method's Integration Response header mapping in API Gateway and redeploy.

## Features (nice to have)
- [ ] Item preview (name/price/image) before sending, to confirm the right SKU.
- [ ] Per-channel result feedback (BigCommerce ✓ / eBay ✓ / Etsy ✗) instead of one combined message.
- [ ] Recent activity log of recently listed SKUs + status.
- [ ] Add Chairish and Facebook Marketplace channels (in the backend spec, not yet in UI).
- [ ] Status view backed by the DynamoDB cross-reference matrix (DRAFT / LIVE / SOLD).
- [ ] Mark-sold / delist button.
