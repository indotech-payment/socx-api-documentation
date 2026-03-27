# Dokumentasi API Indotech (Reseller H2H)

Repositori ini berisi **dokumentasi teknis** untuk integrasi **Host-to-Host (H2H)** antara sistem Anda dan platform **Indotech** sebagai reseller. Dokumen ditulis dalam Bahasa Indonesia dan diorganisir per **kategori produk** serta **referensi teknis** (selaras sidebar MkDocs).

---

## Daftar isi

### Introduction & Transaction Flow

- [Ringkasan alur](doc/introduction-transaction-flow.md)
- [Pengenalan](doc/01-pengenalan.md)
- [Direct Purchase without Inquiry](doc/transaksi-direct/flow-direct-purchase-without-inquiry.md)
- [Direct Purchase with Inquiry](doc/transaksi-direct/flow-direct-purchase-with-inquiry.md)

### PREPAID (Pulsa, Data)

- [Ringkasan PREPAID](doc/prepaid/README.md) — request, respon, test case

### GAME

- [Ringkasan GAME](doc/game/README.md)
- [Top-up — tanpa zona (non-zone)](doc/game/topup-non-zone.md)
- [Top-up — dengan zona](doc/game/topup-zona.md)
- [Voucher](doc/game/voucher.md)
- [Klasifikasi & contoh respons (gabungan)](doc/transaksi-direct/klasifikasi-produk-game.md)

### EWALLET

- [Ringkasan EWALLET](doc/ewallet/README.md)
- [DANA (inquiry) — ringkasan](doc/ewallet/dana-inquiry.md)
- [DANA — Denom tetap](doc/ewallet/dana-inquiry-denom-tetap.md)
- [DANA — Denom Bebas](doc/ewallet/dana-inquiry-denom-bebas.md)

### Inquiry khusus

- [Inquiry PLN (`CPLN`)](doc/inquiry/inquiry-pln.md)

### Referensi teknis

- [Persiapan integrasi](doc/02-persiapan-integrasi.md)
- [Cek saldo](doc/transaksi-direct/cek-saldo.md) · [Pembelian JSON](doc/transaksi-direct/pembelian-json-post.md) · [HTTP / XML](doc/transaksi-direct/pembelian-http.md) · [Cek status](doc/transaksi-direct/cek-status.md)
- [Kode respons (RC)](doc/transaksi-direct/kode-respons.md)
- [Inquiry POST (JSON) — kontrak umum](doc/inquiry/inquiry-post.md)
- [Contoh respons pulsa](doc/transaksi-direct/contoh-respons-pulsa.md) · [Skenario pengujian](doc/transaksi-direct/skenario-pengujian.md)
- [Lampiran deposit tiket](doc/appendix-deposit-ticket.md)

**Beranda situs (MkDocs):** [doc/index.md](doc/index.md)

---

## Apa yang tercakup

| Area | Status | Keterangan |
|------|--------|------------|
| Introduction & alur transaksi | Tersedia | Direct purchase, inquiry, diagram flow |
| PREPAID (pulsa, data) | Tersedia | Request / respon / test case |
| GAME (top-up non-zone, zona, voucher) | Tersedia | Halaman per kategori + klasifikasi gabungan |
| EWALLET (direct purchase, DANA inquiry) | Tersedia | Termasuk denom tetap & open amount |
| Inquiry PLN | Tersedia | Contoh `CPLN` |
| Direct purchase (JSON / HTTP / XML) | Tersedia | `code`, `msisdn`, `request_id` |
| Cek saldo · status · RC | Tersedia | `GET /saldo`, `POST /status`, tabel RC |
| Skenario pengujian | Tersedia | Checklist QA |
| Deposit tiket | Lampiran | Di luar fokus direct purchase |
| Daftar harga / katalog lengkap | Menyusul | Perlu `code` resmi dari tim Indotech |

---

Detail lengkap: [Pengenalan](doc/01-pengenalan.md) · [Persiapan integrasi](doc/02-persiapan-integrasi.md).

---

## Daftar endpoint (quick reference)

