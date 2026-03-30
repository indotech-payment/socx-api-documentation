# Introduction & Transaction Flow

Bagian ini merangkum alur dasar integrasi sebelum masuk ke kategori produk.

## Direct Purchase without Inquiry

Alur **tanpa** pre-check inquiry — langsung [`POST /purchase`](transaksi-direct/pembelian-json-post.md). Diagram dan langkah lengkap: **[Direct Purchase without Inquiry](transaksi-direct/flow-direct-purchase-without-inquiry.md)** (acuan diagram mengikuti [klasifikasi produk game](transaksi-direct/klasifikasi-produk-game.md)).

## payment with inquiry

Alur **dengan** [`POST /inquiry`](inquiry/inquiry-post.md) dulu, lalu purchase. Diagram dan langkah lengkap: **[payment with inquiry](transaksi-direct/payment-with-inquiry.md)**.

## Referensi cepat

| Kebutuhan | Halaman |
|-----------|---------|
| Ringkasan folder direct purchase (tabel file) | [Transaksi — direct purchase](transaksi-direct/README.md) |
| Inquiry umum & katalog | [Inquiry & katalog](inquiry/README.md) |
| payment with inquiry (alur & diagram) | [payment with inquiry](transaksi-direct/payment-with-inquiry.md) |
