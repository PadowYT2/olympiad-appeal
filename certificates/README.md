1. Сертификат: `C=RU, L=Moscow, O=Example LLC, CN=example.com; расширения: subjectAltName=DNS:auth.example.com`

Команда для сгенерирования:

```sh
openssl req -x509 -newkey ed25519 -noenc -keyout 1.key -out 1.pem -subj "/C=RU/L=Moscow/O=Example LLC/CN=example.com" -addext "subjectAltName=DNS:auth.example.com"
```

2. Сертификат: `C=RU, L=Moscow, O=Example LLC, CN=auth.example.com; расширения: subjectAltName=DNS:*.example.com`

Команда для сгенерирования:

```sh
openssl req -x509 -newkey ed25519 -noenc -keyout 2.key -out 2.pem -subj "/C=RU/L=Moscow/O=Example LLC/CN=auth.example.com" -addext "subjectAltName=DNS:*.example.com"
```

3. Сертификат: `C=RU, L=Moscow, O=Example LLC, CN=www.example.com; расширения: subjectAltName=DNS:*.www.example.com`

Команда для сгенерирования:

```sh
openssl req -x509 -newkey ed25519 -noenc -keyout 3.key -out 3.pem -subj "/C=RU/L=Moscow/O=Example LLC/CN=www.example.com" -addext "subjectAltName=DNS:*.www.example.com"
```
