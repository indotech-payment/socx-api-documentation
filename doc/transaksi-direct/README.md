# Transaksi — Direct purchase

Bagian ini fokus pada alur **pembelian langsung** (top-up / voucher). Untuk **diagram alur** tingkat dokumen: **[Direct Purchase without Inquiry](./flow-direct-purchase-without-inquiry.md)** (tanpa `POST /inquiry`) dan **[payment with inquiry](./payment-with-inquiry.md)** (inquiry dulu, lalu purchase).

## Alur disarankan

1. **Cek saldo** (opsional tapi dianjurkan sebelum transaksi besar): [`GET /saldo`](./cek-saldo.md)
2. **Purchase** — pilih satu jalur:
   - [`POST /purchase` pulsa/data](./pembelian-pulsa-data.md)
   - [`POST /purchase` game](./pembelian-game.md)
   - [`POST /purchase` ewallet](./pembelian-ewallet.md)
   - [`/http/purchase`](./pembelian-http.md)
3. Jika `rc = 68` (**pending**): polling [`POST /status`](./cek-status.md) sampai final, atau tunggu **callback** (kontrak callback perlu dikonfirmasi — lihat catatan di [contoh pulsa](./contoh-respons-pulsa.md)).

## Isi folder

| File | Isi |
|------|-----|
| [cek-saldo.md](./cek-saldo.md) | GET saldo |
| [pembelian-pulsa-data.md](./pembelian-pulsa-data.md) | Request/response purchase pulsa & data |
| [pembelian-game.md](./pembelian-game.md) | Request/response purchase game |
| [pembelian-ewallet.md](./pembelian-ewallet.md) | Request/response purchase ewallet |
| [pembelian-http.md](./pembelian-http.md) | GET/POST http purchase |
| [cek-status.md](./cek-status.md) | POST status |
| [kode-respons.md](./kode-respons.md) | Tabel RC |
| [contoh-respons-pulsa.md](./contoh-respons-pulsa.md) | Contoh lengkap pulsa |
| [flow-direct-purchase-without-inquiry.md](./flow-direct-purchase-without-inquiry.md) | Alur & diagram direct purchase **tanpa** inquiry |
| [payment-with-inquiry.md](./payment-with-inquiry.md) | payment with inquiry — alur, diagram, referensi produk |
| [klasifikasi-produk-game.md](./klasifikasi-produk-game.md) | Klasifikasi + contoh request/response game; mapping `msisdn` |
| [skenario-pengujian.md](./skenario-pengujian.md) | Skenario QA |

Deposit tiket (`/deposit_ticket`) ada di spesifikasi sumber tetapi di luar fokus **direct purchase**; dapat ditambahkan halaman terpisah jika dibutuhkan.

