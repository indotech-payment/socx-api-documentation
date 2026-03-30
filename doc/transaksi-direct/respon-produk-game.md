# Respons produk game

Halaman ini khusus berisi contoh **respons** transaksi game.

## Field respons (umum)

| Field | Tipe | Keterangan |
|-------|------|------------|
| `code` | string | Kode produk game |
| `rc` | string | Kode hasil transaksi |
| `price` | string/number | Harga transaksi |
| `balance` | string/number | Saldo setelah transaksi |
| `sn` | string | Referensi biller / serial voucher (jika ada) |
| `message` | string | Pesan status |
| `trxid` / `tr_id` | number/string | ID transaksi |

## Respons pending (contoh `CML5`)

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

## Respons sukses

### 1) Game top-up (`CML5`)

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

### 2) Voucher game (`GPC5`)

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

## Catatan

- Untuk daftar berbagai kode gagal, lihat [kode respons (RC)](./kode-respons.md).
- Untuk klasifikasi parameter per `code` (voucher/top-up non-zona/top-up zona), lihat [klasifikasi produk game](./klasifikasi-produk-game.md).
