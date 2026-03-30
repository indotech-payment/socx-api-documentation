# Top-up — tanpa zona (non-zone)

Kategori ini dipakai untuk game yang cukup memakai **user/game ID** tanpa zone/server terpisah.

## Definisi

- Tujuan: isi saldo/item ke akun game memakai **ID pemain**.
- `msisdn` berisi ID akun game (bukan nomor HP voucher).
- `sn` pada sukses (`rc=00`) umumnya berupa referensi transaksi dari biller.

## Daftar game non-zone

- Mobile Legend (MLBB)
- Free Fire
- PUBG Mobile
- Call of Duty Mobile (CODM)
- Garena Undawn
- Honor of Kings
- Arena of Valor (AOV)

## Tabel operasional (non-zone)

| code | nama | kategori | format `msisdn` | payload | contoh `msisdn` | `sn` (contoh sukses) | status |
|------|------|----------|-----------------|---------|-----------------|----------------------|--------|
| `CFF5` | Free Fire 5 Diamond CORP | `TOPUP_NON_ZONA` | user ID | `code`, `msisdn`, `request_id` | `704899131` | `Free Fire 5 Diamonds /nickname : 死•ＩＲＦＡＮ•☠︎ refid: ab954b112f6c8aefbc6550167da150eb` | Terverifikasi |

## Request

```json
{
  "code": "CFF5",
  "msisdn": "704899131",
  "request_id": "eg45e10xpxge57760"
}
```

## Respons sukses

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
