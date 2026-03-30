# Dokumentasi API SOCX (Reseller H2H)

Dokumen ini untuk integrasi **Host-to-Host (H2H)** reseller ke platform SOCX. Isi disusun bertahap: **pengenalan → persiapan integrasi → transaksi → kode respons → contoh → pengujian**.

Gunakan **menu kiri** untuk navigasi (situs ini dihasilkan dengan [MkDocs Material](https://squidfunk.github.io/mkdocs-material/)).

## Isi dokumentasi

| Bagian | Keterangan |
|--------|------------|
| [Pengenalan](01-pengenalan.md) | Gambaran umum, base URL, autentikasi |
| [Persiapan integrasi](02-persiapan-integrasi.md) | IP statis, whitelist, token, format `request_id` |
| **Transaksi direct purchase** | |
| → [Cek saldo](transaksi-direct/cek-saldo.md) | `GET /saldo` |
| → [PREPAID — Pulsa & Data](transaksi-direct/pembelian-pulsa-data.md) | `POST /purchase` prepaid: request & respons |
| → [Top Up & Voucher — game (POST)](game/topup-voucher.md) | `POST /purchase` game: request, klasifikasi, respons |
| → [Ewallet Direct Purchase](transaksi-direct/pembelian-ewallet.md) | `POST /purchase` e-wallet (request & respons) |
| → [Cek status](transaksi-direct/cek-status.md) | `POST /status` |
| → [Kode respons (RC)](transaksi-direct/kode-respons.md) | Tabel RC |
| → [Skenario pengujian](transaksi-direct/skenario-pengujian.md) | Checklist QA integrasi |
| [Inquiry](inquiry/README.md) | `POST /inquiry` — contoh PLN prabayar (`CPLN`) |
| [Lampiran — deposit tiket](appendix-deposit-ticket.md) | Di luar direct purchase; dari spesifikasi sumber |

## Status dokumen

- **Siap dipakai untuk integrasi:** direct purchase (JSON/HTTP), cek saldo, cek status, tabel RC — sesuai sumber internal `socx.md`.
- **Perlu review tim SOCX / API:** callback setelah `rc = 68` (pending), verifikasi webhook/XML `topUpReport`, URL & kontrak **inquiry** / daftar harga, finalisasi parameter game per `code` di tabel klasifikasi.


