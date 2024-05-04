---
## Front matter
lang: ru-RU
title: Лабораторная работа № 11
subtitle: Настройка NAT. Планирование
author:
  - Демидова Е. А.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 27 апреля 2024

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
---

# Вводная часть

## Цели и задачи

**Цели**

Провести подготовительные мероприятия по подключению локальной сети организации к Интернету.

**Задачи**

1. Построить схему подсоединения локальной сети к Интернету.
2. Построить модельные сети провайдера и сети Интернет.
3. Построить схемы сетей L1, L2, L3.

# Выполнение лабораторной работы

## Схема сети

![Схема L1 сети с выходом в Интернет](image/1.png){#fig:001 width=40%}

## Схема сети

![Схема L2 сети с выходом в Интернет](image/2.png){#fig:003 width=40%}

## Схема сети

![Схема L3 сети с выходом в Интернет](image/3.png){#fig:002 width=90%}

## Схема сети

![Медиаконвертер с модулями PT-REPEATER-NM-1FFE и PT-REPEATER-NM-1CFE](image/4.png){#fig:004 width=50%}

## Схема сети

![Схема сети с выходом в Интернет](image/5.png){#fig:005 width=50%}

## Схема сети

![Схема сети в физической рабочей области Packet Tracer](image/6.png){#fig:006 width=50%}

## Схема сети

![Оборудование в здании сети провайдера](image/7.png){#fig:007 width=60%}

## Схема сети

![Оборудование в здании сети модельного Интернета](image/8.png){#fig:008 width=60%}

## Добавление DNS-записей

: Распределение ip-адресов модельного Интернета {#tbl:ip}

| IP-адреса     | Примечание            |
|---------------|-----------------------|
| 192.0.2.1     | provider-gw-1         |
| 192.0.2.11    | www.yandex.ru         |
| 192.0.2.12    | stud.rudn.university  |
| 192.0.2.13    | esystem.pfur.ru       |
| 192.0.2.14    | www.rudn.ru           |

## Добавление DNS-записей

![Добавление DNS-записей](image/9.png){#fig:009 width=50%}


# Выводы

В результате выполнения лабораторной работы провели подготовительные мероприятия по подключению локальной сети организации к Интернету.