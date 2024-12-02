
# Практическая работа 9 Знакомство с облачными платформами IoT Создание моделей и объектов
## Задание по подключению MQTT устройства к облачной платформе Rightech
Цель: подключить и настроить устройство с поддержкой MQTT на платформе Rightech IoT Cloud, используя внешний MQTT-брокер.

1. Регистрация на платформе Rightech IoT Cloud: Перейдите на [Rightech IoT Cloud](https://rightech.io) и зарегистрируйтесь. После регистрации зайдите в свою учетную запись.
2. Создание модели устройства: В личном кабинете перейдите в раздел «Модели». Нажмите «Создать модель» и выберите шаблон для MQTT устройства. Настройте параметры модели:
	- Название модели.
	- Параметры данных (тип данных, параметры передачи).
	- Добавьте свойства (например, температура, влажность) или другие необходимые параметры для мониторинга устройства.
3. Настройка MQTT брокера: Если MQTT брокер ещё не установлен, скачайте и установите MQTT брокер Mosquitto с [официального сайта](https://mosquitto.org/download/). После установки настройте брокер, указав следующие параметры:
	- Порт (по умолчанию 1883 или 8883 для защищенного соединения).
	- Разрешите доступ для устройства через публичную сеть или используйте локальный сервер для тестов.
	- Проверьте соединение с брокером, чтобы убедиться в корректной работе.
4. Добавление устройства в облако Rightech:
   - В разделе «Объекты» на платформе Rightech добавьте новое устройство.
   - Выберите ранее созданную модель и укажите параметры подключения:
     - Адрес MQTT брокера.
     - Порт (1883 или другой, который вы настроили).
     - Топики для подписки и публикации данных (например, `device/data`).
     - Логин и пароль для безопасного подключения, если это требуется вашим брокером.
5. Настройка физического устройства:
	- Программируйте устройство для подключения к MQTT брокеру.
	- Укажите:
	- IP адрес брокера.
	- Порт подключения.
	- Топики для отправки данных.
	- Установите параметры передачи данных, такие как интервал отправки.
	- Запустите устройство и убедитесь, что оно подключено к брокеру и публикует данные.
6. Мониторинг данных на платформе:
	- Перейдите в панель управления в Rightech IoT Cloud.
	- Проверьте, поступают ли данные от устройства в реальном времени.
	- Настройте графики, фильтры, уведомления или триггеры, чтобы мониторить изменения показателей устройства.
7. Тестирование и отладка:
	- В случае отсутствия данных проверьте:
	- Соединение устройства с брокером.
	- Корректность топиков MQTT.
	- Логи на платформе и устройстве.
	- Убедитесь, что данные передаются корректно и отображаются в интерфейсе платформы.

```c++
mosquitto_pub -d -h dev.rightech.io -i mqtt-mirea5sem-1 -t base/state/temperature -m 32 -u user -P 123123 -p 8883
```

Пример MQTT запросов: Например, с mosquitto_pub клиентом из проекта Eclipse Mosquitto.
```c++
$ mosquitto_pub -d -h dev.rightech.io -i <ric-mqtt-client-id> -t base/state/temperature -m 23
```

Публикация данных с устройства: Топик: `device/data`
```c++
mosquitto_pub -h broker_address -t device/data -m '{"temperature": 25}'
```

Подписка на команды: Топик: `device/commands`
```c++
mosquitto_sub -h broker_address -t device/commands
```
## Задание практической работы №9
### Часть 1. Регистрация на платформе Rightech IoT Cloud 
Rightech IoT Cloud — это бескодовая (no-code) IoT-платформа для быстрого создания прикладных проектов интернета вещей. Для регистрации на платформе необходимо перейти по данной ссылке https://dev.rightech.io/

Программный продукт Rightech IoT Cloud (RIC, рус. Райтек ИоТ Клауд) от компании-разработчика КОМНЭТ является фреймворк-инструментом и предназначен для быстрого создания разработчиками приложений интернета вещей) Платформа RIC реализована на принципах универсализации и имеет низкую зависимость от конкретного оборудования и протоколов, что позволяет легко объединять разнородные устройства в едином разрабатываемом на платформе решении.

### Часть 2. Создание виртуальных устройств в облаке
Согласно варианту по номеру бригады создайте в облаке виртуальные устройства для получения данных. Каждое устройство должно иметь свой профиль, соответствующий передаваемым на устройство данным. В качестве протокола для профилей устройств используйте MQTT. 

1.	Датчик движения
2.	Датчик температуры
3.	Датчик напряжения

### Часть 3. Отправка данных в облако
Выполните передачу тестовых данных в каждое из созданных устройств. Данные должны соответствовать типу устройства, то есть, к примеру, в термометр должна поступить температура. Данные можно передавать при помощи утилиты `mosquito_pub`. Ссылка на документацию по передаче данных на устройства по MQTT.

В отчете необходимо отразить созданные устройства, процесс отправки данных с облако, а также отображение этих данных на виртуальных устройствах в облачной платформе.

![500](../../images/Pasted%20image%2020241201222220.png)

# ПРАКТИЧЕСКАЯ РАБОТА №10 – УПРАВЛЕНИЕ УСТРОЙСТВАМИ ПРИ ПОМОЩИ ПЛАТФОРМ ИНТЕРНЕТА ВЕЩЕЙ
На платформе Rightech реализуйте сценарии, предложенные в таблице 1 согласно своему варианту, используя приведенную в методичке теоретическую информацию.

1. Включение и выключение вентилятора по температуре
2. Изменение цвета диодной ленты по датчику влажности

В отчете необходимо отразить файл конфигурации для подключения, схему автомата, описать логику работы автомата, скриншоты состояний и переходов, состояния устройств в журнале объектов

# ПРАКТИЧЕСКАЯ РАБОТА №11 – РЕАКЦИИ ПЛАТФОРМ ИНТЕРНЕТА ВЕЩЕЙ НА ПРИХОДЯЩИЕ ДАННЫЕ
Добавьте в логику правил из 10 практической работы формирование нескольких типов тревог: 
- Для первого объекта логики из варианта – тревогу при выходе приходящего параметра за допустимые границы (границы задайте самостоятельно и проверьте работоспособность на физическом датчике); 
- Для второго объекта логики из варианта – тревогу при отсутствии ожидаемого параметра в приходящем сообщении (к примеру, в приходящем сообщении отсутствует параметр с состоянием кнопки);

В отчет включите обновленные цепочки правил, скрипты проверок и формирования тревог, а также результаты тестирования цепочек при помощи утилит mosquitto.

# ПРАКТИЧЕСКАЯ РАБОТА №12 – ОТПРАВКА ОПОВЕЩЕНИЙ ОТ ОБЛАЧНОЙ ПЛАТФОРМЫ
Реализуйте отправку e-mail сообщений из облачной платформы при возникновении тревог на автомате, созданных в практической работе №11. В качестве SMTP сервера для пересылки сообщений предлагается использовать Yandex и Google.

В отчет включите обновленную схему автомата, параметры настройки SMTP-сервера и отправки письма на электронную почту, а также результаты тестирования SMTP-сервера, автомата и скриншоты приходящих электронных писем.