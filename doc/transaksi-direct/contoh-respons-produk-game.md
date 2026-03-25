# Contoh respons — produk game (top-up / voucher)

Pada level API SOCX, **format request/response sama** dengan pulsa: `code`, `msisdn`, `request_id`, dan field respons yang identik. Perbedaannya ada pada **arti bisnis** field:

| Field | Pulsa | Produk game (umum) |
|-------|--------|---------------------|
| `code` | SKU pulsa (mis. `HSA5`) | SKU game atau voucher digital (**dari katalog — TBD**) |
| `msisdn` | Nomor HP | **Tergantung SKU:** nomor HP (mis. voucher Google Play / Roblox) atau gabungan **user ID game** / **user ID + zone** untuk top-up — lihat [Klasifikasi produk game](klasifikasi-produk-game.md) |
| `sn` | Referensi / serial pulsa | Untuk voucher: **kode voucher**; untuk top-up: sering kosong atau referensi |

**Penting:** Spesifikasi `socx.md` tidak membedakan endpoint; pastikan untuk setiap produk Anda memakai **`code` dan format `msisdn` yang benar** sesuai daftar dari SOCX (akan dilengkapi lewat inquiry / dokumen produk).

## Request (JSON POST) — contoh berdasarkan data transaksi

### 1) Voucher (contoh: Google Play / Roblox)

`msisdn` diisi **nomor HP** pelanggan.

```json
{
  "code": "GPC5",
  "msisdn": "081386467468",
  "request_id": "km17l40myg3z51097"
}
```

### 2) Top-up non-zona (contoh: FF / AoV)

`msisdn` diisi **user ID game** sesuai aturan SKU.

```json
{
  "code": "CFF5",
  "msisdn": "704899131",
  "request_id": "eg45e10xpxge57760"
}
```

### 3) Top-up zona (contoh: ML)

`msisdn` diisi gabungan **user ID + zone/server ID** sesuai format SKU.

```json
{
  "code": "CML5",
  "msisdn": "4189395759887",
  "request_id": "b624qp05nhnh52066"
}
```

## Respons — pending (contoh CML5)

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

## Respons — sukses (contoh GPC5 / voucher)

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

## Respons — sukses (contoh CML5 / top-up zona)

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

## Respons — sukses (contoh CFF5 / top-up non-zona)

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

## Catatan `sn` per kategori

| Kategori | Arti `sn` |
|----------|-----------|
| Voucher (contoh `GPC5`) | Kode voucher untuk redeem |
| Top-up (contoh `CML5`, `CFF5`) | Referensi/bukti transaksi dari provider (tetap simpan) |

## “List game”

- **Bukan bagian endpoint purchase:** daftar SKU game / denom diharapkan dari **inquiry / API katalog** (menyusul, dari tim SOCX).
- Dokumen ini hanya menjamin **kontrak respons transaksi** konsisten dengan pulsa; variasi isi `sn` dan `message` per produk didokumentasikan per SKU setelah katalog tersedia.

## Tabel checklist per SKU game

| `code` | Nama produk | Format `msisdn` | Isi `sn` saat sukses | Catatan |
|--------|-------------|-----------------|----------------------|---------|
| `GPC5` | Google Play Rp 5.000 | nomor HP | `03GCXLDRDPPNBBEL` | Voucher |
| `CML5` | MLBB 5 Diamonds (5+0) | gabungan user + zone | `ZIYECH. . RefId: CS774320333ZGVLM0U8VI` | Top-up zona |
| `CFF5` | Free Fire 5 Diamond | user ID | `Free Fire 5 Diamonds /nickname ... refid ...` | Top-up non-zona |

Salin tabel ini ke spreadsheet internal dan lengkapi bersama tim produk/API agar integrator punya **spesifikasi reply tertentu** per game.
