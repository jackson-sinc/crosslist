# crosslist

Cross-list tool for **Industrial Treasures** — type a SKU, pick channels
(BigCommerce / eBay / Etsy), and send it to the ingest API.

It POSTs to the ingest API with:

```json
{ "sku": "ANT-001", "target_channels": ["bigcommerce", "ebay", "etsy"] }
```

## Run

```bash
python3 -m http.server 8000
```
Open http://localhost:8000

Login: `industrial` / `123` (front-end demo gate — see `TODO.md` for the real-auth note).
The ingest endpoint is set in `INGEST_URL` inside `index.html`.
