# Словарь DevOps

Скопировано 25.11.2026 со страницы https://prostodevops.ru/glossary

## Термины

### __error__

Служебное поле, которое LogQL ставит строке, если парсер не смог её разобрать, например `JSONParserErr`. В метрических запросах такие строки отсеивают фильтром `| __error__=""`, но он прячет их молча, и число на графике может оказаться меньше настоящего.

```bash
{job="orders"} | json | __error__!=""
# только строки, которые не разобрались
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### $__rate_interval

Переменная Grafana для окна в `rate` и `increase`: подстраивается под диапазон графика и не опускается ниже четырёх интервалов сбора из `timeInterval` источника.

```bash
rate(http_requests_total[$__rate_interval])
```

Разбирается в уроке: [Дашборды в Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/dashbordy-v-grafana)

### Алерт

Сообщение о проблеме, которое мониторинг отправляет сам, без человека у дашборда. Его порождает правило в Prometheus, а доставляет Alertmanager.

Разбирается в уроке: [Алерты и Alertmanager](https://prostodevops.ru/courses/devops-bootcamp/lessons/alerty-i-alertmanager)

### Аргумент

То, что пишут после имени команды через пробел: папка, файл, текст. Параметры с дефисом, например `-r`, тоже аргументы.

```bash
cd /var/log
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### Архив

Один файл, в который упакованы папки и файлы вместе со структурой и правами. В Linux их собирает `tar`.

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)

### Атомарная операция

Действие, которое выполняется целиком или никак, без промежуточного состояния. Так работает `mv` в пределах одного диска.

Разбирается в уроке: [Работа с файлами и директориями](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-3-rabota-s-faylami-i-direktoriyami)

### Блочное устройство

Диск, раздел или флешка, которые читают и пишут блоками. В Linux они видны файлами в /dev: /dev/sda, /dev/sdb1.

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### Боевой сервер

Сервер, на котором работает настоящий сайт с покупателями. Изменения сначала пробуют на тестовом сервере.

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### Бэкап

Резервная копия файлов или данных, из которой можно всё вернуть после ошибки или поломки.

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)

### Бюджет ошибок

Допустимая доля неудач: 100% минус SLO. При SLO 99,9% за 30 дней это около 43 минут недоступности.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Временной ряд

Значения одной метрики с одним набором лейблов во времени. Каждое новое сочетание лейблов – новый ряд, который система мониторинга хранит отдельно.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Гистограмма

Тип метрики: раскладывает измерения по накопительным корзинам с границей `le`, плюс `_sum` и `_count`. Перцентиль по ним считает Prometheus.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### Домашняя папка

Личная папка пользователя, где лежат его файлы и настройки. Обозначается `~`, у пользователя student это `/home/student`.

Разбирается в уроке: [Файловая система и навигация](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-2-faylovaya-sistema-i-navigatsiya)

### Драйвер журналирования Docker

Часть Docker, которая решает, куда записать вывод контейнера. По умолчанию `json-file` – файл на хосте без ограничения размера; `local` сжимает и крутит файлы сам, `journald` пишет в журнал systemd. Умолчания задают в `/etc/docker/daemon.json`, и действуют они только на новые контейнеры.

```bash
docker inspect -f '{{.HostConfig.LogConfig.Type}}' delivery
```

Разбирается в уроке: [Логи Docker и Kubernetes](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-docker-kubernetes)

### Зависимость

Пакет, без которого другой пакет не работает. apt ставит зависимости сам, dpkg – нет.

Разбирается в уроке: [Менеджер пакетов apt и dpkg](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-menedzher-paketov-apt-dpkg)

### Источник данных Grafana

Подключение, откуда Grafana берёт значения для панелей: Prometheus, Loki, PostgreSQL. Сама Grafana метрики не хранит – она пересылает запросы панелей в источник.

Разбирается в уроке: [Дашборды в Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/dashbordy-v-grafana)

### Кардинальность

Число уникальных сочетаний лейблов у метрики – столько рядов система хранит. Растёт умножением, поэтому номер покупателя или заказа в лейбл не кладут.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Код завершения

Число, которое команда сообщает в конце работы: `0` – успех, любое другое – ошибка. Код последней команды – в `$?`.

