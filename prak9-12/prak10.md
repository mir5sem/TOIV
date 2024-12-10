# Практическая работа №10 – Управление устройствами при помощи платформ Интернета вещей
### Логика
Цель раздела «Логика» заключается в повышении уровня абстракции: от работы с моделями и элементами устройства к созданию сценариев автоматического взаимодействия с ним. Каждый сценарий автоматизации — это алгоритм, который определяет логику поведения объекта. С помощью такого сценария можно отслеживать изменения в устройстве и, в зависимости от этих изменений, автоматически выполнять соответствующие действия без участия пользователя. Сценарий автоматизации основан на конечном автомате, состоящем из состояний и переходов между ними.

Конечный автомат (или детерминированный конечный автомат, ДКА) — это математическая модель, используемая для описания поведения систем с конечным числом состояний. Конечный автомат состоит из множества состояний, событий и правил, которые определяют, как система переходит из одного состояния в другое на основе событий или входных данных.

### Основные элементы конечного автомата
1. Конечное множество состояний — набор возможных состояний, в которых может находиться система. Каждое состояние описывает определённое положение или характеристику системы. Например, для системы безопасности дома состояния могут быть "Система активна" и "Система отключена".
2. Начальное состояние — это состояние, в котором система находится в самом начале. Для каждого конечного автомата оно одно.
3. Конечное множество событий или входных данных — события, которые приводят к изменению состояния системы. Эти события могут быть внешними (например, нажатие кнопки) или внутренними (например, изменение температуры).
4. Правила переходов или функция перехода — набор правил, которые определяют, как система переходит из одного состояния в другое в ответ на конкретное событие или входные данные. Переход всегда однозначно определён: при получении одного и того же события система всегда переходит в одно и то же состояние.
5. Конечное множество конечных состояний — определенные состояния, в которых система завершает выполнение своей логики. Это может быть состояние успешного завершения работы или сбоя.

### Пример работы конечного автомата
Представим простой автомат для турникета в метро:
- Состояния: "Заблокирован" и "Разблокирован".
- События: "Билет проведён" и "Прохождение через турникет".

Правила переходов:
1. Если турникет заблокирован и проведён билет, то он переходит в состояние "Разблокирован".
2. Если турникет разблокирован, и кто-то проходит через него, он возвращается в состояние "Заблокирован".
В этом примере при каждом событии система чётко определяет своё текущее состояние и действует в соответствии с правилами переходов.

### Инструкция по настройке файла конфигурации для подключения к демонстрационному стенду (чемодану)
Для подключения облачной платформы Rightech к демонстрационному стенду Wirenboard (чемодану) необходимо в домашней директории пользователя добавить конфигурацию в файл mosquitto.conf:

```
#rightech connect config
connection rightech
address dev.rightech.io:1883
clientid temp_1
try_private false
start_type automatic
topic /devices/имя_устройства/controls/параметр both
topic /devices/имя_устройства/controls/параметр both
```

**!!! Обратите внимание на то, что необходимо указывать конкретные топики устройств.**

Это связано с тем, что платформа Rightech имеет ограничение в 14400 пакетов на отправку в сутки от одного объекта. После превышения данной квоты, платформа блокирует объект на ограниченное время (до конца дня по UTC+0).

### Создание сценария автоматизации
Для создания нового автомата необходимо перейти на вкладку «Логика» и добавить автомат, нажав на «+». После нажатия на данную кнопку, откроется окно следующего вида:
