# PREPAID — Pulsa & Data

Transaksi prepaid (pulsa dan data) — **request**, **respons** (pending & sukses), dan catatan field. RC lengkap: [Kode respons (RC)](kode-respons.md).

## Kontrak HTTP

**Endpoint**

```
https://indotechapi.socx.app/reseller/api/v1/purchase
```

**Header**

```
Authorization: Bearer <JWT>
Content-Type: application/json
```

**Body** — `code`, `msisdn`, `request_id`. Untuk pulsa, `msisdn` = nomor HP pelanggan (digit, biasanya `08...`).

---

## Request — contoh pulsa

```json
{
  "code": "CTSEL5",
  "msisdn": "081234567890",
  "request_id": "26031600002200"
}
```

Alternatif (format HTTP):

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

---

## Request — contoh data

```json
{
  "code": "CTMINI13",
  "msisdn": "082121250591",
  "request_id": "26031600002201"
}
```

---

## Respons — pending (`rc = 68`)

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

| Field | Contoh | Keterangan |
|-------|--------|------------|
| `sn` | `""` | Belum ada serial — normal saat pending |
| `message` | teks pending | Jangan anggap sukses ke end-user |

Lanjutkan dengan [`POST /status`](cek-status.md) memakai `request_id` yang sama (atau callback jika disepakati).

---

## Respons — sukses (`rc = 00`)

### Pulsa (contoh ringkas)

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

### Pulsa (contoh spesifikasi / validasi dengan tim SOCX)

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

### Data (contoh)

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

---

## Catatan

- Respons gagal dan kode lain: [Kode respons (RC)](kode-respons.md).
