# Top-up — dengan zona

Kategori ini dipakai untuk game yang memerlukan **user ID + zone/server ID**.

## Daftar game

- Mobile Legends
- game lain yang butuh zone/server sesuai katalog Indotech

## Request

```json
{
  "code": "CML5",
  "msisdn": "4189395759887",
  "request_id": "b624qp05nhnh52066"
}
```

> `msisdn` dikirim sebagai nilai gabungan user + zone sesuai format SKU; SOCX/Indotech memproses pemisahannya di backend.

## Respon

### Sukses (`rc=00`)

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

### Pending (`rc=68`)

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

