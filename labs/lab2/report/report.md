---
## Front matter
title: "Лабораторная работа № 2. Настройка DNS-сервера."
subtitle: "Отчет"
author: "Анна Александровна Глушенок"

## Generic options
lang: ru-RU
toc-title: "Содержание"

## Pdf output format
toc: true
toc-depth: 2
lof: true
lot: false
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt

## I18n babel
babel-lang: russian
babel-otherlangs: english

## Fonts
mainfont: Liberation Serif
sansfont: Liberation Sans
monofont: Liberation Mono

## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
lofTitle: "Список иллюстраций"

## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float}
  - \floatplacement{figure}{H}
---

# Цель работы

Приобретение практических навыков по установке и конфигурированию DNS-сервера, усвоение принципов работы системы доменных имён.

# Установка DNS-сервера

1. Запустите виртуальную машину server:

![](image/1.png){#fig:001 width=80%}

2. Перейдите в режим суперпользователя

![](image/2.png){#fig:002 width=80%}

3. Установите bind и bind-utils

![](image/3.png){#fig:003 width=80%}

4. С помощью утилиты dig сделайте запрос, например, к DNS-адресу www.yandex.ru:

![](image/4.png){#fig:004 width=80%}

# Конфигурирование кэширующего DNS-сервера при отсутствии фильтрации DNS-запросов маршрутизаторами

1. В отчёте проанализируйте построчно содержание файлов. 

![](image/5.png){#fig:005 width=80%}

2. Запустите DNS-сервер
3. Включите запуск DNS-сервера в автозапуск при загрузке системы

![](image/6.png){#fig:006 width=80%}

4. Проанализируйте в отчёте отличие в выведенной на экран информации при выполнении команд dig www.yandex.ru
и dig @127.0.0.1 www.yandex.ru

![](image/7.png){#fig:007 width=80%}

![](image/8.png){#fig:008 width=80%}

5. Сделайте DNS-сервер сервером по умолчанию для хоста server и внутренней вир-
туальной сети

![](image/9.png){#fig:009 width=80%}

6. Перезапустите NetworkManager, Проверьте наличие изменений в файле /etc/resolv.conf.

![](image/10.png){#fig:010 width=80%}

7. Требуется настроить направление DNS-запросов от всех узлов внутренней сети, включая запросы от узла server, через узел server. Для этого внесите изменения в файл /etc/named.conf

![](image/11.png){#fig:011 width=80%}

8. . Внесите изменения в настройки межсетевого экрана узла server, разрешив работу с DNS

![](image/12.png){#fig:012 width=80%}

9. Убедитесь, что DNS-запросы идут через узел server, который прослушивает порт 53

![](image/13.png){#fig:013 width=80%}

# Конфигурирование первичного DNS-сервера

1. Скопируйте шаблон описания DNS-зон named.rfc1912.zones из каталога /etc в ка-
талог /etc/named и переименуйте его в user.net 

![](image/14.png){#fig:014 width=80%}

2. Включите файл описания зоны /etc/named/user.net в конфигурационном файле DNS /etc/named.conf

![](image/15.png){#fig:015 width=80%}

3. Откройте файл /etc/named/user.net на редактирование

![](image/16.png){#fig:016 width=80%}

4. В каталоге /var/named создайте подкаталоги master/fz и master/rz, в которых будут располагаться файлы прямой и обратной зоны соответственно

![](image/17.png){#fig:017 width=80%}

5. Скопируйте шаблон прямой DNS-зоны named.localhost из каталога /var/named в каталог /var/named/master/fz и переименуйте его в user.net 

![](image/18.png){#fig:018 width=80%}

6. Измените файл /var/named/master/fz/user.net

![](image/19.png){#fig:019 width=80%}

7. Скопируйте шаблон обратной DNS-зоны named.loopback из каталога /var/named в каталог /var/named/master/rz и переименуйте его в 192.168.1
8. Измените файл /var/named/master/rz/192.168.1

![](image/20.png){#fig:020 width=80%}

9. Далее требуется исправить права доступа к файлам в каталогах /etc/named и /var/named, чтобы демон named мог с ними р10. После изменения доступа к конфигурационным файлам named требуется корректно восстановить их метки в SELinuxаботать
10. После изменения доступа к конфигурационным файлам named требуется корректно восстановить их метки в SELinux. Для проверки состояния переключателей SELinux, относящихся к named, введите: getsebool -a | grep named. При необходимости дайте named разрешение на запись в файлы DNS-зоны:

![](image/21.png){#fig:021 width=80%}

![](image/22.png){#fig:022 width=80%}

# Анализ работы DNS-серверf

1. При помощи утилиты dig получите описание DNS-зоны с сервера ns.user.net
2. При помощи утилиты host проанализируйте корректность работы DNS-сервера

![](image/23.png){#fig:023 width=80%}

![](image/24.png){#fig:024 width=80%}

![](image/25.png){#fig:025 width=80%}

# Внесение изменений в настройки внутреннего окружения виртуальной машины

1. На виртуальной машине server перейдите в каталог для внесения изменений в настройки внутреннего окружения /vagrant/provision/server/, создайте в нём каталог dns, в который поместите в соответствующие каталоги конфигурационные файлы DNS

![](image/26.png){#fig:026 width=80%}

2. В каталоге /vagrant/provision/server создайте исполняемый файл dns.sh

![](image/27.png){#fig:027 width=80%}

3. Для отработки созданного скрипта во время загрузки виртуальной машины server в конфигурационном файле Vagrantfile необходимо добавить в разделе конфигурации для сервера

![](image/28.png){#fig:028 width=80%}

# Выводы

В ходе выполнения лабораторной работы № 2 мне удалось  прибрести практические навыки по установке и конфигурированию DNS-сервера, усвоение принципов работы системы доменных имён.
