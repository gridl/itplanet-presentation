## 1 слайд

Тема моего диплома: "Разработка виртуальной инфраструктуры для реализации облачных услуг" напрямую не связана со свободным ПО.

Мой доклад будет об использовании свободного программного обеспечения в этой инфраструктуре.

## 2 слайд — Разработка виртуальной инфраструктуры для реализации облачных услуг

В ходе диплома необходимо было разработать инфраструктуру, которая могла бы предоставлять услуги хостинга сайтов, а также предоставление аренды виртуальных выделенных серверов для клиентов.

Основные требования которые я поставил перед собой перед началом проектирования:
- лишиться единых точек отказа по максимуму где это возможно, это в первую очередь резервные каналы связи, использование RAID-массивов, репликация DNS-серверов
- защита от несанкционированного доступа и DDoS-атак, как небольших flood-атаки, так и крупных заказных атак, при котором забиваются гигабитные каналы
- необходимо использовать свободное ПО из-за ограниченности бюджета
- на ранних этапах проектирования необходимо предусмотреть документирование и автоматизацию инфраструктуры, так как при разрастании инфраструктуры обслуживать ее будет все сложнее, а документирование всех действий и автоматизация очень облегчает этот процесс

## 3 слайд — Общая схема инфраструктуры

В ходе разработки инфраструктуры была составлена общая схема инфраструктуры, которая представлена на слайде.

Большая часть оборудования была размещена в одном из московских дата-центров, сервера для дочерних DNS-серверов и серверов мониторинга были размещены в другом дата-центре, также в Москве.

В качестве аппаратной части использовались блейд-сервера на основе Supermicro, типовых конфигураций с оперативной памятью от 48 до 96GB.

Для высокой скорости работы дисковой подсистемы использованы SSD-диски, объединенные в массив RAID-10, на серверах бекапов SATA-диски объединенные в RAID-10, каждый диск размером 4TB.

## 4 слайд — Серверная операционная система

Для инфраструктуры была выбрана операционная система Linux, а именно дистрибутив CentOS 7.

Дистрибутив вышел в 2014 году, поэтому полная поддержка пакетной базы продлится до 2020 года, а устранение критических уязвимостей до 2024 года.

CentOS является открытым проектом, который основан на коммерческом дистрибутиве Red Hat Enterprise Linux 7, и совместим с ним, поэтому документации в сети достаточно.

Ну и самое главное, у меня был опыт работы с этим дистрибутивом и он мне нравится.

## 5 слайд — Мониторинг

Nagios является системой событийного мониторинга Linux-систем.

При каких-либо проблемах на серверах возможна отправка уведомления по почте или SMS, либо можно вести мониторинг в реальном режиме в веб-браузере.

В ходе эксплуатации Nagios были замечены некоторые баги с утечками памяти, очередями проверок.

*переключение слайда*

В ходе поисков решений этих проблем было решено мигрировать на Icinga2, который является ответвлением (форком) Nagios.

В нем исправлено много проблем и добавлены новые особенности, такие как переработанный пользовательский интерфейс, расширенная документация.

А самое главное, что все скрипты мониторинга, которые работали в Nagios так же работали и в Icinga2, то есть они сохранили обратную совместимость.

## 6 слайд — Метрики

Для построения графиков использовался Munin, который отлично справляется со своей задачей.

Графики нужны для анализа нагрузки на сервера, исследования аномальных ситуаций и анализа работы серверов и сервисов.

Преимущества Munin в большом количестве плагинов, а также в простоте написания своих.

## 7 слайд — Автоматизация управления

Ansible позволяет централизованно управлять серверами.

Это удобно использовать в гомогенных средах, таких как сервера хостинга.

Преимущества использования Ansible по сравнению с аналогами Puppet/Chef/SaltStack -- это относительно низкий порог вхождения, отсутствие тяжелых зависимостей, все что нужно это запущенная служба SSH.

