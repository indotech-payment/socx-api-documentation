# DANA (Inquiry) — Denom tetap

Contoh inquiry DANA dengan nilai nominal pada parameter `idpel`:

```bash
curl -L -X POST 'http://indotechapi.socx.app/reseller/api/v1/inquiry' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer xxxx' \
  -d '{"code":"DANA","idpel":"08996647676#1000","request_id":"26032600000"}'
```

Contoh respons:

```json
{
  "code": "DANA",
  "idpel": "08996647676#1000",
  "request_id": "26032600000",
  "product_name": "DANA",
  "client_name": "DNID aXX danX",
  "info": null,
  "rc": "00",
  "msg": "SUKSES",
  "jumlah_tagihan": "1",
  "denda": "",
  "tagihan": "1000",
  "admin": "60",
  "total": "1060",
  "balance": 29986574717
}
```

Lihat juga: [Denom Bebas](dana-inquiry-denom-bebas.md) · [Ringkasan DANA](dana-inquiry.md)
