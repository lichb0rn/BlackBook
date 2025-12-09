---
title: "Пошаговое руководство как собрать ядро Linux с нуля"
source: "https://wiki.merionet.ru/articles/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya"
author:
  - "[[Merion Academy]]"
published:
created: 2025-12-09
description: "Большое пошаговое руководство как собрать ядро Linux с нуля"
tags:
  - "clippings"
---
## Пошаговое руководство как собрать ядро Linux с нуля

Ядро **Linux** является основой **Unix** -подобных операционных систем. Ядро отвечает за связь между оборудованием и программным обеспечением и за распределение доступных ресурсов.

### Сборка ядра Linux

Процесс создания ядра Linux состоит из семи простых шагов. Однако процедура требует значительного времени для завершения, в зависимости от скорости системы.

> Примечание. Если версия на веб-сайте ядра не совпадает с версией из приведенных ниже шагов, используйте эти команды и замените номер версии ядра.

---

### Шаг 1. Загрузите исходный код

1\. Посетите официальный сайт ядра [www.kernel.org](https://www.kernel.org/) и загрузите последнюю версию. Загруженный файл содержит сжатый исходный код.

[![www.kernel.org](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/1.png "www.kernel.org")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/1.png)

2\. Откройте терминал и используйте команду `wget` для загрузки исходного кода ядра Linux:

```ruby
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.9.6.tar.xz
```

По завершении загрузки в выходных данных отображается сообщение "saved".

[![saved](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/2.png "saved")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/2.png)

---

### Шаг 2: извлеките исходный код

Когда файл будет готов, запустите команду `tar`, чтобы извлечь исходный код:

```
tar xvf linux-5.9.6.tar.xz
```

Вывод отображает извлеченный исходный код ядра:

[![Извлеченный исходный код](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/3.png "Извлеченный исходный код")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/3.png)

---

### Шаг 3: Установите необходимые пакеты

Перед сборкой ядра установите дополнительные пакеты. Для этого запустите эту команду:

```csharp
sudo apt-get install git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison
```

Команда, которую мы использовали выше, устанавливает следующие пакеты:

- **git** - отслеживает и записывает все изменения исходного кода во время разработки. Это также позволяет отменить изменения.
- **fakeroot** - упаковочный инструмент, создающий фальшивую корневую среду.
- **build-essential** - Устанавливает инструменты разработки, такие как C, C++, gcc и g++.
- **ncurses-dev** - Библиотека программирования, предоставляющая API для текстовых терминалов.
- **xz-utils** - обеспечивает быстрое сжатие и распаковку файлов.
- **libssl-dev** - поддерживает SSL и TSL, которые шифруют данные и делают интернет-соединение безопасным.
- **bc (Basic Calculator)** - математический язык сценариев, поддерживающий интерактивное выполнение операторов.
- **flex (Fast Lexical Analyzer Generator)** - генерирует лексические анализаторы, преобразующие символы в токены.
- **libelf-dev** - выдает общую библиотеку для управления файлами ELF (исполняемые файлы, дампы ядра и объектный код)
- **bison** - генератор парсера GNU, который преобразует описание грамматики в программу на языке C.
[![sudo apt-get install](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/4.png "sudo apt-get install")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/4.png)

---

### Шаг 4: Настройте ядро

Исходный код ядра Linux поставляется с конфигурацией по умолчанию. Однако вы можете настроить его под свои нужды. Для этого выполните следующие действия:

1\. Перейдите к каталогу `linux-5.9.6.` с помощью команды `cd`:

```bash
cd linux-5.9.6
```

2\. Скопируйте существующий файл конфигурации с помощью команды `cp`:

```bash
cp -v /boot/config-$(uname -r) .config
```
[![cp -v /boot/config-$(uname -r) .config<](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/5.png "cp -v /boot/config-$(uname -r) .config<")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/5.png)

3\. Чтобы внести изменения в файл конфигурации, выполните команду `make`:

```
make menuconfig
```

Команда запускает несколько скриптов, которые затем открывают меню конфигурации:

[![make menuconfig](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/6.png "make menuconfig")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/6.png)

4\. Меню конфигурации включает в себя такие параметры, как прошивка, файловая система, сеть и параметры памяти. Используйте стрелки, чтобы сделать выбор, или выберите HELP, чтобы узнать больше о вариантах. Когда вы закончите вносить изменения, выберите SAVE, а затем выйдите из меню.

[![Save](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/7.png "Save")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/7.png)

> Примечание. Изменение настроек некоторых параметров может привести к тому, что ядро не будет работать. Если вы не знаете, что изменить, оставьте настройки по умолчанию.

---

### Шаг 5: Соберите ядро

1\. Начните сборку ядра, выполнив следующую команду:

```
make
```

Процесс сборки и компиляции ядра Linux занимает некоторое время.

Терминал перечисляет все компоненты ядра Linux: управление памятью, драйверы оборудования, драйверы файловой системы, сетевые драйверы и управление процессами.

[![make](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/8.png "make")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/8.png)

2\. Установите необходимые модули с помощью этой команды:

```
sudo make modules_install
```
[![sudo make modules_install](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/9.png "sudo make modules_install")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/9.png)

3\. Наконец, установите ядро, набрав:

```
sudo make install
```

Вывод показывает готово, когда закончено:

[![sudo make install](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/10.png "sudo make install")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/10.png)

---

### Шаг 6. Обновите загрузчик (необязательно)

Загрузчик **GRUB** - это первая программа, которая запускается при включении системы.

Команда `make install` выполняет этот процесс автоматически, но вы также можете сделать это вручную.

1\. Обновите initramfs до установленной версии ядра:

```
sudo update-initramfs -c -k 5.9.6
```

2\. Обновите загрузчик GRUB с помощью этой команды:

```sql
sudo update-grub
```

Терминал выведет процесс и подтверждающее сообщение:

[![sudo update-grub](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/11.png "sudo update-grub")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/11.png)

---

### Шаг 7: перезагрузите и проверьте версию ядра

Когда вы выполните описанные выше действия, перезагрузите компьютер.

Когда система загрузится, проверьте версию ядра с помощью команды `uname`:

```bash
uname -mrs
```

Терминал покажет текущую версию ядра Linux.

[![uname -mrs](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/12.png "uname -mrs")](https://legacy.merionet.ru/images/poshagovoe-rukovodstvo-kak-sobrat-yadro-linux-s-nulya/12.png)

---

### Итог

В этом пошаговом руководстве вы узнали, как собрать ядро Linux с нуля и установить необходимые пакеты.

Ссылка  
скопирована

*![icon strelka](https://wiki.merionet.ru/images/blocks/recommendation/icons/strelka.svg)* *![icons](https://wiki.merionet.ru/images/blocks/recommendation/icons/icon-group-2-mob.svg)*

## узнай больше на курсе

Онлайн-курс по Linux

Курс по Linux от Мерион Нетворкс - стань Linux администратором, прокачай свой скиллсет умением работать с операционными системами линукс и сделай большой шаг к DevOps

[Подробнее о курсе](https://wiki.merionet.ru/merion-academy/course/kurs-po-linux?utm_source=knowledgebase&utm_medium=own&utm_campaign=native_banner)

Полный курс по сетевым технологиям

Полный курс по сетевым технологиям от Мерион Нетворкс - учим с нуля сетевых инженеров и DevOPS специалистов

[Подробнее о курсе](https://wiki.merionet.ru/merion-academy/course/polnyj-kurs-po-kompyuternym-setyam?utm_source=knowledgebase&utm_medium=own&utm_campaign=native_banner)

DevOps-инженер с нуля

Стань DevOps-инженером с нуля и научись использовать инструменты и методы DevOps

[Подробнее о курсе](https://wiki.merionet.ru/merion-academy/course/devops-inzhener-s-nulya?utm_source=knowledgebase&utm_medium=own&utm_campaign=native_banner)

Python программист с нуля

Стань разработчиком на одном из самых популярных языков программирования - Python

[Подробнее о курсе](https://wiki.merionet.ru/merion-academy/course/kurs-po-python?utm_source=knowledgebase&utm_medium=own&utm_campaign=native_banner)

Онлайн-курс по кибербезопасности

Полный курс по кибербезопасности от Мерион Нетворкс - учим с нуля специалистов по информационной безопасности. Пора стать безопасником!

[Подробнее о курсе](https://wiki.merionet.ru/merion-academy/course/kurs-po-kiberbezopasnosti?utm_source=knowledgebase&utm_medium=own&utm_campaign=native_banner)

Онлайн-курс по сетевой безопасности

Изучи основы сетевой безопасности и прокачай скилл системного администратора и сетевого инженера

[Подробнее о курсе](https://wiki.merionet.ru/merion-academy/course/onlajn-kurs-po-setevoj-bezopasnosti?utm_source=knowledgebase&utm_medium=own&utm_campaign=native_banner)

Еще по теме:

![img](https://wiki.merionet.ru/images/wiki/general/icons/servers_theory.png)

[5 Linux команд, о которых вы никогда не слышали](https://wiki.merionet.ru/articles/5-linux-komand-o-kotoryx-vy-nikogda-ne-slysali)

Узнайте про 5 полезных Linux - команд: tldr, timeout, ncdu, fd и trash, которые упрощают жизнь при работе в CLI

![img](https://wiki.merionet.ru/images/wiki/general/icons/servers_theory.png)

[Что такое REST на самом деле?](https://wiki.merionet.ru/articles/cto-takoe-rest-na-samom-dele)

Что позволяет называть один API как REST API, а другой нет? Сейчас попробуем разложить все по полочкам, чтобы ты на собесе жидко не споткнулся о такую, казалось бы, простую тему.

![img](https://wiki.merionet.ru/images/wiki/general/icons/servers_how-to.png)

[Управление портами в Linux: полное руководство](https://wiki.merionet.ru/articles/upravlenie-portami-v-linux-polnoe-rukovodstvo)

Узнайте, как работают сетевые порты в Linux, какие бывают типы портов, и как управлять ими с помощью команд netstat, ss, ufw и iptables

![img](https://wiki.merionet.ru/images/wiki/general/icons/servers_useful.png)

[Nginx: как работает самый быстрый веб-сервер](https://wiki.merionet.ru/articles/nginx-kak-rabotaet-samyi-bystryi-veb-server)

Рассказываем, как появился nginx, его отличия от apache, для чего нужен nginx и какие у него преимущества

![img](https://wiki.merionet.ru/images/wiki/general/icons/servers_how-to.png)

[Установка и настройка Fail2Ban: Ubuntu, CentOS, Fedora и Debian](https://wiki.merionet.ru/articles/ustanovka-i-nastroika-fail2ban-ubuntu-centos-fedora-i-debian)

В этом руководстве вы узнаете, как установить и настроить Fail2ban на своем сервере.