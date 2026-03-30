# Pembelian — Pulsa & Data (JSON POST)

Request dan respons khusus kategori prepaid (pulsa dan data) via `POST /purchase`.

## Request (contoh pulsa)

```json
{
  "code": "CTSEL5",
  "msisdn": "081234567890",
  "request_id": "26031600002200"
}
```

## Response sukses (contoh pulsa)

```json
{
  "code": "CTSEL5",
  "msisdn": "081234567890",
  "request_id": "26031600002200",
  "trxid": 2421510,
  "price": 5450,
  "rc": "00",
  "balance": 120995,
  "sn": "04092900001248875319",
  "message": "SUKSES"
}
```

## Request (contoh data)

```json
{
  "code": "CTMINI13",
  "msisdn": "082121250591",
  "request_id": "26031600002201"
}
```

## Response sukses (contoh data)

```json
{
  "code": "CTMINI13",
  "msisdn": "082121250591",
  "request_id": "26031600002201",
  "trxid": 2421511,
  "price": 14950,
  "rc": "00",
  "balance": 115545,
  "sn": "04042000001595621715",
  "message": "SUKSES"
}
```

## Catatan

- Endpoint: `{base_url}/purchase`
- Header: `Authorization: Bearer <JWT>`
- Untuk daftar `rc` gagal, lihat [kode respons (RC)](./kode-respons.md).
