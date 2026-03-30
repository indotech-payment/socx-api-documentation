# Top-up — dengan zona

Kategori ini dipakai untuk game yang memerlukan **user ID + zone/server ID**.

## Definisi

- `msisdn` dikirim sebagai nilai gabungan user + zone sesuai format SKU.
- SOCX/Indotech memproses pemisahan nilai tersebut di backend.
- Contoh kategori ini: Mobile Legends (`CML5`).

## Tabel operasional (zona)

| code | nama | kategori | format `msisdn` | payload | contoh `msisdn` | `sn` (contoh sukses) | status |
|------|------|----------|-----------------|---------|-----------------|----------------------|--------|
| `CML5` | MLBB 5 Diamonds (5+0 Diamonds) Corporate | `TOPUP_ZONA` | gabungan user + zone | `code`, `msisdn`, `request_id` | `4189395759887` | `ZIYECH. . RefId: CS774320333ZGVLM0U8VI` | Terverifikasi |

## Daftar game
- Mobile Legends


## Request 

```json
{
  "code": "CML5",
  "msisdn": "4189395759887",
  "request_id": "b624qp05nhnh52066"
}
```

## Respons sukses

```json
{
  "data": {
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
}
```

## Respons pending

```json
{
  "code": "CML5",
  "msisdn": "4189395759887",
  "request_id": "b624qp05nhnh52066",
  "rc": "68",
  "trxid": 2505577,
  "price": 1440,
  "balance": 83844592,
  "message": "PENDING, Transaksi sedang diproses"
}
```

## Test Case

- Validasi format gabungan `msisdn` (user+zone) sesuai SKU.
- Jika `rc=68`, polling `POST /status` sampai final.
- Ulangi `request_id` yang sama harus idempotent.
- Referensi skenario umum: [Skenario pengujian](../transaksi-direct/skenario-pengujian.md).

