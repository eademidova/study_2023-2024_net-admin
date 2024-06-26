---
## Front matter
title: "Лабораторная работа № 8"
subtitle: "Настройка сетевых сервисов. DHCP"
author: "Демидова Екатерина Алексеевна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: false # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Приобретение практических навыков по настройке динамического распределения IP-адресов посредством протокола DHCP (Dynamic Host Configuration Protocol) в локальной сети.

# Задание

1. Добавить DNS-записи для домена donskaya.rudn.ru на сервер dns.
2. Настроить DHCP-сервис на маршрутизаторе.
3. Заменить в конфигурации оконечных устройствах статическое распределение адресов на динамическое.
4. При выполнении работы необходимо учитывать соглашение об именовании.

# Выполнение лабораторной работы

Откроем проект прошлой лабораторной работы(рис. [-@fig:001]).

![Схема сети без учёта физических параметров сети в логической рабочей области Packet Tracer](image/1.png){#fig:001 width=90%}

В логическую рабочую область проекта добавьте сервер dns и подключим его к коммутатору msk-donskaya-eademidova-sw-3 через порт Fa0/2. В конфигурации сервера укажите в качестве адреса шлюза 10.128.0.1, а в качестве адреса самого сервера — 10.128.0.5 с соответствующей маской 255.255.255.0.(рис. [-@fig:002]).

![Логическая схема локальной сети с добавленным DNS-сервером](image/2.png){#fig:002 width=90%}

Активируем порт,к которому подключен DNS-сервер, на коммутаторе с помощью команд:

```
msk-donskaya-eademidova-sw-3>en
msk-donskaya-eademidova-sw-3#conf t
msk-donskaya-eademidova-sw-3(config)#interface f0/2
msk-donskaya-eademidova-sw-3(config-if)#switchport mode access 
msk-donskaya-eademidova-sw-3(config-if)#switchport access vlan 3
msk-donskaya-eademidova-sw-3(config-if)#exit
```

Настроим сервис DNS(рис. [-@fig:003]):
- в конфигурации сервера выберите службу DNS, активируйте её (выбрав
флаг On);
- в поле Type в качестве типа записи DNS выберите записи типа A (A Record);
- в поле Name укажите доменное имя, по которому можно обратиться,
например, к web-серверу — www.donskaya.rudn.ru, затем укажите его
IP-адрес в соответствующем поле 10.128.0.2;
- нажав на кнопку Add , добавьте DNS-запись на сервер;
- аналогичным образом добавьте DNS-записи для серверов mail, file, dns согласно распределению адресов из таблицы  из лабораторной работы 3;
- сохраните конфигурацию сервера.

(рис. [-@fig:003]).

![Окно настройки сервиса DNS](image/3.png){#fig:003 width=90%}

Настроим DHCP-сервис на маршрутизаторе(рис. [-@fig:004]), используя приведённые ниже команды для каждой выделенной сети: укажем IP-адрес DNS-сервера; затем перейдем к настройке DHCP; зададим название конфигурируемому диапазону адресов (пулу адресов), укажем адрес сети, а также адреса шлюза и DNS-сервера; зададим пулы адресов, исключаемых из динамического распределениятабл. [-@tbl:plan].

![Настройка DHCP-сервиса на маршрутизаторе](image/4.png){#fig:004 width=90%}

:Регламент выделения ip-адресов (для сети класса C) {#tbl:iplan}

| IP-адреса | Назначение           |
|-----------|----------------------|
| 1         | Шлюз                 |
| 2-19      | Сетевое оборудование |
| 20-29     | Серверы              |
| 30-199    | Компьютеры, DHCP     |
| 200-219   | Компьютеры, Static   |
| 220-229   | Принтеры             |
| 230-254   | Резерв               |

Просмотрим информацию о пулах DHCP и о привязках выданных адресов(рис. [-@fig:005]).

![Просмотр информации о DHCP пулах и выданных адресах](image/5.png){#fig:005 width=90%}

Можно увидеть информацию об IP-адресах пулов, шлюзе и диапозоне. Пока что никаие адреса не были выданы, поэтому в информации о привязке ничего нет.


На оконечных устройствах замените в настройках статическое распределение адресов на динамическое. Можем увидеть, что выделяется c первого адреса из доступного диапазона по-очереди(рис. [-@fig:006]).

![IP-адрес выделенный DHCP](image/6.png){#fig:006 width=90%}

Проверим доступность устройств из разных подсетей(рис. [-@fig:007]).

![Проверка доступности устройств из разных подсетей](image/7.png){#fig:007 width=90%}

В режиме симуляции изучим, каким образом происходит запрос адреса по протоколу DHCP (рис. [-@fig:008], [-@fig:009]).

![DHCP запрос на выделение адреса](image/8.png){#fig:008 width=90%}

![DHCP ответ с выделенным адресом](image/9.png){#fig:009 width=90%}

Мы отправили запрос на выделение адреса для устройства donskaya-dk-1. Сначала DHCP-пакет рассылается всем устройствам сети и принимается маршрутизатором. В заголовках DNCP при этом указан только MAC-адрес устройства, которому нужен адрес(рис. [-@fig:010]).

![DHCP запрос на выделение адреса. Заголовки пакета](image/10.png){#fig:010 width=90%}

Затем маршрутизатор выделяет адрес нужному MAC-адресу на основе информации об уже занятях в этой подсети адресах. Он отпрвляет ответ устройству о том, какой именно адрес выделен. Теперь в заголовках указан адрес шлюза подсети, адрес устройства, а также информация об адресе dns-сервера(рис. [-@fig:011]).

![DHCP ответ с выделенным адресом. Заголовки пакета](image/11.png){#fig:011 width=90%}

## Контрольные вопросы

1. За что отвечает протокол DHCP?
2. Какие типы DHCP-сообщений передаются по сети?
3. Какие параметры могут быть переданы в сообщениях DHCP?
4. Что такое DNS?
5. Какие типы записи описания ресурсов есть в DNS и для чего они используются?

1. Протокол DHCP отвечает за динамическое назначение IP-адресов и других сетевых параметров устройствам в сети.
2. Типы DHCP-сообщений: DHCP Discover, DHCP Offer, DHCP Request, DHCP Acknowledge.
3. Параметры DHCP могут включать IP-адреса, шлюзы, DNS-серверы, временные интервалы аренды и другие настройки сети.
4. DNS (Domain Name System) - служит для преобразования доменных имен в IP-адреса и обратно.
5. Типы записей DNS: A (IPv4-адрес), AAAA (IPv6-адрес), CNAME (каноническое имя), MX (почтовый сервер), TXT (текстовая информация) и другие.

# Выводы

В результате выполнения лабораторной работы получили навыки по настройке динамического распределения IP-адресов посредством протокола DHCP в локальной сети.
