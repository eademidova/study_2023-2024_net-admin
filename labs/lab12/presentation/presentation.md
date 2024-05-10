---
## Front matter
lang: ru-RU
title: Лабораторная работа № 12
subtitle: Настройка NAT
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

# Цели и задачи

## Цели

Приобретение практических навыков по настройке доступа локальной сети к внешней сети посредством NAT.

## Задачи

1. Сделать первоначальную настройку маршрутизатора provider-gw-1 и коммутатора provider-sw-1 провайдера: задать имя, настроить доступ по паролю и т.п.
2. Настроить интерфейсы маршрутизатора provider-gw-1 и коммутатора provider-sw-1 провайдера: 
3. Настроить интерфейсы маршрутизатора сети «Донская» для доступа к сети провайдера.
4. Настроить на маршрутизаторе сети «Донская» NAT с правилами, указанными в разделе 12.2.
5. Настроить доступ из внешней сети в локальную сеть организации, как указано в разделе 12.2.
6. Проверить работоспособность заданных настроек.

# Выполнение лабораторной работы

## Настройка NAT

![Первоначальная настройка маршрутизатора provider-eademidova-gw-1](image/1.png){#fig:001 width=50%}

## Настройка NAT

![Первоначальная настройка коммутатора provider-eademidova-sw-1](image/2.png){#fig:003 width=50%}

## Настройка NAT

![Настройка интерфейсов маршрутизатора provider-eademidova-gw-1](image/3.png){#fig:002 width=42%}

## Настройка NAT

![Настройка интерфейсов коммутатора provider-eademidova-sw-1](image/4.png){#fig:004 width=42%}

## Настройка NAT

![Настройка интерфейсов маршрутизатора msk-donskaya-eademidova-gw-1](image/5.png){#fig:005 width=45%}

## Проверка NAT

![Проверка связи между маршрутизаторами](image/6.png){#fig:006 width=90%}

## Проверка NAT

![Проверка связи между сервером и маршрутизатором](image/7.png){#fig:007 width=90%}

## Настройка NAT

![Настройка пула адресов для NAT](image/8.png){#fig:008 width=90%}

## Настройка NAT

![Настройка списка доступа для NAT](image/9.png){#fig:009 width=90%}

## Настройка NAT

![Настройка NAT](image/10.png){#fig:010 width=90%}

## Настройка NAT

![Схема сети Интернет с ноутбуком](image/11.png){#fig:011 width=90%}

## Настройка NAT

![Настройка доступа из Интернета](image/12.png){#fig:012 width=90%}

## Проверка NAT

![Доступ dk-donskaya-1 к www.yandex.ru](image/13.png){#fig:013 width=70%}

## Проверка NAT

![Доступ dk-donskaya-1 к esystem.pfur.ru](image/14.png){#fig:014 width=70%}

## Проверка NAT

![Доступ dep-donskaya-1 к www.yandex.ru](image/15.png){#fig:015 width=70%}

## Проверка NAT

![Доступ dep-donskaya-1 к esystem.pfur.ru](image/16.png){#fig:016 width=70%}

## Проверка NAT

![Проверка доступа из Интернета по ftp](image/17.png){#fig:017 width=45%}

## Проверка NAT

![Проверка доступа из Интернета к web-серверу](image/18.png){#fig:018 width=90%}

# Выводы

В результате выполнения лабораторной были приобретены практические навыки по настройке доступа локальной сети к внешней сети посредством NAT.