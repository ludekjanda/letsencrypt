---
title: Часто поставлені питання
linkTitle: Часто поставлені питання (FAQ)
slug: faq
lastmod: 2024-06-26
menu:
  main:
    weight: 30
    parent: about
show_lastmod: 1
---

FAQ розділяється на такі розділи:

- [Загальні питання](#general)
- [Технічні питання](#technical)

# <a id="general">Загальні питання</a>

## Які сервіси пропонує Let's Encrypt?

Let's Encrypt - це глобальний центр сертифікації (ЦС). Ми дозволяємо людям та організаціям по всьому світу отримувати, поновлювати та управляти сертифікатами SSL/TLS. Наші сертифікати можуть використовуватися веб-сайтами для забезпечення безпечного з'єднання HTTPS.

Let's Encrypt пропонує сертифікати перевірки домену (DV). Ми не пропонуємо перевірку організації (OV) або розширену перевірку (EV) насамперед тому, що ми не можемо автоматизувати видачу для таких типів сертифікатів.

Щоб почати користуватися Let's Encrypt, відвідайте нашу сторінку [Починаємо](/getting-started).

## Яка вартість того, щоб мати змогу користуватися Let's Encrypt? Це дійсно безкоштовно?

Ми не стягуємо плату за наші сертифікати. Let's Encrypt - це некомерційна організація, наша місія полягає у створенні більш безпечної та з повагою до конфіденційності мережі шляхом сприяння для широкого впровадження протоколу HTTPS. Наші послуги безкоштовні та прості у використанні, тому кожен веб-сайт може використовувати HTTPS.

Нам потрібна підтримка від щедрих спонсорів, грантодавців та приватних осіб, щоб безкоштовно надавати наші послуги по всьому світу. Якщо ви зацікавлені у допомозі нам, будь ласка, [профінансуйте](/donate) або [станьте нашим спонсором](https://www.abetterinternet.org/sponsor).

У деяких випадках інтегратори (наприклад, провайдери хостингу) стягуватимуть номінальну плату, що відображає адміністративні та управлінські витрати, які вони несуть, щоб надавати сертифікати Let's Encrypt.

## Яку підтримку ви пропонуєте?

Керуємо Let's Encrypt невеликою командою і покладаємося на автоматизацію, щоб зменшити витрати. У такому разі ми не можемо запропонувати нашим підписникам пряму підтримку. Однак у нас є кілька чудових варіантів для підтримки:

1. У нас є дійсно корисна [ документація ](/docs).
2. У нас є дуже активні та корисні У нас є дуже активні та корисні [ форуми підтримки спільноти ](https://community.letsencrypt.org/). Члени нашої спільноти чудово відповідають на запитання, і на багато найпоширеніших питань уже отримано відповіді.

Ось [ відео, яке нам подобається ](https://www.youtube.com/watch?v=Xe1TZaElTAs) про силу великої підтримки спільноти.

## Вебсайт, що використовує Let's Encrypt, займається фішингом/шкідливим ПЗ/шахрайством/... що мені робити?

Ми рекомендуємо повідомляти про такі сайти безпечному перегляду Google та програмі Microsoft Smart Screen, які здатні більш ефективно захищати користувачів. Ось URL -адреси звітів:

- [https://safebrowsing.google.com/safebrowsing/report_badware/](https://safebrowsing.google.com/safebrowsing/report_badware/)
- [https://www.microsoft.com/en-us/wdsi/support/report-unsafe-site-guest](https://www.microsoft.com/en-us/wdsi/support/report-unsafe-site-guest)

Якщо ви хочете дізнатися більше про нашу політику та міркування, ви можете зробити це тут:

https://letsencrypt.org/2015/10/29/phishing-and-malware.html

# <a id="technical">Технічні питання</a>

## Чи надійні сертифікати від Let's Encrypt для мого браузера?

Так, надійні для більшості браузерів та операційних систем. Докладніше дивись у [ списку сумісності ](/docs/cert-compat).

## Чи видає Let's Encrypt сертифікати на щось, крім SSL/TLS для веб-сайтів?

Сертифікати Let's Encrypt - це стандартні сертифікати перевірки домену, тому ви можете використовувати їх для будь-якого сервера, який використовує доменне ім’я, наприклад веб-сервери, поштові сервери, FTP-сервери та багато іншого.

Для того, щоб зашифрувати електронну пошту та код, потрібен інший тип сертифікату, який Let's Encrypt не видає.

## Чи можливо у Let's Encrypt генерувати або зберігати приватні ключі моїх сертифікатів на серверах Let's Encrypt?

Ні. Ніколи.

Приватний ключ завжди формується та управляється на ваших власних серверах, а не центром сертифікації Let's Encrypt.

## Який термін служби сертифікатів Let's Encrypt? Як довго вони дійсні?

Наші сертифікати є дійсними протягом 90 днів. Про те, чому можна прочитати [ тут ](/2015/11/09/why-90-days.html).

Це неможливо відрегулювати, немає винятків. Ми рекомендуємо автоматично поновлювати ваші сертифікати кожні 60 днів.

## Чи буде Let's Encrypt видавати сертифікати перевірки організації (OV) або розширеної перевірки (EV)?

Ми не плануємо видавати сертифікати OV або EV.

## Чи можу я отримати сертифікат на кілька доменних імен (сертифікати SAN або сертифікати UCC)?

Так, один і той же сертифікат може містити кілька різних назв за допомогою механізму суб’єктної альтернативної назви (SAN).

## Чи видає Let's Encrypt сертифікати із відкритим ключем?

Так. Видавання за допомогою ACMEv2 здійснюється через [виклик DNS-01](/docs/challenge-types/#dns-01-challenge). Додаткову технічну інформацію дивись у [ цій публікації ](https://community.letsencrypt.org/t/acme-v2-production-environment-wildcards/55578).

## Чи існує клієнт Let's Encrypt (ACME) для моєї операційної системи?

Доступна велика кількість [ клієнтів ACME ](/docs/client-options). Швидше за все, є шанси, що щось добре працює у вашій операційній системі. Ми рекомендуємо починати з [ Certbot ](https://certbot.eff.org/).

## Чи можна використовувати приватний ключ, який вже існує або запит на підпис сертифіката (CSR)?

Так, але не всі клієнти можуть підтримувати цю функцію. Працює [ Certbot ](https://certbot.eff.org/).

## Я запросив сертифікат, і тепер мій домен отримує багато трафіку! Чому так відбувається?

Це нормально й очікувано. Під час [процесу видачі сертифіката](/how-it-works), Let's Encrypt перевірить контроль над вашим доменом з [кількох мережевих перспектив](/2020/02/19/multi-perspective-validation). Після успішної перевірки, ваш сертифікат буде внесено до численних [Журналів прозорості сертифікатів (CT)](/docs/ct-logs). Детальніше про те, чому це необхідно, дивіться [тут](https://certificate.transparency.dev/howctworks/#pki). Незабаром після того, як сертифікат буде надіслано до CT, автоматизовані боти CT зможуть виявити ваш домен, спробувати отримати до нього доступ і генерувати подальший трафік у журналах вашого вебсервера.

## Які IP -адреси використовує Let's Encrypt для перевірки мого веб-сервера?

Ми не публікуємо список IP -адрес, які використовуємо для перевірки, і ці IP - адреси можемо змінити в будь-який час. Зверніть увагу, що тепер ми [перевіряємо з декількох IP-адрес](/2020/02/19/multi-perspective-validation.html).

## Я успішно поновив сертифікат, але цього разу перевірки не відбулося - як це можливо?

Після того, як ви успішно вирішите завдання для домену, отримана авторизація буде кешована для використання вашого облікового запису пізніше. Кешовані авторизації тривають 30 днів з моменту перевірки. Якщо у запитаному вами сертифікаті всі необхідні авторизації кешуються, перевірка не повториться, поки не закінчиться відповідна авторизація в кеші.

## Чому мій клієнт Let's Encrypt (ACME) повинен запускатися у випадковий час?

Ми просимо клієнтів [ACME виконувати рутинне оновлення у випадковий час](https://letsencrypt.org/docs/integration-guide/#when-to-renew), щоб уникнути сплесків трафіку у визначений час доби, наприклад, рівно опівночі за Гринвічем або в першу секунду кожної години чи хвилини. Якщо сервіс занадто завантажений, клієнтам буде запропоновано [спробувати пізніше](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/503), тому рандомізація часу поновлення може допомогти уникнути непотрібних повторних спроб.

## Де можна більше дізнатися про TLS/SSL та PKI загалом?

Дослідник з безпеки та практик Іван Ристіч, опублікував посібник з конфігурації, який надає корисну інформацію про те, що вам слід вирішити перед <a href="https://www.feistyduck.com/library/bulletproof-tls-guide/online/" target="_blank" rel="noopener noreferer">налаштуванням конфігурації TLS</a>.

Для ширшого розуміння та більшої кількості подробиць ми радимо <a href="https://www.feistyduck.com/books/bulletproof-tls-and-pki/" target="_blank" rel="noopener noreferer">Bulletproof TLS і PKI</a>, також написаний Рістічем.
