## Домашнее задание к занятию "13.Системы мониторинга"
---
#### 1) Вас пригласили настроить мониторинг на проект. На онбординге вам рассказали, что проект представляет из себя платформу для вычислений с выдачей текстовых отчетов, которые сохраняются на диск. Взаимодействие с платформой осуществляется по протоколу http. Также вам отметили, что вычисления загружают ЦПУ. Какой минимальный набор метрик вы выведите в мониторинг и почему?

#### Ответ: 
#### - CPU usage (utilization): Позволяет отследить загрузку процессора, так как вычисления нагружают CPU. Это поможет определить моменты пиковых нагрузок и оценить производительность системы.
#### - Memory usage (RAM): Мониторинг использования памяти необходим для предотвращения утечек памяти и обеспечения стабильности работы платформы.
#### - Disk usage: Отслеживание свободного места на диске важно для сохранения текстовых отчетов.
#### - HTTP response time: Позволяет оценить скорость обработки запросов и выявить задержки.
#### - HTTP response codes: Метрика для отслеживания ошибок (4xx, 5xx) и успешных запросов (2xx), что важно для оценки доступности и качества сервиса.

---
#### 2) Менеджер продукта посмотрев на ваши метрики сказал, что ему непонятно что такое RAM/inodes/CPUla. Также он сказал, что хочет понимать, насколько мы выполняем свои обязанности перед клиентами и какое качество обслуживания. Что вы можете ему предложить?

#### Ответ: Для менеджера продукта метрики можно представить в понятной форме:
#### - "Доступность системы": процент успешных запросов (HTTP 2xx).
#### - "Время отклика": среднее время обработки HTTP-запросов.
#### - "Загрузка сервера": визуализация CPU и памяти, чтобы понять текущие ресурсы и необходимость масштабирования.
#### Создание дашбордов с графиками и цветовой кодировкой (зеленый — нормально, красный — критично) в системах мониторинга вроде Grafana.

---
#### 3) Вашей DevOps команде в этом году не выделили финансирование на построение системы сбора логов. Разработчики в свою очередь хотят видеть все ошибки, которые выдают их приложения. Какое решение вы можете предпринять в этой ситуации, чтобы разработчики получали ошибки приложения?

#### Ответ: Можно использовать существующие инструменты, например:
#### - Сохранение логов в локальные файлы: настроить приложения на запись ошибок в локальные лог-файлы.
#### - Мониторинг логов с помощью Telegraf: используя плагин inputs.tail, собирать ошибки из файлов и передавать их в центральную систему мониторинга (InfluxDB/Chronograf).
#### - Уведомления через почту или мессенджеры: например, с помощью скриптов или open-source решений.

---
#### 4) Вы, как опытный SRE, сделали мониторинг, куда вывели отображения выполнения SLA=99% по http кодам ответов. Вычисляете этот параметр по следующей формуле: summ_2xx_requests/summ_all_requests. Данный параметр не поднимается выше 70%, но при этом в вашей системе нет кодов ответа 5xx и 4xx. Где у вас ошибка?

#### Ответ: Ошибка в формуле связана с отсутствием запросов 4xx и 5xx. Это может быть из-за наличия большого количества перенаправлений (HTTP 3xx) или некорректной обработки других HTTP-кодов. Решение:
#### - Проверьте, включены ли 3xx-коды в summ_all_requests.
#### - Перепроверьте источники данных для расчета метрик.

---
#### 5) Опишите основные плюсы и минусы pull и push систем мониторинга.

#### Ответ: 
#### - Pull:
#### - Плюсы:
```
Централизованный контроль за сбором данных.
Подходит для динамических окружений.
```
#### - Минусы:
```
Требует открытых портов на наблюдаемых хостах.
Может не подойти для устройств за NAT.
```
#### - Push:
#### - Плюсы:
```
Простота настройки для устройств за NAT.
Не нужно открывать дополнительные порты.
```
#### - Минусы:
```
Может быть сложнее управлять источниками данных.
Потеря данных при недоступности сервера.
```

---
#### 6) Какие из ниже перечисленных систем относятся к push модели, а какие к pull? А может есть гибридные?

#### Ответ:
`Prometheus` Pull
`TICK` Push
`Zabbix` Гибрид
`VictoriaMetrics` Pull
`Nagios` Pull

---
#### 7) Склонируйте себе репозиторий и запустите TICK-стэк, используя технологии docker и docker-compose. В виде решения на это упражнение приведите скриншот веб-интерфейса ПО chronograf (http://localhost:8888). P.S.: если при запуске некоторые контейнеры будут падать с ошибкой - проставьте им режим Z, например ./data:/var/lib:Z

#### Ответ:
![image](https://github.com/user-attachments/assets/d2ed5f5e-9d66-49d6-9484-cd72d2d9669c)


---
#### 8) Перейдите в веб-интерфейс Chronograf (http://localhost:8888) и откройте вкладку Data explorer.

#### - Нажмите на кнопку Add a query
#### - Изучите вывод интерфейса и выберите БД telegraf.autogen
#### - В measurments выберите cpu->host->telegraf-getting-started, а в fields выберите usage_system. Внизу появится график утилизации cpu.
#### - Вверху вы можете увидеть запрос, аналогичный SQL-синтаксису. Поэкспериментируйте с запросом, попробуйте изменить группировку и интервал наблюдений.
#### Для выполнения задания приведите скриншот с отображением метрик утилизации cpu из веб-интерфейса.
![image](https://github.com/user-attachments/assets/a989b14c-5463-4793-a2ab-91819a831385)


#### 9) Изучите список telegraf inputs. Добавьте в конфигурацию telegraf следующий плагин - docker:
```
[[inputs.docker]]
  endpoint = "unix:///var/run/docker.sock"
```
#### Дополнительно вам может потребоваться донастройка контейнера telegraf в docker-compose.yml дополнительного volume и режима privileged:
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
#### После настройке перезапустите telegraf, обновите веб интерфейс и приведите скриншотом список measurments в веб-интерфейсе базы telegraf.autogen . Там должны появиться метрики, связанные с docker.
![image](https://github.com/user-attachments/assets/27f72b00-1b7b-4bee-8e8f-74d705466895)


#### Факультативно можете изучить какие метрики собирает telegraf после выполнения данного задания.
