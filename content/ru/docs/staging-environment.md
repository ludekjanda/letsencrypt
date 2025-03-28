---
title: Тестовое окружение
slug: staging-environment
date: 2018-01-05
lastmod: 2025-01-22
show_lastmod: 1
---


Мы настоятельно рекомендуем производить проверку в тестовом окружении, перед тем как использовать рабочий сервер. Это позволит обнаружить проблему еще до выпуска доверенных сертификатов и уменьшит шанс столкнуться с ограничениями по лимиту.

URL-адрес ACME нашего [тестового окружения ACME v2](https://community.letsencrypt.org/t/staging-endpoint-for-acme-v2/49605):

`https://acme-staging-v02.api.letsencrypt.org/directory`

Если вы используете Certbot, тестовое окружение можно запустить с помощью флага `--test-cert`. В случае других ACME-клиентов ищите информацию по использованию нашего тестового окружения в их инструкциях. Пожалуйста, обратите внимание, что тестовое окружение v2 требует v2-совместимого ACME-клиента.

# Лимиты

В тестовом окружении используются те же лимиты, что и для [рабочих серверов](/docs/rate-limits), со следующими исключениями:

* **Сертификаты для зарегистрированного домена** &mdash; лимит 30 000 в неделю.
* **Дубликат сертификата** &mdash; лимит 30 000 в неделю.
* **Неудачная проверка** &mdash; лимит 60 в час.
* **Аккаунты на IP-адрес** &mdash; лимит 50 аккаунтов за 3 часа на один IP.
* Для ACME v2 лимит **Новых заказов** — 1500 новых заказов за 3 часа на аккаунт.

# Иерархия тестовых сертификатов

В тестовом окружении имеется своя иерархия сертификатов, [повторяющая рабочую](/certificates).

## Промежуточные сертификаты

В тестовом окружении есть два промежуточных сертификата: промежуточный RSA [(STAGING) Artificial Apricot R3"](/certs/staging/letsencrypt-stg-int-r3.pem) и промежуточный ECDSA [(STAGING) Ersatz Edamame E1"](/certs/staging/letsencrypt-stg-int-e1.pem).

Выпуск сертификатов ECDSA был [включен в тестовом окружении](https://community. letsencrypt. org/t/ecdsa-issuance-available-in-staging-march-24/147839) 24 марта 2021; все запросы на выгрузку сертификатов ECDSA с ключами ECDSA подписаны "(STAGING) Ersatz Edamame E1" и используют иерархию ECDSA. Аналогично, все запросы на получение сертификатов с ключами RSA подписываются "(STAGING) Artificial Apricot R3" и используют иерархию RSA. Не существует способа получения подписанного RSA-сертификата для ключа ECDSA и наоборот; тип полученного сертификата зависит от типа ключа, который вы создали локально.

## Корневые сертификаты

Тестовое окружение имеет два активных корневых сертификата, **которые отсутствуют** в доверенном хранилище/клиенте: "(STAGING) Pretend Pear X1" и "(STAGING) Bogus Broccoli X2". Если вы хотите изменить только тестовый клиент, который доверяет тестовой среде для целей тестирования, вы можете это сделать, добавив ["(STAGING) Pretend Pear X1"](/certs/staging/letsencrypt-stg-root-x1.pem) и/или ["(STAGING) Bogus Broccoli X2"](/certs/staging/letsencrypt-stg-root-x2.pem) сертификат в ваше тестовое доверенное хранилище. Вы можете найти все наши тестовые сертификаты [здесь](/static/certs/staging).  Важно: Не добавляйте тестовый корневой или промежуточный сертификат в доверенное хранилище, которое вы используете для обычного серфинга и другой деятельности в сети, так как они не прошли аудит и не соответствуют стандартам наших рабочих корневых сертификатов, потому небезопасны для использования где-либо еще, кроме тестирования.

# Прозрачность сертификата

Тестовое окружение отправляет предварительные сертификаты в Let's Encrypt [Sapling](/docs/ct-logs) и Google [testtube](http://www.certificate-transparency.org/known-logs#TOC-Test-Logs) журналы тестирования CT и включает возвращенные SCT в выпущенные сертификаты.

# Непрерывная интеграция (CI)/тестирование разработки

Лимиты тестового окружения достаточны для проведения тестирования, но не подходят для интеграции в среды разработки или непрерывной интеграции (CI). Запросы к внешним серверам снижают стабильность окружения. Кроме того, тестовое окружение не может "подделать" результаты DNS или HTTP-проверок, что усложняет проведение тестирования

В дополнение к тестовому окружению, Let's Encrypt предлагает ACME-сервер для окружения разработки и CI под названием [Pebble](https://github.com/letsencrypt/pebble). Запуск Pebble на машине разработчика или CI-сервере выполняется [быстро и просто](https://github.com/letsencrypt/pebble#docker).
