# Klasifikasi produk game

Halaman ini menjadi acuan parameter transaksi per `code`. **Klasifikasi tidak cukup satu sumbu “topup vs voucher”** — dipakai pemisahan: **Voucher** (produk kode digital), **Top-up tanpa zona**, dan **Top-up dengan zona**, lalu mapping ke field **`msisdn`** di API purchase.

Gunakan bersama [Contoh respons — produk game](./contoh-respons-produk-game.md) saat implementasi.

Di API **SOCX purchase**, parameter game biasanya dimapping ke satu field **`msisdn`** sesuai **aturan per `code`** (delimiter dan urutan dari tim SOCX/API).

## Ringkasan tiga kategori

| Kategori | Contoh | Arti `msisdn` di purchase | `sn` saat sukses |
|----------|--------|---------------------------|------------------|
| **Voucher** | Google Play, Roblox | **Nomor HP** (bukan user ID game) | **Kode voucher** untuk redeem |
| **Top-up — tanpa zona** | FF, AoV, dll. | **User / game ID** (+ parameter lain jika perlu), bukan nomor HP sebagai identitas akun | Biasanya kosong atau referensi; ikuti katalog |
| **Top-up — dengan zona** | ML (Mobile Legends) | **User ID + zone / server ID** dalam format yang disepakati | Biasanya kosong atau referensi; ikuti katalog |

### Voucher

Contoh: **Google Play**, **Roblox**.

- **`msisdn`** = **nomor handphone** pelanggan (bukan user ID game).
- **`sn`** pada respons transaksi **sukses final** = **kode voucher**; redeem memakai kode ini, bukan nilai `msisdn` request.

### Top-up — tanpa zona (non-zone)

Contoh: **Free Fire**, **Arena of Valor**, dll.

- Tujuan: isi saldo/item ke **akun game** memakai **ID pemain** (dan field tambahan jika diminta biller — selaraskan dengan katalog SOCX).
- **`msisdn`** memuat gabungan parameter akun game sesuai **tabel per `code`**, **bukan** pola voucher (nomor HP sebagai pengganti user ID).

### Top-up — dengan zona

Contoh: **Mobile Legends**.

- Butuh **zone ID** bersama **user ID**.
- Klien mengirim **`user_id` + `zone_id`** dalam satu nilai **`msisdn`** (format sesuai kesepakatan), lalu SOCX memproses pemisahan nilainya di sisi backend.

> **Catatan:** SKU lain dapat meminta **server_id** (bukan hanya zone) — isi **tabel per `code`** setelah ada katalog resmi.

## Aturan umum field API

| Item | Aturan |
|------|--------|
| `kategori_produk` | `VOUCHER` \| `TOPUP_NON_ZONA` \| `TOPUP_ZONA` (sesuai baris di atas). |
| `msisdn` | Selalu field utama purchase; isinya **bergantung kategori** (HP untuk voucher; ID game / gabungan ID+zona untuk top-up). Untuk top-up zona, klien mengirim nilai gabungan dan SOCX memproses pemisahannya. |
| `request_id` | Wajib unik untuk tiap order baru. |
| `sn` | Untuk **Voucher**: **kode voucher**. Untuk **Top-up**: referensi. |

## Tabel per `code` (isi operasional)

Baris di bawah diisi dari **katalog & uji nyata**. SKU baru ditambahkan seiring data resmi dari tim SOCX/API.

**Keterangan kolom:** `kategori` menunjukkan jenis produk. `format msisdn` menunjukkan format input di request. `payload` berisi field wajib (`code`, `msisdn`, `request_id`). Kolom `sn` menampilkan contoh nilai saat transaksi sukses (`rc=00`). Untuk alur pending (`rc=68`), lihat [Cek status](cek-status.md).

| code | nama | kategori | format `msisdn` | payload | contoh `msisdn` | `sn` (contoh sukses, `rc=00`) | status |
|------|------|----------|-----------------|---------|-----------------|-------------------------------|--------|
| `GPC5` | Google Play Rp 5.000 INDONESIA REGION Corporate | `VOUCHER` | nomor HP | `code`, `msisdn`, `request_id` | `081386467468` | `03GCXLDRDPPNBBEL` | Terverifikasi |
| `CFF5` | Free Fire 5 Diamond CORP | `TOPUP_NON_ZONA` | user ID | `code`, `msisdn`, `request_id` | `704899131` | `Free Fire 5 Diamonds /nickname : 死•ＩＲＦＡＮ•☠︎ refid: ab954b112f6c8aefbc6550167da150eb` | Terverifikasi |
| `CML5` | MLBB 5 Diamonds (5+0 Diamonds) Corporate | `TOPUP_ZONA` | gabungan user + zone | `code`, `msisdn`, `request_id` | `4189395759887` | `ZIYECH. . RefId: CS774320333ZGVLM0U8VI` | Terverifikasi |

## Panduan pengisian cepat

1. **Tentukan kategori** — Voucher, top-up tanpa zona, atau top-up dengan zona (bukan sekadar “topup atau voucher” saja).
2. **Untuk voucher** — pastikan **`msisdn`** = **nomor HP**; **`sn`** = kode redeem.
3. **Untuk top-up** — susun **`user_id`** dan **`zone_id` / `server_id`** jika perlu; mapping ke **`msisdn`** mengikuti ketentuan SOCX.
4. **Validasi reply** — simpan contoh `rc=00` dan `rc=68` per SKU.

## Catatan untuk tim integrasi

- **Voucher** dan **top-up game** adalah **alur bisnis berbeda**; jangan menyamakan `msisdn` voucher (nomor HP) dengan `msisdn` top-up (ID game).
- Jadikan **tabel per `code`** sebagai acuan handover agar tidak salah interpretasi parameter.
