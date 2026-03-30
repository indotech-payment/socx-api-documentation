# DANA (Inquiry)

Satu halaman untuk inquiry DANA: **denom tetap** dan **denom bebas**.

## Kontrak HTTP

- Endpoint: `POST /inquiry`
- Header: `Authorization: Bearer <JWT>`
- Header: `Content-Type: application/json`
- Referensi umum: [Inquiry POST (JSON)](../inquiry/inquiry-post.md)

## 1) Denom tetap

`code` contoh: `DANA`

### Request

```json
{
  "code": "DANA",
  "idpel": "08996647676#1000",
  "request_id": "26032600000"
}
```

### Respons sukses

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

## 2) Denom bebas

`code` contoh: `CDANA` / `DANA_BEBAS` (sesuai katalog).

### Request

```json
{
  "code": "CDANA",
  "idpel": "082218965846#5000",
  "request_id": "26032972396000"
}
```

### Respons sukses

```json
{
  "code": "DANA_BEBAS",
  "idpel": "082218965846#5000",
  "request_id": "26032972396000",
  "product_name": "DANA Denom Bebas",
  "client_name": "DNID SANXX SUSXXXXXXX",
  "info": null,
  "rc": "00",
  "msg": "SUKSES",
  "jumlah_tagihan": "1",
  "denda": "",
  "tagihan": "5000",
  "admin": "0",
  "total": "5000",
  "balance": 4412869
}
```