```bash
ls /nonexistent
echo $?
# 2
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### Компактор

Компонент Loki, который уплотняет индекс и удаляет логи старше срока хранения. Удаляет только при `retention_enabled: true`: без этой строки логи живут вечно, какой срок ни напиши.

Разбирается в уроке: [Метки, кардинальность, хранение и чувствительные данные](https://prostodevops.ru/courses/devops-bootcamp/lessons/metki-kardinalnost-hranenie)

### Компонент Alloy

Блок настроек Alloy, который делает одно дело: находит файлы, читает их, обрабатывает строки или отправляет в Loki. Компоненты связывают аргументом `forward_to` – списком получателей строк; порядок блоков в файле не важен.

```bash
loki.source.file "couriers" {
  targets    = local.file_match.couriers.targets
  forward_to = [loki.write.local.receiver]
}
```

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### Конверсия

Доля откликов, после которых вас позвали на скрининг. Один скрининг на сто откликов – конверсия 1%.

Разбирается в уроке: [Как нанимают в DevOps](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-nanimayut-v-devops)

### Контейнер

Изолированная среда со своими файлами и программами, которая работает на ядре машины-хозяина. Контейнеры запускают через Docker.

Разбирается в уроке: [Docker: архитектура и принципы](https://prostodevops.ru/courses/devops-bootcamp/lessons/4-1-docker-arkhitektura-i-printsipy)

### Кусок (chunk)

Сжатая порция строк одного потока. Loki копит строки в памяти и, когда их набирается достаточно или проходит время, записывает кусок на диск или в объектное хранилище S3.

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### Лейбл

Метка «имя – значение» у метрики: уточняет, что измерено, например `status="500"`. По лейблам отбирают и группируют ряды в запросах.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Лог

Файл-журнал, куда программа записывает, что с ней происходило: запросы, ошибки, предупреждения. Обычно лежат в `/var/log`.

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### Маска, glob

Шаблон имени файла: `*` – любые символы, `?` – один символ, `[...]` – один из перечисленных. Маску раскрывает bash до запуска команды.

```bash
ls /var/log/*.log
```

Разбирается в уроке: [Работа с файлами и директориями](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-3-rabota-s-faylami-i-direktoriyami)

### Маскирование логов

Замена токенов, паролей и персональных данных заглушкой до отправки в Loki. В Alloy это `stage.replace`: он заменяет только группы захвата – части выражения в круглых скобках. Маскирование ставят первым шагом, до разбора строки.

```bash
stage.replace {
  expression = `Bearer ([A-Za-z0-9._~+/=-]+)`
  replace    = "***"
}
```

Разбирается в уроке: [Метки, кардинальность, хранение и чувствительные данные](https://prostodevops.ru/courses/devops-bootcamp/lessons/metki-kardinalnost-hranenie)

### Метка в Loki

Пара «имя – значение» у строки лога, например `job="orders"`: описывает, откуда пришла строка – сервис, сервер, окружение. То же, что лейбл у метрик Prometheus. В индекс Loki попадают только метки, поэтому их мало и значений у каждой немного.

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### Метрика

Число о работе системы, которое измеряют снова и снова: время ответа, число запросов, свободная память. Из значений во времени складывается график.

```bash
http_requests_total{method="POST", status="500"} 47
# имя, лейблы, значение
```

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Метрический запрос

Запрос LogQL, который возвращает числа, а не строки: запрос логов внутри функции с окном в квадратных скобках. Только такой запрос годится для графика и правила алерта; снаружи почти всегда ставят `sum by`, иначе ряды разойдутся по всем полям строки.

```bash
sum by (zone) (rate({job="delivery"} | logfmt | __error__="" | took > 3s [5m]))
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### Монтирование

Подключение диска или раздела к папке в общем дереве. Папку, к которой подключили, называют точкой монтирования.

```bash
df -h
# колонка Mounted on – куда подключён раздел
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### Наблюдаемость

Свойство системы отдавать о себе столько данных, чтобы ответить и на вопрос, который никто не задал заранее. Мониторинг – её часть: проверки, придуманные заранее.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Насыщение

Сколько работы ждёт в очереди к ресурсу. У процессора его видно по load average и колонке `r` в `vmstat`, у диска – по `await` в `iostat -x`.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Оболочка, bash

Программа, которая читает ваши команды в терминале и выполняет их. На серверах с Ubuntu это bash.

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### Опрос цели

Один сбор метрик: Prometheus делает GET на `/metrics` цели и записывает значения со своей отметкой времени. Как часто – задаёт `scrape_interval`.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### Отбор потоков

Обязательная первая часть запроса LogQL – условия на метки в фигурных скобках: `=`, `!=`, `=~`, `!~`. Хотя бы одно условие не должно подходить к пустому значению, поэтому `{job=~".*"}` Loki отклонит, а `{job=~".+"}` примет.

```bash
{job=~"orders|delivery", host="dostavka-app-01"}
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### Пайп

Знак `|` между командами: вывод левой команды становится входом правой.

```bash
history | grep ssh
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### Пакет

Программа, упакованная для установки через `apt`: файлы, зависимости и описание.

Разбирается в уроке: [Менеджер пакетов apt и dpkg](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-menedzher-paketov-apt-dpkg)

### Парсер LogQL

Часть запроса, которая разбирает строку на поля: `json`, `logfmt`, `pattern` для текста с постоянным порядком полей и `regexp` для остального. После парсера по полям фильтруют – `level="error"`, `took > 3s`, – а в индекс поля не попадают.

```bash
{job="delivery"} | logfmt | zone="north" and took > 3s
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### Переменная

Значение с именем, которое хранит bash. Чтобы подставить значение, перед именем ставят `$`.

```bash
echo $HOME
# /home/student
```

Разбирается в уроке: [Основы Bash-скриптинга](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-10-bash-skripting-osnovy)

### Перенаправление

Отправка вывода команды в файл вместо экрана: `>` перезаписывает файл, `>>` дописывает в конец, `2>` сохраняет ошибки.

```bash
date > today.txt
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### Перцентиль

Значение, ниже которого лежит заданная доля измерений. p99 = 3 с значит, что каждый сотый запрос длится дольше трёх секунд.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Подавление (inhibition)

Правило Alertmanager: пока горит алерт-причина, алерты-следствия с теми же значениями лейблов не отправляются.

Разбирается в уроке: [Алерты и Alertmanager](https://prostodevops.ru/courses/devops-bootcamp/lessons/alerty-i-alertmanager)

### Подстановка команды

Конструкция `$(...)`: bash выполняет команду внутри скобок и ставит её ответ на это место.

```bash
echo "Сегодня $(date +%F)"
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### Постоянный журнал

Журнал systemd на диске, в `/var/log/journal`: переживает перезагрузку. Без него журнал живёт в памяти, в `/run/log/journal`, и пропадает. Включают настройкой `Storage=persistent`, место ограничивают `SystemMaxUse=`.

```bash
# /etc/systemd/journald.conf.d/50-persistent.conf
[Journal]
Storage=persistent
SystemMaxUse=2G
```

Разбирается в уроке: [Логи Linux: journald, journalctl и logrotate](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-linux-journald)

### Поток (stream)

Все строки Loki с одинаковым сочетанием значений меток. У каждого потока своя запись в индексе, свой буфер в памяти и свои куски на диске, поэтому число потоков – главная мера нагрузки на Loki. Потоки умножаются: 3 сервиса × 4 уровня × 2 сервера – 24 потока.

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### Права доступа

Кто может читать, изменять и запускать файл: владелец, группа, все остальные.

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### Предел активных потоков

Сколько потоков Loki принимает от одного клиента, по умолчанию 5000. Сверх предела новые строки отклоняются с кодом 429 – обычно потому, что меткой сделали поле с уникальными значениями вроде `request_id`. Лечат удалением метки, а не подъёмом предела.

Разбирается в уроке: [Метки, кардинальность, хранение и чувствительные данные](https://prostodevops.ru/courses/devops-bootcamp/lessons/metki-kardinalnost-hranenie)

### Приоритет записи (PRIORITY)

Уровень важности записи в журнале systemd: от `emerg` (0) до `debug` (7), чем меньше номер, тем важнее. Строка, которую сервис просто напечатал, получает `info`, даже если в ней написано `ERROR`, поэтому ошибки приложения ищут по тексту.

```bash
journalctl -u payments -p err
# уровень err и всё, что важнее
```

Разбирается в уроке: [Логи Linux: journald, journalctl и logrotate](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-linux-journald)

### Провижининг

Настройка Grafana файлами из `/etc/grafana/provisioning/`: источники данных и дашборды создаются при запуске сами, и стенд можно пересоздать с теми же настройками.

Разбирается в уроке: [Дашборды в Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/dashbordy-v-grafana)

### Процесс

Запущенная программа. У каждого процесса свой номер, своя память и текущая папка.

Разбирается в уроке: [Процессы](https://prostodevops.ru/courses/devops-bootcamp/lessons/protsessy-i-monitoring)

### Регулярное выражение

Шаблон для поиска текста: `^ERROR` – строки, которые начинаются с ERROR, `ERROR|FATAL` – одно из двух.

```bash
grep -E "ERROR|FATAL" app.log
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### Релейблинг

Правила, которые переписывают лейблы цели или метрики: делают из служебных `__meta_` понятные, отбрасывают лишние цели и метрики.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### Репозиторий пакетов

Хранилище пакетов на серверах дистрибутива или разработчика: оттуда apt берёт программы. Адреса репозиториев записаны в /etc/apt/sources.list.

Разбирается в уроке: [Менеджер пакетов apt и dpkg](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-menedzher-paketov-apt-dpkg)

### Ротация логов

Старый лог переименовывают (app.log → app.log.1) и начинают новый, обычно раз в сутки. Этим занимается logrotate.

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### Сервис

Программа, которая работает в фоне и сама запускается после перезагрузки сервера. Ими управляет systemd.

Разбирается в уроке: [systemd](https://prostodevops.ru/courses/devops-bootcamp/lessons/systemd-osnovy)

### Скрипт

Файл с командами, которые bash выполняет по очереди. Так автоматизируют повторяющуюся работу.

Разбирается в уроке: [Основы Bash-скриптинга](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-10-bash-skripting-osnovy)

### Скрытый файл

Файл или папка, имя которых начинается с точки, например `.bashrc`. `ls` показывает их только с флагом `-a`.

```bash
ls -a ~
```

Разбирается в уроке: [Файловая система и навигация](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-2-faylovaya-sistema-i-navigatsiya)

### Срок хранения в Loki

Сколько Loki держит логи. Общий срок задаёт `retention_period`, отдельные сроки для части потоков – `retention_stream` с отбором по меткам. По умолчанию Loki не удаляет ничего, просроченное удаляет компактор.

```bash
limits_config:
  retention_period: 336h
  retention_stream:
    - selector: '{level="debug"}'
      priority: 1
      period: 72h
```

Разбирается в уроке: [Метки, кардинальность, хранение и чувствительные данные](https://prostodevops.ru/courses/devops-bootcamp/lessons/metki-kardinalnost-hranenie)

### Структурированный лог

Запись набором полей «имя – значение», обычно одной строкой JSON или в logfmt, а не фразой. Записи отбирают по полям, поэтому правка текста сообщения не ломает поиск и алерты. Имена общих полей договариваются одни на все сервисы.

```bash
{"ts":"2026-10-20T14:03:41.284Z","level":"error","service":"orders","msg":"payment gateway timeout","order_id":88140}
```

Разбирается в уроке: [Как устроены логи](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroeny-logi)

### Тенант

Отдельный клиент Loki со своими данными, правилами и пределами. Когда Loki работает для одного клиента (`auth_enabled: false`), тенант называется `fake`.

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### Типы метрик

Counter – счётчик, только растёт. Gauge – может расти и падать. Histogram – распределение по корзинам. Summary – готовые квантили из приложения.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### Тишина (silence)

Временное отключение уведомлений по лейблам на срок плановых работ. Правила продолжают вычисляться, не уходят только сообщения.

Разбирается в уроке: [Алерты и Alertmanager](https://prostodevops.ru/courses/devops-bootcamp/lessons/alerty-i-alertmanager)

### Трассировка стека (traceback)

Цепочка вызовов, на которой программа упала: в каком файле и строке случилась ошибка. В логе она занимает много строк, и только у первой есть время и уровень, поэтому её пишут одним полем JSON или склеивают при сборе.

Разбирается в уроке: [Как устроены логи](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroeny-logi)

### Трейс

Путь одного запроса через все программы с временем каждого отрезка (span). Показывает, где именно ушло время.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Удалённый открытый файл

Файл, у которого удалили имя, а процесс всё ещё держит его открытым и пишет в него. Место на диске освободится, только когда процесс файл закроет, поэтому `df` и `du` расходятся. Найти такие файлы помогает `lsof +L1`.

```bash
sudo lsof +L1
# в конце строки – пометка (deleted)
```

Разбирается в уроке: [Логи Linux: journald, journalctl и logrotate](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-linux-journald)

### Уровень логирования

Насколько важна запись: `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`. В настройке сервиса уровень работает как порог: при `INFO` записи `DEBUG` и `TRACE` не пишутся вовсе. `ERROR` – операция не выполнилась, `WARN` – сбой, с которым сервис справился сам.

Разбирается в уроке: [Как устроены логи](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroeny-logi)

### Файрвол

Набор правил, какие сетевые соединения сервер принимает, а какие отбрасывает. В Ubuntu правилами управляет команда `ufw`.

Разбирается в уроке: [Защита сервера: SSH, файрвол, обновления](https://prostodevops.ru/courses/devops-bootcamp/lessons/bazovaya-zaschita-servera-ufw-i-harding)

### Фильтр строк

Условие LogQL на текст строки: `|=` – есть подстрока, `!=` – нет, `|~` и `!~` – нашлось или нет регулярное выражение. Различает регистр, для поиска без него пишут `(?i)`. Простая подстрока проверяется быстрее регулярного выражения.

```bash
{job="delivery"} |= "timeout" != "level=debug"
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### Формат CRI

Формат строк лога контейнеров на нодах Kubernetes: время, поток (`stdout` или `stderr`), пометка `F` или `P` и текст. `P` – часть длинной строки, которую среда запуска разрезала, `F` – последняя часть; агент сбора склеивает их обратно.

```bash
2026-10-22T19:42:11.511203874Z stdout F connected to orders queue
```

Разбирается в уроке: [Логи Docker и Kubernetes](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-docker-kubernetes)

### Экспортёр

Программа, которая читает статистику системы, ничего не знающей о Prometheus, и отдаёт её в виде метрик по адресу `/metrics`. Например, `node_exporter` для Linux.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### Юнит

Файл, в котором systemd описан сервис, таймер или другой объект: что запускать, от чего это зависит и что делать при падении.

Разбирается в уроке: [systemd](https://prostodevops.ru/courses/devops-bootcamp/lessons/systemd-osnovy)

### Ядро процессора

Часть процессора, которая в каждый момент выполняет одну задачу. Чем больше ядер, тем больше задач сервер тянет одновременно.

Разбирается в уроке: [Мониторинг](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring)

### Ядро Linux

Основа системы: управляет процессором, памятью, дисками и запускает программы. Версию показывает `uname -r`.

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### Alertmanager

Программа, которая получает алерты от Prometheus, собирает их в группы, убирает повторы и отправляет уведомления нужному получателю – в чат, на почту или в веб-хук.

Разбирается в уроке: [Алерты и Alertmanager](https://prostodevops.ru/courses/devops-bootcamp/lessons/alerty-i-alertmanager)

### ATS

Система, в которой HR ведёт вакансии и кандидатов. Она сортирует и отсеивает резюме по ключевым словам ещё до того, как их увидит человек.

Разбирается в уроке: [Как написать резюме, чтобы позвали на собес](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-napisat-rezyume)

### Blackbox-проверка

Проверка сервиса снаружи, как его видит пользователь: отвечает ли, за какое время, не истёк ли сертификат. В Prometheus её делает `blackbox_exporter`.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### cAdvisor

Сборщик метрик потребления процессора, памяти и сети контейнерами. Встроен в kubelet, отдельно его не ставят.

Разбирается в уроке: [Мониторинг в Kubernetes](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-v-kubernetes)

### copytruncate

Директива logrotate: не переименовывать файл, а скопировать содержимое и обрезать оригинал до нуля. Сигнал программе не нужен, но строки, записанные между копированием и обрезкой, теряются, а программа должна писать в режиме добавления.

Разбирается в уроке: [Логи Linux: journald, journalctl и logrotate](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-linux-journald)

### DNS

Служба, которая превращает имена серверов и сайтов в IP-адреса. С неё начинается почти любое обращение по сети.

Разбирается в уроке: [DNS: записи, зоны, диагностика](https://prostodevops.ru/courses/devops-bootcamp/lessons/2-2-dns-zapisi-zony-diagnostika)

### ELK и EFK

Классическая связка для логов: Elasticsearch строит индекс по каждому слову и полю, Logstash обрабатывает строки, Kibana показывает. Ищет мгновенно по чему угодно, но требует много памяти и кластер из нескольких узлов. В EFK вместо тяжёлого Logstash – Fluentd или Fluent Bit.

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### FHS

Стандарт, по которому в Linux разложены папки: настройки в `/etc`, логи в `/var/log`, домашние папки в `/home`. Поэтому на любом сервере понятно, где что искать.

Разбирается в уроке: [Файловая система и навигация](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-2-faylovaya-sistema-i-navigatsiya)

### Fluent Bit

Лёгкий агент сбора логов на языке C, ему хватает нескольких мегабайт памяти. В Kubernetes его часто ставят DaemonSet; отправлять умеет в Elasticsearch, OpenSearch, S3 и Loki – по роли прямая альтернатива Alloy. Fluentd – его старший родственник на Ruby.

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### Grafana Alloy

Агент сбора от Grafana: ставится на каждый сервер или ноду, читает файлы, журнал systemd и вывод контейнеров, обрабатывает строки и отправляет в Loki. Собирает также метрики и трейсы; сменил Promtail.

```bash
alloy fmt /etc/alloy/config.alloy > /dev/null && echo ok
# проверить синтаксис настроек
```

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### ISO 8601 и RFC 3339

Стандарт записи времени: дата, буква `T`, время с миллисекундами и часовой пояс – `Z` для UTC или смещение вроде `+03:00`. Такое время однозначно, и строки с ним сортируются как обычный текст.

```bash
2026-10-20T14:03:41.284Z
2026-10-20T17:03:41.284+03:00
# один и тот же момент
```

Разбирается в уроке: [Как устроены логи](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroeny-logi)

### journald

Служба systemd (`systemd-journald`), которая собирает в журнал вывод сервисов из stdout и stderr, сообщения ядра и самого systemd. Хранит записи в двоичном виде с полями – юнит, процесс, уровень, загрузка, – а читают их командой `journalctl`.

Разбирается в уроке: [Логи Linux: journald, journalctl и logrotate](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-linux-journald)

### kube-state-metrics

Сервис в кластере, который читает API и превращает состояние объектов в метрики: реплики, фазы подов, перезапуски, requests и limits.

Разбирается в уроке: [Мониторинг в Kubernetes](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-v-kubernetes)

### kubectl logs --previous

Вывод предыдущего, завершённого запуска контейнера. Первое, что смотрят, когда под перезапускается по кругу: причина падения осталась в прошлом запуске. kubelet хранит только один такой запуск.

```bash
kubectl logs delivery-7d4f9c8b6d-x2ktm -n dostavka --previous
```

Разбирается в уроке: [Логи Docker и Kubernetes](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-docker-kubernetes)

### Load average

Три числа нагрузки за 1, 5 и 15 минут: сколько задач в среднем хотели работать на процессоре. Их сравнивают с числом ядер из `nproc`.

Разбирается в уроке: [Мониторинг](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring)

### logfmt

Формат лога из пар `ключ=значение` через пробел. Короче JSON и легче читается глазами, но вложенных полей в нём нет. Loki разбирает его парсером `logfmt`.

```bash
ts=2026-10-20T14:03:41.284Z level=error service=orders msg="payment gateway timeout" order_id=88140
```

Разбирается в уроке: [Как устроены логи](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroeny-logi)

### LogQL

Язык запросов Loki. Запрос начинается с отбора потоков по меткам, дальше идут фильтры строк, парсеры и условия на поля. Функции с окном превращают строки в числа для графиков и алертов.

```bash
{job="orders"} |= "88413" | json | order_id="88413"
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### Loki

Хранилище логов от создателей Grafana. Индексирует только метки, а текст строк хранит сжатыми кусками и при запросе перебирает строки в отобранных потоках. Поэтому дешевле полнотекстовых систем, но каждый запрос начинается с отбора по меткам.

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### MTTR

Mean time to recovery – среднее время от начала аварии до восстановления. Мониторинг сокращает его, потому что быстрее становится понятно, что сломалось.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### NAT

Подмена адреса на границе сети: серверы с приватными адресами выходят в интернет под одним публичным.

Разбирается в уроке: [NAT и приватные адреса](https://prostodevops.ru/courses/devops-bootcamp/lessons/nat-i-privatnye-adresa)

### NTP

Протокол, по которому серверы сверяют часы по сети точного времени. Если часы разошлись, записи разных серверов встают не по порядку даже в UTC. На Ubuntu этим занимается `systemd-timesyncd` или `chrony`.

Разбирается в уроке: [Как устроены логи](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroeny-logi)

### OpenSearch

Открытое ответвление Elasticsearch и Kibana, которое Amazon начал в 2021 году после смены лицензии Elastic. Распространяется под лицензией Apache 2.0, интерфейс называется OpenSearch Dashboards.

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### OpenTelemetry Collector

Агент сбора метрик, логов и трейсов из открытого стандарта OpenTelemetry, не привязанный к поставщику. Alloy – его сборка от Grafana с добавленными компонентами для Prometheus и Loki.

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### PATH

Переменная со списком папок через двоеточие. В этих папках bash ищет программы по имени команды.

```bash
echo $PATH
# /usr/local/bin:/usr/bin:/bin
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### postrotate

Блок правила logrotate с командами, которые выполняются после ротации. Обычно в нём посылают программе сигнал, чтобы она открыла файл лога заново: nginx для этого понимает `USR1`, многие службы – `HUP`.

```bash
postrotate
    [ -s /run/nginx.pid ] && kill -USR1 "$(cat /run/nginx.pid)"
endscript
```

Разбирается в уроке: [Логи Linux: journald, journalctl и logrotate](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-linux-journald)

### Prometheus

Программа, которая сама забирает метрики по HTTP, хранит их историю на локальном диске и отвечает на запросы на языке PromQL.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### Prometheus Operator

Программа в кластере, которая следит за объектами ServiceMonitor, PodMonitor и PrometheusRule и сама собирает из них настройку Prometheus.

Разбирается в уроке: [Мониторинг в Kubernetes](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-v-kubernetes)

### PromQL

Язык запросов Prometheus. На нём считают скорость счётчиков, доли ошибок и перцентили – и на нём же пишут панели Grafana и правила алертов.

```bash
sum(rate(http_requests_total[5m]))
```

Разбирается в уроке: [Язык запросов PromQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-promql)

### Promtail

Прежний агент сбора логов для Loki. Поддержка закончилась 2 марта 2026 года, его место занял Alloy; старые настройки переводит команда `alloy convert --source-format=promtail`.

Разбирается в уроке: [Централизованный сбор: Alloy, Loki и Grafana](https://prostodevops.ru/courses/devops-bootcamp/lessons/centralizovannyy-sbor-loki)

### Pull и push

Pull – сервер мониторинга сам по расписанию забирает метрики у целей, так работает Prometheus. Push – программа сама отправляет данные в центр.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Pushgateway

Промежуточный приёмник для коротких задач: задача перед завершением отправляет туда метрики, а Prometheus забирает их обычным опросом.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### Range vector

Ответ за интервал: в каждом ряду все значения за окно в квадратных скобках. Нарисовать его нельзя – его передают функции вроде `rate`. Ответ на момент, по одному числу в ряду, называют instant vector.

```bash
node_load1[5m]
```

Разбирается в уроке: [Язык запросов PromQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-promql)

### Recording rule

Правило Prometheus, которое считает запрос по расписанию и сохраняет результат как новую метрику. Имя – из трёх частей через двоеточие: уровень, метрика, операция.

```bash
record: instance:node_cpu_busy:ratio5m
```

Разбирается в уроке: [Язык запросов PromQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-promql)

### Request ID

Уникальный номер запроса, его ещё называют correlation ID. Выдают на входе – обычно nginx через `$request_id` – и передают между сервисами в заголовке `X-Request-Id`. Каждый сервис пишет номер в каждую запись, и поиск по нему собирает историю запроса из всех сервисов.

Разбирается в уроке: [Как устроены логи](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroeny-logi)

### Retention

Срок хранения данных в Prometheus; если не задать, 15 дней. Вместе с числом рядов определяет, сколько места займёт база.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### root

Администратор системы с полными правами. Ошибка под root стоит дороже всего, поэтому под ним без нужды не работают.

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### rsyslog

Служба, которая копирует записи журнала systemd в привычные текстовые файлы `/var/log/syslog` и `/var/log/auth.log`. На Ubuntu обычно работает рядом с journald, в Debian начиная с 12-й версии по умолчанию её нет.

Разбирается в уроке: [Логи Linux: journald, journalctl и logrotate](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-linux-journald)

### Ruler

Компонент Loki, который раз в минуту вычисляет правила алертов на LogQL и отправляет сработавшие в Alertmanager. В `expr` правила – только метрический запрос, а файл правил лежит в каталоге тенанта, например `rules/fake/`.

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### Runbook

Инструкция для дежурного: что проверить и что сделать при конкретном алерте. Ссылку на неё кладут в аннотацию runbook_url.

Разбирается в уроке: [Алерты и Alertmanager](https://prostodevops.ru/courses/devops-bootcamp/lessons/alerty-i-alertmanager)

### Service discovery

Обнаружение целей: Prometheus берёт список адресов у Kubernetes, облака, DNS или из файла, а не из вписанного руками списка.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### ServiceMonitor

Объект Prometheus Operator: какие сервисы опрашивать и по какому порту. Оператор превращает его в настройку сбора для Prometheus.

Разбирается в уроке: [Мониторинг в Kubernetes](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-v-kubernetes)

### SLI, SLO и SLA

SLI – измеримый показатель качества сервиса, SLO – цель команды по нему, SLA – договор с клиентом, где за нарушение платят.

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### SSH

Способ безопасно подключиться к удалённому серверу и работать в его терминале.

```bash
ssh student@lab
```

Разбирается в уроке: [SSH: ключи, конфиг, безопасность](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-9-ssh-klyuchi-konfig-bezopasnost)

### stdout и stderr

Два потока вывода программы: в stdout идёт результат, в stderr – сообщения об ошибках. По умолчанию оба попадают на экран.

```bash
ls /nonexistent 2> errors.txt
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### Structured metadata

Поля, которые агент прикрепляет к строке Loki отдельно от текста: request ID, trace ID, имя пода. Потоков не порождают и в индекс не попадают, а фильтровать по ним можно без парсера. Появились в Loki 3.

```bash
{job="orders"} | request_id="req-4b1e07"
```

Разбирается в уроке: [Метки, кардинальность, хранение и чувствительные данные](https://prostodevops.ru/courses/devops-bootcamp/lessons/metki-kardinalnost-hranenie)

### TSDB

База временных рядов. У Prometheus она встроенная: данные лежат на локальном диске блоками по два часа.

Разбирается в уроке: [Как устроен Prometheus](https://prostodevops.ru/courses/devops-bootcamp/lessons/kak-ustroen-prometheus)

### UTC

Всемирное время без часовых поясов. На нём работают серверы, чтобы события из разных стран стояли на одной шкале.

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

## Команды

### `absent_over_time`

Функция LogQL для алерта на молчание: возвращает ряд со значением 1, если за окно не пришло ни одной строки, и пустоту, пока строки есть. Правило `count_over_time(...) == 0` для этого не годится.

```bash
absent_over_time({job="orders"}[10m])
```

Разбирается в уроке: [Метки, кардинальность, хранение и чувствительные данные](https://prostodevops.ru/courses/devops-bootcamp/lessons/metki-kardinalnost-hranenie)

### `adduser`

Заводит пользователя в Debian и Ubuntu с вопросами: сама создаёт домашнюю папку и спрашивает пароль. Удобна, когда пользователя заводят руками.

```bash
sudo adduser andrey
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `amtool`

Утилита Alertmanager: проверяет настройку, показывает, в какой маршрут попадёт алерт с заданными лейблами, и создаёт тишину.

```bash
amtool check-config /etc/alertmanager/alertmanager.yml
amtool config routes test --config.file=/etc/alertmanager/alertmanager.yml team=backend
```

Разбирается в уроке: [Алерты и Alertmanager](https://prostodevops.ru/courses/devops-bootcamp/lessons/alerty-i-alertmanager)

### `apt`

Устанавливает, обновляет и удаляет программы в Ubuntu. Требует прав администратора.

```bash
sudo apt install nginx
```

Разбирается в уроке: [Менеджер пакетов apt и dpkg](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-menedzher-paketov-apt-dpkg)

### `apt-cache`

Показывает сведения из каталога пакетов. `apt-cache policy` – какая версия установлена, какая будет поставлена и откуда.

```bash
apt-cache policy nginx
```

Разбирается в уроке: [Менеджер пакетов apt и dpkg](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-menedzher-paketov-apt-dpkg)

### `apt-get`

То же, что apt, но с неизменным форматом команд и вывода. Его берут в скриптах.

```bash
sudo apt-get install -y nginx
```

Разбирается в уроке: [Менеджер пакетов apt и dpkg](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-menedzher-paketov-apt-dpkg)

### `apt-mark`

Замораживает пакет, чтобы `apt upgrade` его не обновлял: `hold` – заморозить, `unhold` – разморозить.

```bash
sudo apt-mark hold nginx
```

Разбирается в уроке: [Менеджер пакетов apt и dpkg](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-menedzher-paketov-apt-dpkg)

### `awk`

Делит строку на поля (`$1`, `$2`, `$NF`), отбирает строки по условию и считает. Свой разделитель задаёт `-F`.

```bash
awk '{print $1, $9}' access.log
awk -F: '{print $1, $7}' /etc/passwd
```

Разбирается в уроке: [sed и awk: правка и подсчёты](https://prostodevops.ru/courses/devops-bootcamp/lessons/sed-i-awk)

### `blkid`

Показывает UUID, метку и тип файловой системы на разделе.

```bash
sudo blkid /dev/sdb1
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `cat`

Выводит содержимое файла на экран. Для больших файлов удобнее `less`.

```bash
cat report.txt
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `cd`

Переходит в другую папку. Без аргумента – в домашнюю папку, `cd -` – в предыдущую.

```bash
cd /var/log
cd ~
```

Разбирается в уроке: [Файловая система и навигация](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-2-faylovaya-sistema-i-navigatsiya)

### `chattr`

Ставит атрибуты файла: `+i` – нельзя изменить и удалить даже root, `+a` – только дописывать.

```bash
sudo chattr +i /etc/dostavka/prod.conf
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `chgrp`

Меняет группу файла. То же умеет `chown :группа`.

```bash
sudo chgrp developers report.txt
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `chmod`

Меняет права файла или папки: цифрами (`644`, `755`) или буквами (`u+x`, `o-r`). `-R` – вместе со всем содержимым папки.

```bash
chmod 640 db.yaml
chmod u+x deploy.sh
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `chown`

Меняет владельца и группу файла: `владелец:группа`. Владельца может менять только root.

```bash
sudo chown dostavka:dostavka db.yaml
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `count_over_time`

Функция LogQL: сколько строк подошло за окно. Если строк нет совсем, возвращает не ноль, а пустой ответ, поэтому для алерта на молчание есть `absent_over_time`.

```bash
count_over_time({job="orders"} |= "panic" [5m]) > 0
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### `cp`

Копирует файл. Папку целиком копируют с параметром `-r`.

```bash
cp nginx.conf nginx.conf.bak
```

Разбирается в уроке: [Работа с файлами и директориями](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-3-rabota-s-faylami-i-direktoriyami)

### `crontab`

Работает с расписанием cron: `-e` – открыть в редакторе, `-l` – напечатать. В строке пять полей времени и команда.

```bash
crontab -l
30 2 * * * /opt/dostavka/bin/backup.sh
```

Разбирается в уроке: [Bash: надёжные скрипты и cron](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-11-bash-patterny-i-cron)

### `curl`

Отправляет запрос по адресу и печатает ответ. С `-i` показывает код ответа и заголовки, с `-v` – весь ход запроса, с `-s -o /dev/null -w "%{http_code}"` – только код ответа.

```bash
curl -i http://10.0.1.10/
curl -v -m 5 http://10.0.1.10/
curl -s -o /dev/null -w "%{http_code}\n" http://10.0.1.10/
# 200
```

Разбирается в уроке: [Диагностика сети: ping, traceroute, ss, curl](https://prostodevops.ru/courses/devops-bootcamp/lessons/diagnostika-seti)

### `cut`

Вырезает из каждой строки нужное поле. `-d` – разделитель полей, `-f` – номер поля.

```bash
cut -d' ' -f1 access.log
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `date`

Показывает дату и время. После `+` задают формат: `%F` – дата, `%H-%M` – часы и минуты.

```bash
date +%Y-%m-%d_%H-%M
# 2026-09-26_14-30
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `dd`

Копирует байты из файла или устройства в файл или устройство, не разбираясь, что внутри. Ошибка в `of=` стирает диск без вопросов.

```bash
dd if=/dev/zero of=/tmp/test.bin bs=1M count=100 status=progress
```

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)

### `df`

Показывает место на дисках целиком: сколько всего, занято и свободно на каждом разделе. `df -h` – в понятных единицах.

```bash
df -h
```

Разбирается в уроке: [Файловая система и навигация](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-2-faylovaya-sistema-i-navigatsiya)

### `diff`

Сравнивает два файла построчно и показывает, чем они отличаются.

```bash
diff old.conf new.conf
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `dig`

Задаёт вопрос серверу имён и показывает его ответ: статус, записи и кто отвечал. Файл `/etc/hosts` не читает.

```bash
dig db.dostavka.internal
dig +short db.dostavka.internal
dig -x 10.0.2.10
```

Разбирается в уроке: [DNS: записи, зоны, диагностика](https://prostodevops.ru/courses/devops-bootcamp/lessons/2-2-dns-zapisi-zony-diagnostika)

### `dpkg`

Нижний уровень работы с пакетами: ставит один файл .deb, показывает установленное (`-l`), файлы пакета (`-L`) и чей это файл (`-S`).

```bash
dpkg -S /etc/nginx/nginx.conf
# nginx: /etc/nginx/nginx.conf
```

Разбирается в уроке: [Менеджер пакетов apt и dpkg](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-menedzher-paketov-apt-dpkg)

### `du`

Считает, сколько места занимают папки и файлы. `du -sh папка` – один итог в понятных единицах.

```bash
du -sh /var/log
# 127M	/var/log
```

Разбирается в уроке: [Файловая система и навигация](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-2-faylovaya-sistema-i-navigatsiya)

### `echo`

Печатает текст, который ей передали. Переменные внутри текста bash заменяет значениями.

```bash
echo "Сервер $HOSTNAME"
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `fail2ban-client`

Управляет программой fail2ban, которая блокирует адреса за повторные неудачные попытки входа: показывает заблокированных и снимает блокировку.

```bash
sudo fail2ban-client status sshd
sudo fail2ban-client set sshd unbanip 203.0.113.7
```

Разбирается в уроке: [Защита сервера: SSH, файрвол, обновления](https://prostodevops.ru/courses/devops-bootcamp/lessons/bazovaya-zaschita-servera-ufw-i-harding)

### `fallocate`

Быстро создаёт файл нужного размера – например, под swap.

```bash
sudo fallocate -l 2G /swapfile
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `find`

Ищет файлы и папки по имени, типу, размеру и дате. Первым аргументом – где искать, дальше условия: `-name`, `-type`, `-size`, `-mtime`.

```bash
find /etc -name timezone
find /var/log -size +100M
```

Разбирается в уроке: [Файловая система и навигация](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-2-faylovaya-sistema-i-navigatsiya)

### `findmnt`

Показывает, что куда подключено, деревом. `--verify` проверяет `/etc/fstab`, ничего не подключая.

```bash
sudo findmnt --verify
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `flock`

Ставит замок на файл, чтобы работала только одна копия скрипта. `-n` – не ждать: если замок занят, сразу вернуть ошибку.

```bash
flock -n /run/lock/backup.lock /opt/dostavka/bin/backup.sh
```

Разбирается в уроке: [Bash: надёжные скрипты и cron](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-11-bash-patterny-i-cron)

### `free`

Показывает оперативную память и swap: сколько всего, занято и доступно. `-h` – в понятных единицах.

```bash
free -h
```

Разбирается в уроке: [Мониторинг](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring)

### `getcap`

Показывает capabilities, выданные программе.

```bash
getcap /usr/bin/ping
# /usr/bin/ping cap_net_raw=ep
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `getent`

Спрашивает систему тем же путём, что и программы. `getent hosts имя` показывает, в какой адрес превращается имя: сначала по файлу `/etc/hosts`, затем через службу имён.

```bash
getent hosts db.dostavka.internal
# 10.0.2.10       db.dostavka.internal
```

Разбирается в уроке: [Диагностика сети: ping, traceroute, ss, curl](https://prostodevops.ru/courses/devops-bootcamp/lessons/diagnostika-seti)

### `getfacl`

Показывает обычные права файла и его правила ACL.

```bash
getfacl api.log
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `grep`

Оставляет строки, где есть нужный текст или шаблон. `-i` – без учёта регистра, `-v` – наоборот, `-A`/`-B` – строки вокруг.

```bash
grep -B 2 -A 5 "payment failed" app.log
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `groupadd`

Заводит группу. Переименовывают группу через `groupmod -n`, удаляют – через `groupdel`.

```bash
sudo groupadd developers
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `groups`

Показывает группы, в которых состоит пользователь.

```bash
groups andrey
# andrey : andrey adm sudo
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `gzip`

Сжимает файл: из `app.log` получается `app.log.gz`. Распаковать – `gunzip`.

```bash
gzip app.log
```

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)

### `head`

Показывает начало файла, по умолчанию 10 строк. `-n 20` – двадцать.

```bash
head -n 20 app.log
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `histogram_quantile`

Функция PromQL: перцентиль по корзинам гистограммы. Корзины сначала превращают в скорость через `rate` и складывают, оставив лейбл `le`.

```bash
histogram_quantile(0.99, sum by (le) (rate(http_request_duration_seconds_bucket[5m])))
```

Разбирается в уроке: [Язык запросов PromQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-promql)

### `history`

Показывает прежние команды с номерами. `!номер` повторяет команду, Ctrl+R ищет по истории.

```bash
history
!42
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `hostname`

Выводит имя сервера. Помогает убедиться, что команда уйдёт на нужную машину.

```bash
hostname
# lab
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `htop`

То же, что `top`, но в цвете, с полосками загрузки и деревом процессов (F5).

```bash
htop
```

Разбирается в уроке: [Мониторинг](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring)

### `id`

Показывает пользователя и группы, в которых он состоит. `id -un` выводит только имя пользователя.

```bash
id -un
# student
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `increase`

Функция PromQL: прирост счётчика за всё окно – например, сколько ошибок было за час. Может вернуть дробное число: значения достраиваются до краёв окна.

```bash
increase(http_requests_total{status="500"}[1h])
```

Разбирается в уроке: [Язык запросов PromQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-promql)

### `iostat`

Нагрузка на каждый диск: операции, скорость, ожидание (`r_await`, `w_await`). Ставится пакетом `sysstat`.

```bash
iostat -xm 1
```

Разбирается в уроке: [Мониторинг](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring)

### `ip`

Показывает и меняет сетевые настройки сервера. `ip a` – адреса интерфейсов, `ip route` – таблица маршрутов, `ip -br a` – коротко, по строке на интерфейс.

```bash
ip -br a
ip route
```

Разбирается в уроке: [NAT и приватные адреса](https://prostodevops.ru/courses/devops-bootcamp/lessons/nat-i-privatnye-adresa)

### `iptables`

Показывает и меняет правила, по которым ядро пропускает или отбрасывает пакеты. Правила читаются сверху вниз до первого подходящего.

```bash
sudo iptables -L INPUT -n --line-numbers
```

Разбирается в уроке: [Файрвол: iptables и ufw](https://prostodevops.ru/courses/devops-bootcamp/lessons/2-3-fayrvol-iptables-i-ufw)

### `journalctl`

Читает журнал systemd. `-u` – логи одного сервиса, `-f` – следить за новыми строками, `--since` – с какого времени.

```bash
journalctl -u nginx --since "1 hour ago"
```

Разбирается в уроке: [systemd](https://prostodevops.ru/courses/devops-bootcamp/lessons/systemd-osnovy)

### `kill`

Отправляет сигнал процессу по номеру. Без флага – SIGTERM, просьба завершиться; `-9` – SIGKILL, немедленно.

```bash
kill 4312
kill -9 4312
```

Разбирается в уроке: [Процессы](https://prostodevops.ru/courses/devops-bootcamp/lessons/protsessy-i-monitoring)

### `killall`

Отправляет сигнал всем процессам с точно таким именем программы.

```bash
killall nginx
```

Разбирается в уроке: [Процессы](https://prostodevops.ru/courses/devops-bootcamp/lessons/protsessy-i-monitoring)

### `less`

Показывает большой файл экран за экраном: `/слово` – поиск, `G` – в конец, `q` – выйти.

```bash
less app.log
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `logcli`

Консольный клиент Loki, адрес берёт из переменной `LOKI_ADDR`. `query` возвращает строки, `instant-query` – числа, `labels` – метки, а `series --analyze-labels` – сводку: сколько значений у каждой метки.

```bash
export LOKI_ADDR=http://127.0.0.1:3100
logcli query --since=1h --limit=20 '{job="delivery"}'
logcli series '{}' --since=1h --analyze-labels
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### `logger`

Добавляет запись в системный журнал. `-t` – метка, по которой запись потом находят, `-p` – уровень.

```bash
logger -t backup "Бэкап начат"
journalctl -t backup
```

Разбирается в уроке: [Bash: надёжные скрипты и cron](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-11-bash-patterny-i-cron)

### `logrotate`

Крутит текстовые логи: раз в сутки по таймеру переименовывает файл, старые сжимает, лишние удаляет. Правила – в `/etc/logrotate.d/`. `-d` – показать, что будет сделано, ничего не трогая, `-f` – крутить сейчас.

```bash
sudo logrotate -d /etc/logrotate.d/nginx
sudo logrotate -v -f /etc/logrotate.d/nginx
```

Разбирается в уроке: [Логи Linux: journald, journalctl и logrotate](https://prostodevops.ru/courses/devops-bootcamp/lessons/logi-linux-journald)

### `ls`

Показывает список файлов в папке. `ls -l` – подробно: права, владелец, размер, дата.

```bash
ls -l /var/log
```

Разбирается в уроке: [Файловая система и навигация](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-2-faylovaya-sistema-i-navigatsiya)

### `lsattr`

Показывает атрибуты файла, которые ставит `chattr`.

```bash
lsattr /etc/dostavka/prod.conf
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `lsblk`

Показывает диски и разделы: размер и куда они подключены.

```bash
lsblk
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `lsof`

Показывает открытые файлы и программы, которые их держат. `+L1` – удалённые, но ещё открытые.

```bash
sudo lsof +L1
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `man`

Открывает полную справку по команде. Листать – стрелками, искать – `/слово`, выйти – `q`.

```bash
man date
man 5 passwd
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `mkdir`

Создаёт папку. `-p` – сразу всю цепочку папок и без ошибки, если папка уже есть.

```bash
mkdir -p ~/courier/{app,config,logs}
```

Разбирается в уроке: [Работа с файлами и директориями](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-3-rabota-s-faylami-i-direktoriyami)

### `mkfs`

Создаёт в разделе файловую систему и стирает всё, что там было. Для каждого типа своя команда: `mkfs.ext4`, `mkfs.xfs`.

```bash
sudo mkfs.ext4 -L photos /dev/sdb1
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `mkfs.ext4`

Создаёт в разделе файловую систему ext4 и стирает всё, что там было. `-L` – метка.

```bash
sudo mkfs.ext4 -L photos /dev/sdb1
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `mkfs.xfs`

Создаёт в разделе файловую систему xfs и стирает всё, что там было.

```bash
sudo mkfs.xfs /dev/sdb1
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `mkswap`

Размечает раздел или файл под swap.

```bash
sudo mkswap /swapfile
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `mktemp`

Создаёт временный файл с уникальным именем и печатает его путь; с `-d` – временную папку.

```bash
tmpdir=$(mktemp -d)
```

Разбирается в уроке: [Bash: надёжные скрипты и cron](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-11-bash-patterny-i-cron)

### `mount`

Подключает файловую систему к папке. `mount -a` – подключить всё из `/etc/fstab`.

```bash
sudo mount /dev/sdb1 /srv/photos
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `mpstat`

Загрузка каждого ядра процессора текстом. Ставится пакетом `sysstat`.

```bash
mpstat -P ALL 1
```

Разбирается в уроке: [Мониторинг](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring)

### `mtr`

Много раз подряд опрашивает каждый узел пути и считает по каждому потери и время ответа. С `-r` печатает итоговый отчёт.

```bash
mtr -rn -c 20 10.0.2.10
```

Разбирается в уроке: [Диагностика сети: ping, traceroute, ss, curl](https://prostodevops.ru/courses/devops-bootcamp/lessons/diagnostika-seti)

### `mv`

Переносит или переименовывает файл и папку. Молча перезаписывает файл с тем же именем, `-i` – спросит.

```bash
mv courier.conf.new courier.conf
```

Разбирается в уроке: [Работа с файлами и директориями](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-3-rabota-s-faylami-i-direktoriyami)

### `nc`

Открывает подключение к адресу и порту. `nc -zv -w 3 адрес порт` проверяет, доступен ли порт: `succeeded` – доступен, `refused` – отказ, `timed out` – ответа нет.

```bash
nc -zv -w 3 10.0.2.10 5432
```

Разбирается в уроке: [Диагностика сети: ping, traceroute, ss, curl](https://prostodevops.ru/courses/devops-bootcamp/lessons/diagnostika-seti)

### `ncdu`

Показывает, что занимает место, и даёт ходить по папкам стрелками.

```bash
sudo ncdu /
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `nproc`

Выводит, сколько ядер процессора доступно. С этим числом сравнивают load average.

```bash
nproc
# 4
```

Разбирается в уроке: [Мониторинг](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring)

### `passwd`

Задаёт или меняет пароль. `-l` – заблокировать вход по паролю, `-u` – разблокировать, `-S` – показать состояние.

```bash
sudo passwd andrey
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `pgrep`

Находит процессы по имени и выводит их номера. `-a` – вместе с командой, `-f` – поиск по всей строке запуска.

```bash
pgrep -a nginx
```

Разбирается в уроке: [Процессы](https://prostodevops.ru/courses/devops-bootcamp/lessons/protsessy-i-monitoring)

### `pidof`

Выводит номера процессов с точно таким именем программы.

```bash
pidof nginx
```

Разбирается в уроке: [Процессы](https://prostodevops.ru/courses/devops-bootcamp/lessons/protsessy-i-monitoring)

### `ping`

Отправляет серверу короткие запросы и ждёт ответы: показывает, доходят ли до него данные, с какой задержкой и какими потерями. Порты не проверяет.

```bash
ping -c 4 10.0.2.10
```

Разбирается в уроке: [Диагностика сети: ping, traceroute, ss, curl](https://prostodevops.ru/courses/devops-bootcamp/lessons/diagnostika-seti)

### `pkill`

Отправляет сигнал процессам по имени; `-f` – по всей строке запуска. Кого заденет, заранее покажет `pgrep -a`.

```bash
pkill -f "python manage.py"
```

Разбирается в уроке: [Процессы](https://prostodevops.ru/courses/devops-bootcamp/lessons/protsessy-i-monitoring)

### `predict_linear`

Функция PromQL: продолжает тренд ряда на заданное число секунд вперёд. Так алерт говорит «место закончится через четыре часа», а не «занято 90 %».

```bash
predict_linear(node_filesystem_avail_bytes{mountpoint="/"}[6h], 4 * 3600) < 0
```

Разбирается в уроке: [Язык запросов PromQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-promql)

### `promtool`

Утилита из поставки Prometheus: проверяет файл настройки и файлы правил до того, как Prometheus их перечитает.

```bash
promtool check config /etc/prometheus/prometheus.yml
promtool check rules /etc/prometheus/rules/infra.yml
```

Разбирается в уроке: [Алерты и Alertmanager](https://prostodevops.ru/courses/devops-bootcamp/lessons/alerty-i-alertmanager)

### `ps`

Показывает процессы. `ps aux` – все процессы сервера, `ps -eo` – свои колонки.

```bash
ps -eo pid,user,rss,cmd --sort=-rss | head
```

Разбирается в уроке: [Процессы](https://prostodevops.ru/courses/devops-bootcamp/lessons/protsessy-i-monitoring)

### `pstree`

Рисует дерево процессов: кто кого запустил. `-p` – с номерами процессов.

```bash
pstree -p
```

Разбирается в уроке: [Процессы](https://prostodevops.ru/courses/devops-bootcamp/lessons/protsessy-i-monitoring)

### `pwd`

Выводит полный путь папки, в которой вы сейчас находитесь.

```bash
pwd
# /home/student
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `quantile_over_time`

Функция LogQL: перцентиль чисел из `unwrap` за окно. Группировку `by` пишут после закрывающей скобки, а не снаружи через `sum by`: складывать перцентили бессмысленно.

```bash
quantile_over_time(0.95, {job="delivery"} | logfmt | __error__="" | unwrap duration(took) [5m]) by (zone)
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### `rate`

Функция PromQL: средний прирост счётчика в секунду за окно. Сама учитывает сброс счётчика при перезапуске. Окно – хотя бы четыре интервала сбора.

```bash
sum(rate(http_requests_total[5m]))
```

Разбирается в уроке: [Язык запросов PromQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-promql)

### `rm`

Удаляет файлы, корзины нет. `-r` – папку со всем содержимым, `-f` – без вопросов. Перед удалением по маске проверьте её через `ls`.

```bash
ls *.gz
rm *.gz
```

Разбирается в уроке: [Работа с файлами и директориями](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-3-rabota-s-faylami-i-direktoriyami)

### `rmdir`

Удаляет только пустую папку: если внутри что-то есть, откажется.

```bash
rmdir ~/courier/logs
```

Разбирается в уроке: [Работа с файлами и директориями](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-3-rabota-s-faylami-i-direktoriyami)

### `rsync`

Копирует папки и копирует только то, что изменилось. Умеет копировать на другой сервер.

```bash
rsync -av ~/courier/ /backup/courier/
```

Разбирается в уроке: [SSH: ключи, конфиг, безопасность](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-9-ssh-klyuchi-konfig-bezopasnost)

### `scp`

Копирует файлы на сервер и с сервера по SSH. Путь на сервере пишут как `сервер:путь`, папку копирует `-r`.

```bash
scp nginx.conf web:/tmp/
scp web:/var/log/nginx/error.log .
```

Разбирается в уроке: [SSH: ключи, конфиг, безопасность](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-9-ssh-klyuchi-konfig-bezopasnost)

### `sed`

Меняет текст по шаблону: `s/что/на что/` заменяет, `d` удаляет строки. С `-i` правит сам файл, `-i.bak` оставляет копию.

```bash
sed 's/80/8080/' nginx.conf
sed -i.bak 's/^timeout=.*/timeout=60/' app.conf
```

Разбирается в уроке: [sed и awk: правка и подсчёты](https://prostodevops.ru/courses/devops-bootcamp/lessons/sed-i-awk)

### `setcap`

Выдаёт программе отдельное право root – capability, – вместо всех прав root.

```bash
sudo setcap cap_net_bind_service=+ep /usr/local/bin/dostavka-api
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `setfacl`

