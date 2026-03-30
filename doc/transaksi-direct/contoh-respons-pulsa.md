# Contoh respons — produk pulsa

Produk **pulsa** memakai `code` SKU pulsa (contoh dokumen: `CTSEL5`) dan `msisdn` = **nomor HP pelanggan** (hanya digit, biasanya dimulai `08...`).

## Request (JSON POST)

```http
POST /reseller/api/v1/purchase HTTP/1.1
Host: indotechapi.socx.app
Authorization: Bearer <JWT>
Content-Type: application/json

{
  "code": "CTSEL5",
  "msisdn": "08121231231",
  "request_id": "PULSA-20250322-0001"
}
```

## Skenario A — Pending (`rc = 68`)

Transaksi diterima; biller masih memproses.

```json
{
  "code": "CTSEL5",
  "msisdn": "08121231231",
  "request_id": "PULSA-20250322-0001",
  "rc": "68",
  "trxid": 16413,
  "price": 5400,
  "balance": 341890000,
  "sn": "",
  "message": "PENDING, Transaksi sedang diproses"
}
```

| Field | Nilai contoh | Interpretasi pulsa |
|-------|----------------|----------------------|
| `sn` | `""` | Belum ada serial; normal untuk pending |
| `price` | `5400` | Harga yang dikenakan untuk SKU ini |
| `message` | teks pending | Tampilkan status internal; jangan anggap sukses ke end-user |

**Langkah integrator:** panggil [`POST /status`](./cek-status.md) dengan `request_id` yang sama, atau tunggu notifikasi server-ke-server jika sudah disepakati (perlu konfirmasi).

## Skenario B — Sukses (`rc = 00`) — contoh spesifikasi

**Catatan:** Contoh di bawah menggambarkan bentuk respons yang **diharapkan** integrator; sesuaikan dengan respons real dari API setelah transaksi final (validasi dengan tim SOCX).

```json
{
  "code": "CTSEL5",
  "msisdn": "08121231231",
  "request_id": "PULSA-20250322-0001",
  "rc": "00",
  "trxid": 16413,
  "price": 5400,
  "balance": 341884600,
  "sn": "04092900001248875319",
  "message": "SUKSES"
}
```

Untuk penanganan berbagai macam gagal lain, lihat [kode respons (RC)](./kode-respons.md).