Написание сценариев (их называют playbook'ами) очень простое и наглядное, для этого используется удобочитаймый синтаксис YAML.

## 8 слайд — Виртуализация

Для создания виртуальных выделенных серверов необходимо использование технологий виртуализации.

С помощью технологии OpenVZ можно на одном физическом сервере создавать множество виртуальных серверов.

У каждого такого сервера есть свой IP-адрес, своя операционная система, установленные приложения, управляются они так же как и физический сервер.

Единственный минус технологии, обусловленный его архитектурой, в таком контейнере можно запускать только Linux-дистрибутивы.

Но зато скорость работы таких контейнеров практически не отличается от работы реального физического сервера.

*переключение слайда*

Для клиентов, которые хотят устанавливать в свои виртуальные серверы Windows или FreeBSD например, необходимо использование технологии полной (аппаратной) виртуализации, такую как KVM.

Виртуальные машины KVM не настолько быстрые как контейнеры на OpenVZ, но зато обеспечивают эмуляцию собственного оборудования и изменение ядра гостевой ОС.

## 9 слайд — Защита от вредоносов

Уязвимости в движках клиентских сайтов позволяют злоумышленникам получать ограниченные доступы к серверу, чаще всего это рассылка спама, размещение фишинговых страниц, кража баз данных.

Maldet позволяет по известным сигнатурам обнаруживать вредоносные файлы, перемещать в карантин для ручного исследования зараженных файлов и даже в некоторых случаях лечить автоматически.

## 10 слайд — Защита сети

Защита сети обеспечивается в первую очередь правильно настроенным фаерволом (IPTables), а также мониторингом наиболее активных соединений к серверу, в этом могут помочь fail2ban, ipset и ddos-deflate.

При грамотной настройке фаерволла и системных настроек стека TCP/IP возможно блокирование атак вплоть до 100Mb/s.

*шпаргалка по параметрам ядра*
- tcp_max_syn_backlog определяет максимальное число запоминаемых запросов на соединение, для которых не было получено подтверждения от подключающегося клиента
- net.ipv4.tcp_syncookies защита от syn-flood атак
- net.ipv4.conf.default.rp_filter защита от подмены IP
- tcp_fin_timeout определяет время сохранения сокета в состоянии FIN-WAIT-2 после его закрытия локальной стороной
- tcp_synack_retries определяет число попыток повтора передачи пакетов SYNACK для пассивных соединений TCP.
net.core.netdev_max_backlog определяет максимальное количество пакетов в очереди на обработку, если интерфейс получает пакеты быстрее, чем ядро может их обработать
- net.core.somaxconn аксимальное число открытых сокетов, ждущих соединения

## 11 слайд — Панели управления для клиентов

Клиенты арендующие виртуальные сервера, как правило, не очень хорошо администрируют сервер из консоли, поэтому для этого им удобно пользоваться панелью управления.

Одна из таких - это Vesta, она обладает широким функционалом, простым интерфейсом и бесплатна для клиентов.

Она проста в установке, поэтому ее легко интегрировать в скрипты развертывания окружений контейнеров.

Приятно что ведется активная разработка панели, особенно радует стек предустановленного программного обеспечения, мультиязычный интерфейс, и очень мощные средства управления через консоль.

## 12 слайд — Сравнение с закрытыми аналогами

В данной таблице можно увидеть используемые Open Source инструменты и их закрытые аналоги с указанием цен на использование.

Представим себе небольшую инфраструктуру с 10-ю серверами виртуального хостинга, 10-ю серверами Virtuozzo и 10-ю vSphere Server.

Стоимость лицензий и сторонней поддержки программного обеспечения для такой инфраструктуры будет стоит примерно 262 000 долларов в год.

## 13 слайд — Проекты в Open Source

Было проделано много работы, прочитано море документации, набито десятки шишек, некоторые проекты, скрипты, руководства я выложил в Open Source.

В частности руководство по администрированию OpenVZ, руководство по администрированию новой версии Virtuozzo 7.

Оригинальный скрипт ddos-deflate, который я нашел на сайте автора в интернете с недавних пор недоступен, очень вовремя я его форкнул и доделал под себя.

Один из playbook'ов по развертыванию окружения для WordPress в Virtuozzo-контейнере я также выложил в открытый доступ.

На том же GitHub есть репозиторий с некоторыми моими скриптами для мониторинга.

Ну и сам диплом тоже есть в открытом доступе, я его писал с помощью LaTeX, поэтому кому-то он еще пригодится в качестве шаблона для своего диплома.
