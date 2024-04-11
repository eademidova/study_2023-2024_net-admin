---
## Front matter
lang: ru-RU
title: Лабораторная работа № 9
subtitle: Использование протокола STP. Агрегирование каналов
author:
  - Демидова Е. А.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 11 апреля 2024

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

Изучение возможностей протокола STP и его модификаций по обеспечению отказоустойчивости сети, агрегированию интерфейсов и перераспределению нагрузки между ними.

**Задачи**

1. Сформируйте резервное соединение между коммутаторами msk-donskaya-sw-1 и msk-donskaya-sw-3.
2. Настройте балансировку нагрузки между резервными соединениями.
3. Настройте режим Portfast на тех интерфейсах коммутаторов, к которым подключены серверы.
4. Изучите отказоустойчивость резервного соединения.
5. Сформируйте и настройте агрегированное соединение интерфейсов Fa0/20 -- Fa0/23 между коммутаторами msk-donskaya-sw-1 и msk-donskaya-sw-4.

# Выполнение лабораторной работы

## Схема сети

![Схема сети в логической рабочей области Packet Tracer](image/1.png){#fig:001 width=70%}

## Настройка резервного соединения

![Логическая схема локальной сети с резервным соединением](image/2.png){#fig:002 width=65%}

## Настройка резервного соединения

![Проверка доступности устройств с помощью команды `ping`](image/3.png){#fig:003 width=50%}

## Настройка резервного соединения

![Проверка доступности устройств в режиме симуляции](image/4.png){#fig:004 width=70%}

## Настройка STP

![Просмотр информации о STP для vlan 3 на msk-pavlovskaya-eademidova-sw-1](image/5.png){#fig:005 width=50%}

## Настройка STP

![Просмотр информации о STP для vlan 3 на msk-donskaya-eademidova-sw-1](image/6.png){#fig:006 width=50%}

## Настройка STP

![Проверка пути от хоста dk-donskaya-1 до mail](image/7.png){#fig:007 width=70%}

## Настройка STP

![Проверка пути от хоста dk-donskaya-1 до web](image/8.png){#fig:008 width=70%}

## Настройка Portfast

![Настройка режима Portfast на msk-donskaya-eademidova-sw-2](image/9.png){#fig:009 width=70%}

## Настройка Portfast

![Настройка режима Portfast на msk-donskaya-eademidova-sw-3](image/10.png){#fig:010 width=70%}

## Извучение отказоустойчивости

![Изучение отказоустойчивости протокола STP и время восстановления соединения](image/11.png){#fig:011 width=70%}

## Настройка Rapid PVST+

```
msk-donskaya-eademidova-sw-1( config )#spanning-tree mode rapid-pvst
msk-donskaya-eademidova-sw-2( config )#spanning-tree mode rapid-pvst
msk-donskaya-eademidova-sw-3( config )#spanning-tree mode rapid-pvst
msk-donskaya-eademidova-sw-4( config )#spanning-tree mode rapid-pvst
msk-pavlovskaya-eademidova-sw-1( config )#spanning-tree mode rapid-pvst
```

## Настройка Rapid PVST+

![Изучение отказоустойчивость протокола Rapid PVST+ и время восстановления соединения](image/12.png){#fig:012 width=70%}

## Агрегирование каналов

![Логическая схема локальной сети с агрегированным соединением](image/13.png){#fig:013 width=70%}

## Агрегирование каналов

![Настройка агрегирования каналов на msk-donskaya-eademidova-sw-1](image/15.png){#fig:014 width=35%}

## Агрегирование каналов

![Настройка агрегирования каналов на msk-donskaya-eademidova-sw-1](image/14.png){#fig:015 width=40%}

# Выводы

В результате выполнения лабораторной работы изучили возможности протокола STP и его модификаций по обеспечению отказоустойчивости сети, агрегированию интерфейсов и перераспределению нагрузки между ними.