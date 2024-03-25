---
## Front matter
lang: ru-RU
title: Лабораторная работа № 6
subtitle: Статическая маршрутизация VLAN
author:
  - Демидова Е. А.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 16 марта 2024

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

Настроить статическую маршрутизацию VLAN в сети.

**Задачи**

1. Добавить в локальную сеть маршрутизатор, провести его первоначальную настройку.
2. Настроить статическую маршрутизацию VLAN.
3. При выполнении работы необходимо учитывать соглашение об именовании.

# Выполнение лабораторной работы

## Настройка маршрутизатора

![Настройка маршрутизатора msk-donskaya-eademidova-пw-1](image/1.png){#fig:001 width=50%}

## Настройка Trunk-порта коммутатора

![Настройка Trunk-порта коммутатора msk-donskaya-eademidova-sw-1](image/2.png){#fig:002 width=50%}

## Настройка виртуальных интерфейсов

![Настройка виртуальных интерфейсов на маршрутизаторе](image/3.png){#fig:003 width=40%}

## Проверка доступности устройств

![Проверка доступности устройств с помоощью команды `ping`](image/4.png){#fig:004 width=35%}

## Проверка доступности устройств

![Проверка доступности устройств в режиме симулции в разных VLAN](image/5.png){#fig:005 width=65%}

## Проверка доступности устройств

![Проверка доступности устройств в режиме симулции в одном VLAN](image/6.png){#fig:006 width=90%}

## Просмотр пакета

![Содержимое ICMP-пакета](image/7.png){#fig:007 width=50%}

# Выводы

В результате выполнения лабораторной работы получили основные навыки по настройке статической марщрутизации VLAN в сети.