| Metode | Path | Fungsi | Dokumentasi |
|--------|------|--------|-------------|
| `GET` | `/saldo` | Cek saldo deposit | [doc/transaksi-direct/cek-saldo.md](doc/transaksi-direct/cek-saldo.md) |
| `POST` | `/purchase` | Transaksi pembelian (JSON) — **disarankan** | [doc/transaksi-direct/pembelian-json-post.md](doc/transaksi-direct/pembelian-json-post.md) |
| `GET` / `POST` | `/http/purchase` | Pembelian via query atau form + `token` | [doc/transaksi-direct/pembelian-http.md](doc/transaksi-direct/pembelian-http.md) |
| `POST` | `/xml/purchase` | Pembelian format XML (`topUpRequest`) | [doc/transaksi-direct/pembelian-xml.md](doc/transaksi-direct/pembelian-xml.md) |
| `POST` | `/status` | Cek status by `request_id` | [doc/transaksi-direct/cek-status.md](doc/transaksi-direct/cek-status.md) |
| `POST` | `/deposit_ticket` | Buat tiket deposit | [doc/appendix-deposit-ticket.md](doc/appendix-deposit-ticket.md) |

**Idempotensi:** jika Anda mengirim ulang **`request_id` yang sama** dan transaksi itu sudah pernah diproses, API mengembalikan **respons yang sama** dengan transaksi tersebut (bukan transaksi baru).

**Pending (`rc = 68`):** transaksi diterima tetapi belum final; lanjutkan dengan polling **`/status`** dan/atau mekanisme callback jika sudah disepakati dengan tim Indotech (detail callback/XML `topUpReport` — review internal).

---

## Alur integrasi (disarankan)

1. **Persiapan:** whitelist IP, simpan JWT dengan aman, tentukan konvensi `request_id` (unik per order baru).
2. **Opsional:** `GET /saldo` sebelum transaksi besar.
3. **Purchase:** `POST /purchase` (atau jalur HTTP/XML jika sistem Anda mengharuskan).
4. **Jika `rc = 68`:** panggil `POST /status` dengan interval wajar hingga status final (`00` atau kode gagal).
5. **Simpan** `trxid`, `request_id`, `sn` (jika ada) untuk rekonsiliasi dan dukungan pelanggan.

Alur: [Direct Purchase without Inquiry](doc/transaksi-direct/flow-direct-purchase-without-inquiry.md) · [Direct Purchase with Inquiry](doc/transaksi-direct/flow-direct-purchase-with-inquiry.md) · [flow inquiry & purchase (ringkas)](doc/transaksi-direct/flow-inquiry-purchase.md) · [pulsa](doc/transaksi-direct/contoh-respons-pulsa.md) · [game](doc/game/README.md) · [skenario pengujian](doc/transaksi-direct/skenario-pengujian.md).

---

## Struktur repositori

```
.
├── README.md                 ← Pengantar repositori (Anda di sini)
├── mkdocs.yml                ← Navigasi situs (Material)
├── requirements-docs.txt
├── .gitignore
└── doc/
    ├── index.md              ← Beranda MkDocs
    ├── introduction-transaction-flow.md
    ├── 01-pengenalan.md
    ├── 02-persiapan-integrasi.md
    ├── appendix-deposit-ticket.md
    ├── prepaid/              ← Pulsa, data
    ├── game/                 ← Top-up non-zone, zona, voucher
    ├── ewallet/              ← Direct purchase + DANA inquiry
    ├── inquiry/
    │   ├── README.md
    │   ├── inquiry-post.md   ← POST /inquiry (kontrak umum)
    │   └── inquiry-pln.md    ← Contoh CPLN
    └── transaksi-direct/     ← Purchase, saldo, status, RC, klasifikasi game
```

---

## Lisensi & kontak

Hak cipta dan kebijakan distribusi dokumen mengikuti kebijakan **Indotech / pemilik API**. Untuk akses sandbox, whitelist IP, atau pertanyaan integrasi, hubungi **tim teknis Indotech** melalui kanal resmi yang diberikan kepada mitra.

---
