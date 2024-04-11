---
## Front matter
title: "Лабораторная работа № 9"
subtitle: "Использование протокола STP. Агрегирование каналов"
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

Изучение возможностей протокола STP и его модификаций по обеспечению отказоустойчивости сети, агрегированию интерфейсов и перераспределению нагрузки между ними.

# Задание

1. Сформируйте резервное соединение между коммутаторами msk-donskaya-sw-1 и msk-donskaya-sw-3.
2. Настройте балансировку нагрузки между резервными соединениями.
3. Настройте режим Portfast на тех интерфейсах коммутаторов, к которым подключены серверы.
4. Изучите отказоустойчивость резервного соединения.
5. Сформируйте и настройте агрегированное соединение интерфейсов Fa0/20 -- Fa0/23 между коммутаторами msk-donskaya-sw-1 и msk-donskaya-sw-4.

# Выполнение лабораторной работы

Откроем проект прошлой лабораторной работы(рис. [-@fig:001]).

![Схема сети в логической рабочей области Packet Tracer](image/1.png){#fig:001 width=90%}

Сформируем резервное соединение между коммутаторами msk-donskaya-eademidov-sw-1 и msk-donskaya-eademidov-sw-3 (рис. [-@fig:002]). Для этого:
- заменим соединение между коммутаторами msk-donskaya-sw-1 (Gig0/2) и msk-donskaya-sw-4 (Gig0/1) на соединение между коммутаторами msk-donskaya-eademidov-sw-1 (Gig0/2) и msk-donskaya-eademidov-sw-3 (Gig0/2);
- сделаем порт на интерфейсе Gig0/2 коммутатора msk-donskaya-eademidov-sw-3 транковым:
```
msk-donskaya-eademidova-sw-3(config)# int g0/2
msk-donskaya-eademidova-sw-3(config-if)# switchport mode trunk
```
- соединение между коммутаторами msk-donskaya-eademidov-sw-1 и msk-donskaya-eademidov-sw-4 сделаем через интерфейсы Fa0/23, и также активируем их в транковом режиме:

```
msk-donskaya-eademidova-sw-1(config)# int f0/23
msk-donskaya-eademidova-sw-1(config-if)# switchport mode trunk
```

```
msk-donskaya-eademidova-sw-4(config)# int f0/23
msk-donskaya-eademidova-sw-4(config-if)# switchport mode trunk
```

![Логическая схема локальной сети с резервным соединением](image/2.png){#fig:002 width=90%}

С оконечного устройства dk-donskaya-1 пропингуем серверы mail и web(рис. [-@fig:003]).

![Проверка доступности устройств с помощью команды `ping`](image/3.png){#fig:003 width=90%}

Пакеты успешно отправлены и получены.

В режиме симуляции проследим движение пакетов ICMP. Можно увидеть, что движение пакетов происходит через коммутатор msk-donskaya-eademidova-sw-2(рис. [-@fig:004]).

![Проверка доступности устройств в режиме симуляции](image/4.png){#fig:004 width=90%}

На коммутаторе msk-pavlovskaya-eademidova-sw-1 посмотрим состояние протокола STP
для vlan 3. В результате выведена следующая информация, связанная с протоколом STP(рис. [-@fig:005]):

![Просмотр информации о STP для vlan 3 на msk-pavlovskaya-eademidova-sw-1](image/5.png){#fig:005 width=90%}

В качестве корневого коммутатора STP настроим коммутатор msk-donskaya-eademidova-sw-1(рис. [-@fig:006]).

![Просмотр информации о STP для vlan 3 на msk-donskaya-eademidova-sw-1](image/6.png){#fig:006 width=90%}

Используя режим симуляции, убедимся, что пакеты ICMP пойдут от хоста dk-donskaya-1 до mail через коммутаторы msk-donskaya-eademidova-sw-1 и msk-donskaya-eademidova-sw-3, а от хоста dk-donskaya-1 до web через коммутаторы msk-donskaya-eademidova-sw-1 и msk-donskaya-eademidova-sw-2(рис. [-@fig:007], [-@fig:008]).

![Проверка пути от хоста dk-donskaya-1 до mail](image/7.png){#fig:007 width=90%}

![Проверка пути от хоста dk-donskaya-1 до web](image/8.png){#fig:008 width=90%}

Настроим режим Portfast на тех интерфейсах коммутаторов, к которым подключены серверы, чтобы они при подключении не использовали лишние ресурсы(рис. [-@fig:009], [-@fig:010]).

![Настройка режима Portfast на msk-donskaya-eademidova-sw-2](image/9.png){#fig:009 width=90%}

![Настройка режима Portfast на msk-donskaya-eademidova-sw-3](image/10.png){#fig:010 width=90%}

Изучим отказоустойчивость протокола STP и время восстановления соединения при переключении на резервное соединение. Для этого используем команду `ping -n 1000 mail.donskaya.rudn.ru` на хосте dk-donskaya-1, а разрыв соединения обеспечим переводом соответствующего интерфейса коммутатора в состояние shutdown(рис. [-@fig:011]).

![Изучение отказоустойчивости протокола STP и время восстановления соединения](image/11.png){#fig:011 width=90%}

На восстановление требуется время равное пяти пинга.

Переключиим коммутаторы в режим работы по протоколу Rapid PVST+:
```
msk-donskaya-eademidova-sw-1( config )#spanning-tree mode rapid-pvst
msk-donskaya-eademidova-sw-2( config )#spanning-tree mode rapid-pvst
msk-donskaya-eademidova-sw-3( config )#spanning-tree mode rapid-pvst
msk-donskaya-eademidova-sw-4( config )#spanning-tree mode rapid-pvst
msk-pavlovskaya-eademidova-sw-1( config )#spanning-tree mode rapid-pvst
```
Изучим отказоустойчивость протокола Rapid PVST+ и время восстановления соединения при переключении на резервное соединение(рис. [-@fig:012]).

![Изучение отказоустойчивость протокола Rapid PVST+ и время восстановления соединения](image/12.png){#fig:012 width=90%}

Теперь на восстановление соединения требуется время всего одного пинга.

Сформируем агрегированное соединение интерфейсов Fa0/20 - Fa0/23 между коммутаторами msk-donskaya-eademidova-sw-1 и msk-donskaya-eademidova-sw-4(рис. [-@fig:013]).

![Логическая схема локальной сети с агрегированным соединением](image/13.png){#fig:013 width=90%}

Настроим агрегирование каналов. Сначала отключим на обоих коммутаторах транковый интерфейс Fa0/23. Затем задаем новый интерфейс, объединяющий диапазон адресов Fa0/20 - Fa0/23, и настраиваем на нём статическую агрегацию(рис. [-@fig:014], [-@fig:015]).

![Настройка агрегирования каналов на msk-donskaya-eademidova-sw-1](image/15.png){#fig:014 width=90%}

![Настройка агрегирования каналов на msk-donskaya-eademidova-sw-1](image/14.png){#fig:015 width=90%}


## Контрольные вопросы

1. Какую информацию можно получить, воспользовавшись командой определения состояния протокола STP для VLAN (на корневом и не на корневом устройстве)? Приведите примеры вывода подобной информации на устройствах.

На корневом устройстве можно увидеть обозначение, что оно корневое, а также MAC-адрес корневного устройства и отправителя(в этом случае они совпадают), время жизни сообщения и интервал, через который посылаются пакеты. В случае же не корневного устройства будет также указано расстояние до корневного устройства, и MAC-адрес отправителя будет соответствовать рассматриваемому устройству.

Приведём пример вывода подобной информации на корневом устройстве(рис. [-@fig:0016]).

![Просмотр информации о STP для vlan 3 на msk-donskaya-eademidova-sw-1](image/6.png){#fig:016 width=90%}

Приведём пример вывода подобной информации не на корневом устройстве(рис. [-@fig:0017]).

![Просмотр информации о STP для vlan 3 на msk-donskaya-eademidova-sw-2](image/17.png){#fig:017 width=90%}

2. При помощи какой команды можно узнать, в каком режиме, STP или Rapid PVST+, работает устройство? Приведите примеры вывода подобной информации на устройствах.

Можно узнать в каком режиме работает устройство посмотрев текующую конфигурацию с помощью команды `show run`(рис. [-@fig:0018]).

![Просмотр режима устройства Rapid PVST+](image/18.png){#fig:018 width=90%}

3. Для чего и в каких случаях нужно настраивать режим Portfast?

PortFast. Это функция протокола STP, которая позволяет Edged Port — порту с подключенным конечным пользователем сразу перейти к состоянию Forwarding, минуя состояния Listening и Learning. Это позволяет ускорить процесс подключения порта. Эту функцию рекомендуется использовать при подключении узлов, чтобы они могли начать обмен данными по сети VLAN немедленно, не дожидаясь протокола spanning-tree. Используется в случаях, когда к порту подключены только оконечные устройства

4. В чем состоит принцип работы агрегированного интерфейса? Для чего он используется?

Агрегированный интерфейс объединяет несколько сетевых интерфейсов для увеличения пропускной способности и обеспечения отказоустойчивости. Он используется для повышения производительности и надежности сетевого соединения.

5. В чём принципиальные отличия при использовании протоколов LACP (Link Aggregation Control Protocol), PAgP (Port Aggregation Protocol) и статического агрегирования без использования протоколов?

LACP и PAgP - динамические протоколы, управляющие созданием и управлением агрегированных соединений. Статическое агрегирование настраивается вручную без использования протоколов.

6. При помощи каких команд можно узнать состояние агрегированного канала EtherChannel?

Для проверки состояния агрегированного канала EtherChannel используются команды "show etherchannel summary" и "show etherchannel port-channel".

# Выводы

В результате выполнения лабораторной работы изучили возможности протокола STP и его модификаций по обеспечению отказоустойчивости сети, агрегированию интерфейсов и перераспределению нагрузки между ними.