Добавляет правила ACL – доступ для отдельного пользователя или группы поверх обычных прав. Ставится пакетом `acl`.

```bash
sudo setfacl -m u:maria:r api.log
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `sort`

Сортирует строки. `-n` – по числу, `-r` – в обратном порядке, `-h` – по размерам 1K, 2M.

```bash
sort -rn counts.txt
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `source`

Выполняет команды из файла в текущем терминале. Так применяют новые настройки bash без перезапуска.

```bash
source ~/.bashrc
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `ss`

Показывает сетевые соединения и порты. `ss -tlnp` – какие порты слушают программы на сервере и на каких адресах.

```bash
sudo ss -tlnp
```

Разбирается в уроке: [Защита сервера: SSH, файрвол, обновления](https://prostodevops.ru/courses/devops-bootcamp/lessons/bazovaya-zaschita-servera-ufw-i-harding)

### `ssh-add`

Добавляет приватный ключ в ssh-agent: парольную фразу спросит один раз. `-l` – показать ключи в агенте.

```bash
ssh-add ~/.ssh/id_ed25519
ssh-add -l
```

Разбирается в уроке: [SSH: ключи, конфиг, безопасность](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-9-ssh-klyuchi-konfig-bezopasnost)

### `ssh-copy-id`

Дописывает ваш публичный ключ в `authorized_keys` на сервере. После этого вход идёт по ключу.

```bash
ssh-copy-id andrey@web-01.dostavka.example
```

Разбирается в уроке: [SSH: ключи, конфиг, безопасность](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-9-ssh-klyuchi-konfig-bezopasnost)

### `ssh-keygen`

Создаёт пару SSH-ключей. `-t` – тип ключа, `-C` – комментарий. С `-R` удаляет запись о сервере из known_hosts.

```bash
ssh-keygen -t ed25519 -C "andrey@laptop"
```

Разбирается в уроке: [SSH: ключи, конфиг, безопасность](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-9-ssh-klyuchi-konfig-bezopasnost)

### `sshd`

Программа на сервере, которая принимает соединения по SSH. `sshd -t` проверяет настройки на ошибки, `sshd -T` печатает их так, как прочитает из всех файлов.

```bash
sudo sshd -t
sudo sshd -T | grep passwordauthentication
```

Разбирается в уроке: [Защита сервера: SSH, файрвол, обновления](https://prostodevops.ru/courses/devops-bootcamp/lessons/bazovaya-zaschita-servera-ufw-i-harding)

### `stress-ng`

Создаёт искусственную нагрузку на процессор, память или диск. Запускают только на тестовой машине.

```bash
stress-ng --cpu 4 --timeout 90s
# 4 потока нагрузки на процессор на 90 секунд
```

Разбирается в уроке: [Мониторинг и наблюдаемость](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring-i-nablyudaemost)

### `su`

Переключает на другого пользователя целиком и спрашивает его пароль. `su -` загружает его настройки, как при входе.

```bash
su - andrey
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `sudo`

