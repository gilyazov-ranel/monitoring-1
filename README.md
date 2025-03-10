# Домашнее задание к занятию "13.Системы мониторинга"

## Обязательные задания

1. Вас пригласили настроить мониторинг на проект. На онбординге вам рассказали, что проект представляет из себя 
платформу для вычислений с выдачей текстовых отчетов, которые сохраняются на диск. Взаимодействие с платформой 
осуществляется по протоколу http. Также вам отметили, что вычисления загружают ЦПУ. Какой минимальный набор метрик вы
выведите в мониторинг и почему?
### Ответ
Минимальный набор метрик:   
    Загрузка ЦПУ - поможет отслеживать, интенсивность использования ресурсов системы  
    Время отклика - необходимо для оценки производительности системы и ее отзывчивости  
    Число активных запросов - поможет в планировании ресурсов  
    Использование памяти - поможет предотвратить утечки памяти для обеспечения стабильной работы  
    Ошибки -  поможет выявлять проблемы в системе    
    Метрики для хранилища:  
        Общий объем хранилища - сколько места доступно в системе   
        Используемое пространство - объем данных, уже записанных в хранилище   
        Свободное пространство - количество доступного места для новых данных   
        Скорость чтения и записи - производительность операций ввода-вывода, что влияет на время доступа к данным  
        Число операций ввода-вывода в секунду (IOPS)   
#
2. Менеджер продукта посмотрев на ваши метрики сказал, что ему непонятно что такое RAM/inodes/CPUla. Также он сказал, 
что хочет понимать, насколько мы выполняем свои обязанности перед клиентами и какое качество обслуживания. Что вы 
можете ему предложить?
### Ответ 
RAM (Оперативная память) - это временное хранилище для данных и программ, которые в данный момент используются сервером. Чем больше RAM, тем больше процессов может одновременно обрабатываться, что влияет на скорость работы приложения.   
Inodes - это структуры данных в файловой системе, которые хранят информацию о файлах и каталогах. Количество inodes определяет, сколько файлов можно создать в файловой системе, и это важно для управления ресурсами.   
CPU (Центральный процессор) - это основной элемент компьютера, который исполняет команды программы. Высокая загрузка CPU может указывать на недостаточную производительность приложений или на необходимость оптимизации кода.  
Предложим добавить метрики для повышения качества и надежности:     
Время безотказной работы - это процент времени, в течение которого сервисы доступны.    
Время отклика - это среднее время, необходимое для обработки запросов пользователей.    
Также можно использовать опросы клиентов или Net Promoter Score (NPS) для оценки общего удовлетворения клиентов.    
#
3. Вашей DevOps команде в этом году не выделили финансирование на построение системы сбора логов. Разработчики в свою 
очередь хотят видеть все ошибки, которые выдают их приложения. Какое решение вы можете предпринять в этой ситуации, 
чтобы разработчики получали ошибки приложения?
### Ответ 
Можно предложить использовать встроенные средства логирования, которые обычно доступны во многих языках программирования и фреймворков.   
Например настроить логирование ошибок непосредственно в коде приложения, используя стандартные библиотеки для логирования,   
также можно делать интеграцию с электронной почтой или мессенджерами для уведомления команды о возникающих ошибках в реальном времени.   
#
4. Вы, как опытный SRE, сделали мониторинг, куда вывели отображения выполнения SLA=99% по http кодам ответов. 
Вычисляете этот параметр по следующей формуле: summ_2xx_requests/summ_all_requests. Данный параметр не поднимается выше 
70%, но при этом в вашей системе нет кодов ответа 5xx и 4xx. Где у вас ошибка?
### Ответ
Стоит учитывать запросы которые имет коды 3xx (для перенаправлений) и 1xx (для информационных ответов), потому что данные коды не являются ошибками 
то есть формула должа выглядеть следующим образом (summ_2xx_requests + summ_3xx_requests + summ_1xx_requests)/summ_all_requests
#
5. Опишите основные плюсы и минусы pull и push систем мониторинга.
### Ответ
Pull-системы мониторинга:
Плюсы:
1. Упрощение инфраструктуры: Система мониторинга запрашивает данные, что снижает требования к клиентам на стороне агентского ПО, так как они не должны постоянно отправлять информацию.
2. Контроль за частотой сбора: Серверный компонент может контролировать, когда и как часто собирать данные, что позволяет избежать перегрузки сети.
3. Надежность: В случае временной недоступности клиента, сервер все равно сможет запрашивать данные позже, когда клиент станет доступным.

Минусы:
1. Отставание данных: Из-за периодических запросов данные могут быть неактуальными, если сбор информации происходит не очень часто.
2. Привязка к времени: Если мониторинг зависит от частоты опроса, высоко динамичные системы могут оставаться незамеченными.

Push-системы мониторинга:

Плюсы:
1. Актуальность данных: Данные передаются по мере их появления, что обеспечивает получение актуальной информации о состоянии системы в реальном времени.
2. Гибкость: Клиенты могут отправлять данные по мере необходимости, позволяя адаптироваться в зависимости от состояния системы.
3. Снижение нагрузки на сервер: Уменьшается количество опросов сервера, так как данные передаются только при их изменении.

