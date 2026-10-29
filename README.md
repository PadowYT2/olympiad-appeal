# Апелляция по олимпиаде

> [!NOTE]
> there's nothing useful in this repository likely for you, except for the people responsible for the olympiad I took

## Задание

Установите соответствие между доменами и сертификатами, которые можно для них использовать.

| Домены | Сертификаты                                                                                           |
| ------ | ----------------------------------------------------------------------------------------------------- |
| ???    | `C=RU, L=Moscow, O=Example LLC, CN=example.com; расширения: subjectAltName=DNS:auth.example.com`      |
| ???    | `C=RU, L=Moscow, O=Example LLC, CN=auth.example.com; расширения: subjectAltName=DNS:*.example.com`    |
| ???    | `C=RU, L=Moscow, O=Example LLC, CN=www.example.com; расширения: subjectAltName=DNS:*.www.example.com` |

Домены для выбора: `admin.www.example.com`, `www.example.com`, `auth.example.com`, `example.com`

### "Правильный" ответ

1. `example.com`, `auth.example.com`
2. `www.example.com`, `auth.example.com`
3. `www.example.com`, `admin.www.example.com`

### Мой ответ

1. `auth.example.com`
2. `www.example.com`, `auth.example.com`
3. `admin.www.example.com`

## Объяснение и тесты

FQDN указанный в `CN`, не является допустимым к сертификату. Он **должен** быть указан в `subjectAltName`.

### Подготовка и запуск

Нужны данные программы:

- Caddy
- openssl
- curl

Затем клонировать данный репозиторий (ну или разархивировать прикрепленный .zip) и перейти в него.

Сертификаты уже были созданы в папке `certificates`, но вы можете их удалить и сгенерировать заново по заданию
(уже написано в [README](certificates/README.md)).

Теперь запускаем Caddy через `caddy run` и пытаемся открыть сайт с каждым сертификатом, по ссылкам которые в задании.

```sh
# Первый сертификат @ порт 8441
curl -sS --resolve example.com:8441:127.0.0.1 --cacert certificates/1.pem https://example.com:8441/
curl -sS --resolve auth.example.com:8441:127.0.0.1 --cacert certificates/1.pem https://auth.example.com:8441/
curl -sS --resolve www.example.com:8441:127.0.0.1 --cacert certificates/1.pem https://www.example.com:8441/
curl -sS --resolve admin.www.example.com:8441:127.0.0.1 --cacert certificates/1.pem https://admin.www.example.com:8441/

# Второй сертификат @ порт 8442
curl -sS --resolve example.com:8442:127.0.0.1 --cacert certificates/2.pem https://example.com:8442/
curl -sS --resolve auth.example.com:8442:127.0.0.1 --cacert certificates/2.pem https://auth.example.com:8442/
curl -sS --resolve www.example.com:8442:127.0.0.1 --cacert certificates/2.pem https://www.example.com:8442/
curl -sS --resolve admin.www.example.com:8442:127.0.0.1 --cacert certificates/2.pem https://admin.www.example.com:8442/

# Третий сертификат @ порт 8443
curl -sS --resolve example.com:8443:127.0.0.1 --cacert certificates/3.pem https://example.com:8443/
curl -sS --resolve auth.example.com:8443:127.0.0.1 --cacert certificates/3.pem https://auth.example.com:8443/
curl -sS --resolve www.example.com:8443:127.0.0.1 --cacert certificates/3.pem https://www.example.com:8443/
curl -sS --resolve admin.www.example.com:8443:127.0.0.1 --cacert certificates/3.pem https://admin.www.example.com:8443/
```

И можно увидеть, что где ответ `ok` - правильный выбор, а другие варианты просто выдают ошибку (не правильный ответ).
(1 в 1 с моим ответом, который выше)