Выполняет следующую за ней команду от имени root – администратора с полными правами.

```bash
sudo whoami
# root
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `swapon`

Включает swap; `--show` – какой swap включён. Выключает – `swapoff`.

```bash
sudo swapon /swapfile
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `sysctl`

Показывает и меняет настройки ядра до перезагрузки; постоянные – файлами в `/etc/sysctl.d/`.

```bash
sudo sysctl vm.swappiness=10
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `systemctl`

Управляет сервисами systemd: `start`, `stop`, `restart`, `status`; `enable` – запускать при загрузке, `daemon-reload` – перечитать юниты.

```bash
sudo systemctl enable --now nginx
```

Разбирается в уроке: [systemd](https://prostodevops.ru/courses/devops-bootcamp/lessons/systemd-osnovy)

### `systemd-analyze`

Проверки systemd: `verify` – ошибки в юните, `calendar` – когда сработает расписание, `blame` – что тормозит загрузку.

```bash
systemd-analyze calendar "Mon..Fri 09:00"
```

Разбирается в уроке: [systemd](https://prostodevops.ru/courses/devops-bootcamp/lessons/systemd-osnovy)

### `tail`

Показывает конец файла. `-f` – следить за новыми строками, `-F` – и после ротации лога.

```bash
tail -F /var/log/dostavka/app.log
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `tar`