Минусы:
1. Сложности с клиентами: Требуются возможности для настройки и поддержки на стороне клиентов, что может увеличить сложность системы.
2. Потеря данных: В случае временной недоступности серверов или сетевых проблем данные могут потеряться, если клиенты не могут их отправить.
#
6. Какие из ниже перечисленных систем относятся к push модели, а какие к pull? А может есть гибридные?

    - Prometheus (Pull)
    - TICK (Push)
    - Zabbix (Push и pull в зависимости от конфигураций)
    - VictoriaMetrics (Pull)
    - Nagios (Pull)

#
7. Склонируйте себе [репозиторий](https://github.com/influxdata/sandbox/tree/master) и запустите TICK-стэк, 
используя технологии docker и docker-compose.

В виде решения на это упражнение приведите скриншот веб-интерфейса ПО chronograf (`http://localhost:8888`). 
![image](https://github.com/user-attachments/assets/6b6e39a4-e386-4e62-97b4-db7b4f16e825)

P.S.: если при запуске некоторые контейнеры будут падать с ошибкой - проставьте им режим `Z`, например
`./data:/var/lib:Z`
#
8. Перейдите в веб-интерфейс Chronograf (http://localhost:8888) и откройте вкладку Data explorer.
        
    - Нажмите на кнопку Add a query
    - Изучите вывод интерфейса и выберите БД telegraf.autogen
    - В `measurments` выберите cpu->host->telegraf-getting-started, а в `fields` выберите usage_system. Внизу появится график утилизации cpu.
    - Вверху вы можете увидеть запрос, аналогичный SQL-синтаксису. Поэкспериментируйте с запросом, попробуйте изменить группировку и интервал наблюдений.
![image](https://github.com/user-attachments/assets/05f69434-7b94-4f54-89ce-013f296db0ba)

Для выполнения задания приведите скриншот с отображением метрик утилизации cpu из веб-интерфейса.
#
9. Изучите список [telegraf inputs](https://github.com/influxdata/telegraf/tree/master/plugins/inputs). 
Добавьте в конфигурацию telegraf следующий плагин - [docker](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/docker):
![image](https://github.com/user-attachments/assets/68188bed-64e6-41bd-abff-3ead02f3eec1)

```
[[inputs.docker]]
  endpoint = "unix:///var/run/docker.sock"
```

Дополнительно вам может потребоваться донастройка контейнера telegraf в `docker-compose.yml` дополнительного volume и 
режима privileged:
```
  telegraf:
    image: telegraf:1.4.0
    privileged: true
    volumes:
      - ./etc/telegraf.conf:/etc/telegraf/telegraf.conf:Z
      - /var/run/docker.sock:/var/run/docker.sock:Z
    links:
      - influxdb
    ports:
      - "8092:8092/udp"
      - "8094:8094"
      - "8125:8125/udp"
```

После настройке перезапустите telegraf, обновите веб интерфейс и приведите скриншотом список `measurments` в 
веб-интерфейсе базы telegraf.autogen . Там должны появиться метрики, связанные с docker.

Факультативно можете изучить какие метрики собирает telegraf после выполнения данного задания.

## Дополнительное задание (со звездочкой*) - необязательно к выполнению

1. Вы устроились на работу в стартап. На данный момент у вас нет возможности развернуть полноценную систему 
мониторинга, и вы решили самостоятельно написать простой python3-скрипт для сбора основных метрик сервера. Вы, как 
опытный системный-администратор, знаете, что системная информация сервера лежит в директории `/proc`. 
Также, вы знаете, что в системе Linux есть  планировщик задач cron, который может запускать задачи по расписанию.

Суммировав все, вы спроектировали приложение, которое:
- является python3 скриптом
- собирает метрики из папки `/proc`
- складывает метрики в файл 'YY-MM-DD-awesome-monitoring.log' в директорию /var/log 
(YY - год, MM - месяц, DD - день)
- каждый сбор метрик складывается в виде json-строки, в виде:
  + timestamp (временная метка, int, unixtimestamp)
  + metric_1 (метрика 1)
  + metric_2 (метрика 2)
  
     ...
     
  + metric_N (метрика N)
  
- сбор метрик происходит каждую 1 минуту по cron-расписанию

Для успешного выполнения задания нужно привести:

а) работающий код python3-скрипта,

б) конфигурацию cron-расписания,

в) пример верно сформированного 'YY-MM-DD-awesome-monitoring.log', имеющий не менее 5 записей,

P.S.: количество собираемых метрик должно быть не менее 4-х.
P.P.S.: по желанию можно себя не ограничивать только сбором метрик из `/proc`.

2. В веб-интерфейсе откройте вкладку `Dashboards`. Попробуйте создать свой dashboard с отображением:

    - утилизации ЦПУ
    - количества использованного RAM
    - утилизации пространства на дисках
    - количество поднятых контейнеров
    - аптайм
    - ...
    - фантазируйте)
    
    ---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---

