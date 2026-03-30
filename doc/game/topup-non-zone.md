# Top-up — tanpa zona (non-zone)

Kategori ini dipakai untuk game yang cukup memakai **user/game ID** tanpa zone/server terpisah (kecuali catatan khusus di tabel).

## Daftar game non-zone

Beberapa contoh produk top-up game tanpa zona (cukup input user/game ID):

- Mobile Legend (MLBB)
- Free Fire
- PUBG Mobile
- Call of Duty Mobile (CODM)
- Garena Undawn
- Honor of Kings
- Arena of Valor (AOV)


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