Упаковывает папки и файлы в один архив и распаковывает обратно. Сам не сжимает: сжатие включают флагом `z` (gzip) или `J` (xz).

```bash
tar czf dostavka.tar.gz -C /opt dostavka
tar tzf dostavka.tar.gz   # что внутри
```

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)

### `tcpdump`

Показывает пакеты, проходящие через сетевой интерфейс. Запускают на сервере-получателе, чтобы увидеть, доходят ли до него пакеты.

```bash
sudo tcpdump -ni eth0 tcp port 5432
```

Разбирается в уроке: [Диагностика сети: ping, traceroute, ss, curl](https://prostodevops.ru/courses/devops-bootcamp/lessons/diagnostika-seti)

### `tee`

Пишет вход и на экран, и в файл. `-a` – дописать в конец. Через `sudo tee` пишут в файлы root.

```bash
df -h | tee disk.txt
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `timeout`

Запускает команду с пределом по времени. Не уложилась – завершает её и возвращает код 124.

```bash
timeout 30m /opt/dostavka/bin/backup.sh
```

Разбирается в уроке: [Bash: надёжные скрипты и cron](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-11-bash-patterny-i-cron)

### `tldr`

Показывает пять-десять самых частых примеров для команды – быстрее, чем полная справка.

```bash
tldr tar
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `top`

Показывает нагрузку в реальном времени: load average, процессор, память и самые загруженные процессы. `1` – по ядрам, `q` – выйти.

```bash
top
```

Разбирается в уроке: [Мониторинг](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring)

### `touch`

Создаёт пустой файл, а если файл есть – ставит ему время изменения на текущее.

```bash
touch courier.conf
```

Разбирается в уроке: [Работа с файлами и директориями](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-3-rabota-s-faylami-i-direktoriyami)

### `traceroute`

Перечисляет узлы на пути до адреса: шлюзы и самого получателя. Строка `* * *` – узел не ответил на пробу.

```bash
traceroute -n 10.0.2.10
```

Разбирается в уроке: [Диагностика сети: ping, traceroute, ss, curl](https://prostodevops.ru/courses/devops-bootcamp/lessons/diagnostika-seti)

### `trap`

Назначает обработчик: что выполнить при событии. `trap cleanup EXIT` вызовет функцию при любом завершении скрипта.

```bash
trap 'rm -rf "$tmpdir"' EXIT
```

Разбирается в уроке: [Bash: надёжные скрипты и cron](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-11-bash-patterny-i-cron)

### `tree`

Показывает папку деревом со всеми вложенными. `-L 2` – не глубже двух уровней. Часто не установлена: `sudo apt install tree`.

```bash
tree -L 2 /var
```

Разбирается в уроке: [Файловая система и навигация](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-2-faylovaya-sistema-i-navigatsiya)

### `type`

Отвечает, что такое команда: встроенная в bash или отдельная программа. С параметром `-a` показывает все варианты.

```bash
type whoami
type -a echo
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `ufw`

Управляет файрволом в Ubuntu: какие входящие соединения сервер принимает. Правило для SSH добавляют до включения.

```bash
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status verbose
```

Разбирается в уроке: [Защита сервера: SSH, файрвол, обновления](https://prostodevops.ru/courses/devops-bootcamp/lessons/bazovaya-zaschita-servera-ufw-i-harding)

### `umask`

Показывает или задаёт маску, которая выключает права у новых файлов и папок. При `022` файлы получают 644, папки – 755.

```bash
umask
# 0022
```

Разбирается в уроке: [Права доступа](https://prostodevops.ru/courses/devops-bootcamp/lessons/prava-dostupa)

### `umount`

Отключает файловую систему от папки. `target is busy` – с диском ещё работает программа.

```bash
sudo umount /srv/photos
```

Разбирается в уроке: [Диски: блочные устройства, монтирование, fstab](https://prostodevops.ru/courses/devops-bootcamp/lessons/diskovaya-podsistema-blok-ustroystva-mount-fstab)

### `uname`

Выводит сведения о системе: `-r` – версию ядра Linux, `-a` – всё сразу.

```bash
uname -r
# 5.15.0-91-generic
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `uniq`

Схлопывает одинаковые строки, которые стоят подряд, поэтому перед ним обычно `sort`. `-c` – с числом повторов.

```bash
sort ips.txt | uniq -c
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `unwrap`

Выражение LogQL: превращает значение поля в число для функций окна – `avg_over_time`, `max_over_time`, `quantile_over_time`. Значение с единицей, как `4.2s`, оборачивают в `duration(...)`, и Loki переведёт его в секунды.

```bash
avg_over_time({job="delivery"} | logfmt | __error__="" | unwrap duration(took) [5m]) by (zone)
```

Разбирается в уроке: [Язык запросов LogQL](https://prostodevops.ru/courses/devops-bootcamp/lessons/yazyk-zaprosov-logql)

### `unzip`

Распаковывает архив .zip; `-l` – только показать список файлов, `-d` – распаковать в указанную папку.

```bash
unzip -l reports.zip
```

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)

### `uptime`

Показывает, сколько сервер работает без перезагрузки, сколько пользователей подключено и нагрузку. `uptime -p` – только время работы, коротко.

```bash
uptime -p
# up 12 days, 3 hours, 4 minutes
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `useradd`

Заводит пользователя. Без флагов не создаёт домашнюю папку и ставит оболочку `/bin/sh`, поэтому её вызывают с `-m` и `-s /bin/bash`.

```bash
sudo useradd -m -s /bin/bash -G adm andrey
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `userdel`

Удаляет пользователя. С `-r` – вместе с домашней папкой, без него файлы остаются.

```bash
sudo userdel -r andrey
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `usermod`

Меняет пользователя: оболочку, домашнюю папку, группы. Добавить в группу – только с `-aG`: без `-a` список групп заменяется целиком.

```bash
sudo usermod -aG www-data andrey
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `visudo`

Правит правила sudo: не даёт двум людям править файл одновременно и проверяет его перед сохранением. `-c` – проверить все файлы.

```bash
sudo visudo -f /etc/sudoers.d/andrey
```

Разбирается в уроке: [Пользователи и группы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-6-polzovateli-gruppy-prava-dostupa)

### `vmstat`

Сводка по процессору, памяти, swap и дискам – строкой каждую секунду. Первая строка – средние с загрузки сервера.

```bash
vmstat 1 5
```

Разбирается в уроке: [Мониторинг](https://prostodevops.ru/courses/devops-bootcamp/lessons/monitoring)

### `wc`

Считает строки, слова и байты. `wc -l` – только число строк, часто в конце пайпа.

```bash
find /etc -maxdepth 1 -type f | wc -l
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `which`

Показывает, из какого файла bash запустит команду: ищет её в папках из PATH.

```bash
which whoami
# /usr/bin/whoami
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `whoami`

Выводит имя пользователя, от которого вы сейчас работаете.

```bash
whoami
# student
```

Разбирается в уроке: [Первые команды в Linux](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-1-pervye-komandy-v-linux)

### `xargs`

Превращает строки входа в аргументы другой команды.

```bash
find . -name "*.log" -print0 | xargs -0 gzip
```

Разбирается в уроке: [Чтение файлов, потоки и пайпы](https://prostodevops.ru/courses/devops-bootcamp/lessons/1-4-chtenie-faylov-potoki-i-paypy)

### `xz`

Сжимает плотнее gzip, но медленнее. Файл получает расширение `.xz`; распаковать – `unxz`.

```bash
xz -k orders.csv
```

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)

### `zcat`

Выводит сжатый файл .gz, не распаковывая его на диск. С `-f` пропускает и несжатые файлы как есть.

```bash
zcat app.log.2.gz | grep ERROR
```

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)

### `zgrep`

Ищет строки в сжатых файлах .gz, как `grep` в обычных.

```bash
zgrep "payment" app.log.*.gz
```

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)

### `zip`

Упаковывает файлы в архив .zip, который открывается в Windows и macOS без дополнительных программ.

```bash
zip -r reports.zip reports/
```

Разбирается в уроке: [Архивы, сжатие и передача файлов](https://prostodevops.ru/courses/devops-bootcamp/lessons/arkhivy-szhatie-i-peredacha-faylov)