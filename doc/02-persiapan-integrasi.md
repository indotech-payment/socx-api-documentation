# Persiapan integrasi

Checklist sebelum mulai hit API production.

## 1. IP statis & whitelist

- Pastikan server integrasi memakai **IP statis** (atau rentang yang disepakati).
- Kirim IP ke tim SOCX untuk **whitelist** di sisi API.
- Tanpa whitelist, request dapat ditolak di layer jaringan atau aplikasi.

## 2. Token (JWT)

1. Login ke portal reseller SOCX.
2. Buka **Settings**.
3. Salin token dan simpan sebagai rahasia .
4. Header: `Authorization: Bearer <token>`.


## 3. Konvensi `request_id`

- Harus **unik per percobaan transaksi baru** dari sisi Anda.
- Jika Anda mengirim ulang `request_id` yang **sudah pernah diproses** di server SOCX, API mengembalikan **respons yang sama** dengan transaksi tersebut (idempotensi).

Disarankan: prefix lingkungan + timestamp + random, contoh `STG-20250322-abc12`.

## 4. HTTPS

Selalu gunakan **HTTPS** untuk semua panggilan API.

