# Pembelian — Game (JSON POST)

Request dan respons khusus kategori game via `POST /purchase`.

## Request

```json
{
  "url": "https://indotechapi.socx.app/reseller/api/v1/purchase",
  "body": {
    "code": "CML5",
    "msisdn": "1386630284",
    "request_id": "26031700000301"
  }
}
```

## Response sukses (contoh)

```json
{
  "ref_id": "b624qp05nhnh52066",
  "status": "1",
  "code": "CML5",
  "hp": "4189395759887",
  "price": "1440",
  "message": "Success",
  "balance": "83844592",
  "tr_id": "2505577",
  "rc": "00",
  "sn": "ZIYECH. . RefId: CS774320333ZGVLM0U8VI"
}
```

## Catatan

- Format `msisdn` mengikuti aturan per SKU game.
- Detail klasifikasi top-up/voucher ada di [klasifikasi produk game](./klasifikasi-produk-game.md).
- Untuk daftar `rc` gagal, lihat [kode respons (RC)](./kode-respons.md).
