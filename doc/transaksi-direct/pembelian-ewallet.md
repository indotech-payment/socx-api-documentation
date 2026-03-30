# Pembelian — Ewallet (JSON POST)

Request dan respons khusus kategori ewallet via `POST /purchase`.

## Request (contoh)

```json
{
  "code": "CDANA5",
  "msisdn": "085776810414",
  "request_id": "26032500001001"
}
```

## Response sukses (contoh)

```json
{
  "data": {
    "ref_id": "qi46fh0jwcsp58268",
    "status": "1",
    "code": "CDANA5",
    "hp": "085776810414",
    "price": "4545",
    "message": "Success",
    "balance": "7658690",
    "tr_id": "909649",
    "rc": "00",
    "sn": "TopUp DANA-FEBXXX VIAXX HERXXXXX/4500/085776810414/Reff:2025112510121481030100166579732735641"
  }
}
```

## Catatan

- Endpoint: `{base_url}/purchase`
- Untuk flow inquiry DANA, lihat [Ringkasan DANA](../ewallet/dana-inquiry.md).
- Untuk daftar `rc` gagal, lihat [kode respons (RC)](./kode-respons.md).
