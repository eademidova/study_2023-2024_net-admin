---
## Front matter
lang: ru-RU
title: Лабораторная работа № 16
subtitle: Настройка VPN
author:
  - Демидова Е. А.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 30 мая 2024

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

Получение навыков настройки VPN-туннеля через незащищённое Интернет-соединение.

**Задачи**

Настроить VPN-туннель между сетью Университета г. Пиза (Италия) и сетью «Донская» в г. Москва

# Выполнение лабораторной работы

## Размещение оборудования

![Схема сети](image/1.png){#fig:001 width=90%}

## Размещение оборудования

![Города сети](image/2.png){#fig:003 width=60%}

## Размещение оборудования

![Физическая область города Пиза](image/3.png){#fig:002 width=90%}

## Первоначальная настройка оборудования

![Настройка маршрутизатора pisa-unipi-eademidova-gw-1](image/4.png){#fig:004 width=70%}

## Первоначальная настройка оборудования

![Настройка коммутатора pisa-unipi-eademidova-sw-1](image/5.png){#fig:005 width=70%}

## Первоначальная настройка оборудования

![Настройка интерфейсов маршрутизатора pisa-unipi-eademidova-gw-1](image/6.png){#fig:006 width=70%}

## Первоначальная настройка оборудования

![Настройка интерфейсов коммутатора pisa-unipi-eademidova-sw-1](image/7.png){#fig:007 width=70%}

## Первоначальная настройка оборудования

![Проверка связи между устройствами в городе Пиза](image/8.png){#fig:008 width=60%}

## Настройка VPN на основе GRE

![Настройка VPN на маршрутизаторе msk-donskaya-eademidova-gw-1](image/9.png){#fig:009 width=80%}

## Настройка VPN на основе GRE

![Настройка VPN на маршрутизаторе pisa-unipi-eademidova-gw-1](image/10.png){#fig:010 width=90%}

## Настройка VPN на основе GRE

![Проверка доступности узлов сети Университета г. Пиза из сети Донская](image/11.png){#fig:011 width=90%}

# Выводы

В результате выполнения лабораторной были приобретены практические навыки по настройке VPN-туннеля через незащищённое Интернет-соединение.