# Top-up — tanpa zona (non-zone)

Kategori ini dipakai untuk game yang cukup memakai **user/game ID** tanpa zone/server terpisah (kecuali catatan khusus di tabel).

## Daftar produk & akun uji

| Kode (`code`) | Produk | Akun testing (`msisdn`) |
|---------------|--------|-------------------------|
| `PUBGC60` | AOV 40 VOUCHER | `208937006531741` |
| `CODC31` | CODM 31 CP | `7919258494310370169` |
| `CFF5` | Free Fire 5 Diamond | `704899131` |
| `CML5` | MLBB 5 Diamonds (5+0 Diamonds) | `2890873339499` (user `289087333`, server `9499`, gabungan per format SKU) |
| `GUC80` | Garena Undawn 80 RC | `13001106293` |
| `PUBGC60` | PUBG MOBILE 60 UC | `5233371716` |
| `HOKC16` | Honor of Kings 16 Tokens | `11644792630330055579` |


`CML5` (MLBB) secara klasifikasi termasuk **top-up dengan zona** — detail format gabungan ID + server ada di [Top-up — dengan zona](topup-zona.md).

## Request

```json
{
  "code": "CFF5",
  "msisdn": "704899131",
  "request_id": "eg45e10xpxge57760"
}
```

## Respon

```json
{
  "data": {
    "ref_id": "eg45e10xpxge57760",
    "status": "1",
    "code": "CFF5",
    "hp": "704899131",
    "price": "900",
    "message": "Success",
    "balance": "47269920",
    "tr_id": "2434954",
    "rc": "00",
    "sn": "Free Fire 5 Diamonds /nickname : 死•ＩＲＦＡＮ•☠︎ refid: ab954b112f6c8aefbc6550167da150eb"
  }
}
```

## Test Case

- Request valid (`code`, `msisdn`, `request_id`) menghasilkan `rc=00` atau `rc=68`.
- `msisdn` berisi huruf/spasi harus gagal validasi.
- Ulangi `request_id` yang sama harus idempotent (respons sama).
- Referensi skenario umum: [Skenario pengujian](../transaksi-direct/skenario-pengujian.md).
