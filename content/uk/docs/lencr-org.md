---
title: lencr.org
slug: lencr.org
top_graphic: 1
date: 2020-12-04
lastmod: 2020-12-04
show_lastmod: 1
---


# Що таке lencr.org?

`lencr.org` - це домен, що належить Let's Encrypt. Ми використовуємо його для розміщення OCSP, CRLs, та видачі сертифікатів: усі URS-адреси, які відображаються в сертифікатах.

Ми звикли використовувати довші URL-адреси як `http://ocsp.int-x3.letsencrypt.org/`. Проте, коли ми видавали наші [нові кореневі та проміжні сертифікати][1], ми хотіли скоротити їх наскільки це можливо. Кожне з'єднання HTTPS в Інтернеті (мільярди на день) має надіслати копію сертифіката, тому кожен байт має значення. Ми вибрали `lencr.org` через схожість з нашою назвою: **L**et's **ENCR**ypt. Ми вимовляємо це так само, як вигадану область [Ланкр][] у романах Террі Пратчетта _Світ дисків_.

[1]: https://letsencrypt.org/2020/09/17/new-root-and-intermediates.html
[Ланкр]: https://discworld.fandom.com/wiki/Lancre