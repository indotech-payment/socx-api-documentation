# Voucher Game

Kategori voucher menghasilkan kode redeem pada field `sn`.

Dokumentasi ini hanya mencakup **Google Play** dan **Roblox**. Produk voucher lain mengikuti katalog Indotech.

## Google Play

- `GPC5` — Google Play (contoh denominasi di lingkungan uji)

## Roblox

- Kode produk (`code`) mengikuti **katalog Indotech** untuk voucher Roblox (nomor HP di `msisdn` sama seperti voucher lain).

## Request

```json
{
  "code": "GPC5",
  "msisdn": "081386467468",
  "request_id": "km17l40myg3z51097"
}
```

## Respon

```json
{
  "ref_id": "km17l40myg3z51097",
  "status": "1",
  "code": "GPC5",
  "hp": "081386467468",
  "price": "4900",
  "message": "Success",
  "balance": "59412105",
  "tr_id": "2209728",
  "rc": "00",
  "sn": "03GCXLDRDPPNBBEL"
}
```

## Test Case

- `msisdn` untuk voucher harus nomor HP.
- `sn` harus terisi saat `rc=00` (kode voucher redeem).
- Ulangi `request_id` yang sama harus idempotent.
- Referensi skenario umum: [Skenario pengujian](../transaksi-direct/skenario-pengujian.md).
