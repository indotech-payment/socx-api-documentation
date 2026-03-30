# Introduction & Transaction Flow

Bagian ini merangkum alur dasar integrasi sebelum masuk ke kategori produk.

## Direct Purchase without Inquiry

Alur **tanpa** pre-check inquiry — langsung [`POST /purchase`](transaksi-direct/pembelian-json-post.md). Diagram dan langkah lengkap: **[Direct Purchase without Inquiry](transaksi-direct/flow-direct-purchase-without-inquiry.md)** (acuan diagram mengikuti [klasifikasi produk game](transaksi-direct/klasifikasi-produk-game.md)).

## Payment — with inquiry

Alur **dengan** [`POST /inquiry`](inquiry/inquiry-post.md) dulu, lalu purchase. Diagram dan langkah lengkap: **[Payment — with inquiry](transaksi-direct/payment-with-inquiry.md)**.

## Referensi cepat

| Kebutuhan | Halaman |
|-----------|---------|
| Ringkasan folder direct purchase (tabel file) | [Transaksi — direct purchase](transaksi-direct/README.md) |
| Inquiry umum & katalog | [Inquiry & katalog](inquiry/README.md) |
| Diagram inquiry → purchase (game, ringkas) | [Flow inquiry & purchase (umum)](transaksi-direct/flow-inquiry-purchase.md) |
