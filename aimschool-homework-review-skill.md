---
name: "aimschool-homework-review"
description: "Проверка домашних заданий студентов на aimschool.ru с фиксацией в Google Sheets и написанием комментариев на русском языке"
---

# Скилл: проверка ДЗ на aimschool.ru

## Необходимые подключения
Перед началом работы убедись, что подключены:
1. **Claude in Chrome** — для работы с браузером (aimschool.ru)
2. **Google Drive / Google Sheets MCP** — для записи дат в таблицу учёта

## Первый запуск: получи данные от наставника
Если данные ещё не известны, спроси:
1. **Ссылка на Google Sheets** (или ID таблицы) для записи отметок
2. **Название листа** в таблице (например, «УЧЕНИКИ ФАБРИКА КЛОНОВ»)
3. **Название курса** (влияет на колонки и тон комментариев)
4. **Наставник** — мужчина или женщина? (для выбора формы: «проверил» / «проверила»)

## Маппинг колонок (Фабрика клонов, лист УЧЕНИКИ ФАБРИКА КЛОНОВ)
H=Урок 1, I=Урок 2, J=Урок 3, K=Урок 4, L=Урок 5, M=Урок 6, N=Урок 7, O=Урок 8,
P=Урок 9, Q=Урок 10, R=11, S=12, T=13, U=14, V=15, W=16, X=17,
Y=Урок 18, Z=19, AA=20, AB=21, AC=22, AD=23, AE=24, AF=25, AG=26,
AH=Урок 27, AI=Урок 28, AJ=Урок 29, AK=Урок 30

## Рабочий процесс (каждое ДЗ)

### 0. Представиться
Перед началом проверки **сообщить наставнику**:
- Имя студента
- Номер урока и курс
- Что приступаю к проверке

Пример: «Приступаю к проверке ДЗ: Вероника Желобкович, Урок 9, Фабрика клонов. Тариф Клон-Империя»

### 1. Открыть задание
- Перейти на aimschool.ru в список заявок на проверку
- Открыть карточку студента, прочитать приложенные материалы (скриншоты, ссылки, текст)

### 2. Найти описание задания
**Сначала проверить память** (`/areas/course-task-descriptions.md`):
- Если описание задания для этого урока уже сохранено — использовать его
- Если НЕ сохранено: нажать кнопку **«Действия»** в карточке задания → выбрать **«Задание и идеальный ответ»** — откроется модальное окно с текстом задания
- Прочитать текст задания из модального окна
- **Сохранить в память** (файл `/areas/course-task-descriptions.md`) под правильным разделом курса и урока — чтобы не открывать модал повторно в будущих сессиях

⚠️ **ЗАПРЕЩЕНО**: переходить по ссылке «Редактировать урок» или на страницы `/teach/control/lesson/update/...` — это страница редактирования курса, наставнику там делать нечего.

### 3. Написать 3 варианта комментария
Правила:
- Язык: **только русский**
- Тон: поддерживающий, конкретный, по делу
- Структура: что сделано хорошо → что можно улучшить (если есть) → одобрение / принятие
- Не пересказывать задание, не дублировать слова студента
- Писать **3 варианта**: 1 — деловой, 2 — поддерживающий, 3 — экспертный с подсказкой
- Обращение на «вы» (с маленькой буквы)
- Формат приветствия: **«Имя, здравствуйте! [текст]»** (сначала имя, потом запятая, потом «здравствуйте!»)
- Только короткое тире (-), никогда длинное (—)
- Комментарий — черновик для наставника; наставник сам нажимает «Принять» или «Отклонить»

#### Правила для комментариев по n8n-заданиям
Когда комментарий касается настройки нод или выражений в n8n:

- **Названия нод** — писать точно так, как они названы в процессе (воркфлоу) студента, чтобы он понимал, где именно нужно вносить изменения
- **Выражения писать без знака `=`** в начале — в визуальном интерфейсе n8n знак `=` перед выражением превращает значение в формулу, что вызовет новые ошибки вместо текста
- **Выражения писать полностью — от `{{` до `}}`** — студент будет копировать и вставлять их напрямую в ноды в визуальном интерфейсе n8n
- **Сверять названия нод**: если в эталоне нода называется иначе, чем у студента — **обязательно указать это** в комментарии, чтобы студент знал о расхождении и подставил своё название

### 4. Наставник принимает ДЗ
⚠️ **Claude НИКОГДА не нажимает «Принять», «Отклонить» или «Отправить»** — это делает наставник сам.

### 5. Записать в Google Sheets
После того как наставник сообщил «принял» (или аналог):
- ⛔ **ЗАПРЕЩЕНО открывать таблицу в той же вкладке, где открыт aimschool.ru** — использовать `tabs_create_mcp` для создания новой вкладки, открыть таблицу в ней
- Найти строку студента (по имени или поиском Ctrl+F)
- Определить нужную колонку по номеру урока (см. маппинг выше)
- Перейти в ячейку через Name Box: тройной клик по полю имени ячейки (левый верхний угол), ввести адрес (например `H354`), Enter
- Записать дату в формате `ДД.ММ.ГГГГ` (например `25.09.2026`)
- Нажать Enter для подтверждения
- **Закрыть новую вкладку** после записи, вернуться к вкладке aimschool.ru

## ЖЁСТКИЕ ЗАПРЕТЫ (нарушение недопустимо)

⛔ **ЗАПРЕЩЕНО открывать Google Sheets в той же вкладке, где открыт aimschool.ru** — всегда создавать новую вкладку через `tabs_create_mcp`, открывать таблицу там, после записи закрывать вкладку.

⛔ **ЗАПРЕЩЕНО редактировать строки 1, 2 и 3** в любом листе Google Sheets — это строки с заголовками и служебными данными. Запись дат производится ТОЛЬКО начиная со строки 4 и ниже.

⛔ **ЗАПРЕЩЕНО** переходить по ссылке «Редактировать урок» или на страницы `/teach/control/lesson/update/...` на aimschool.ru.

⛔ **ЗАПРЕЩЕНО** нажимать «Принять», «Отклонить» или «Отправить» на aimschool.ru — только наставник.

## Известные проблемы и решения

### Чёрный экран в Sheets (активный фильтр)
Данные → Удалить фильтр. Меню «Данные» находится примерно на x=320 в верхней панели.

### Name Box не принимает адрес ячейки
Если выделена целая строка («354:354»), одиночный клик не помогает.
Решение: **тройной клик** по Name Box → вся строка выделяется → ввести адрес → Enter.

### Случайное открытие меню / диалогов
Если открылся диалог (печать, ярлык и т.п.) — нажать Escape и попробовать снова с более точными координатами.

### Поиск Ctrl+F не находит имя (0 из 0)
Причина: активный фильтр. Решение: Данные → Удалить фильтр, затем повторить поиск.

## Формат отчёта наставнику
После каждого ДЗ кратко сообщить:
- Имя студента и номер урока
- Черновик комментария (для вставки в поле ответа)
- Подтверждение записи в таблицу (после сигнала наставника)

---

## ЭТАЛОНЫ воркфлоуов (n8n)

### Фабрика клонов — Урок 2 (Клон-Система)

**Структура воркфлоу (3 ноды):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `When chat message received` | Chat Trigger | Точка входа - триггер чата |
| `AI Agent` | LangChain Agent (typeVersion 3.1) | systemMessage: «Ты куратор мужчина курса Фабрика клонов, который посвящен автоматизации n8n, поприветствуй ученика и дай напутствие в дружелюбном тоне на настрой к изучению материалов.» |
| `OpenAI Chat Model` | LangChain OpenAI Chat (typeVersion 1.3) | Модель: gpt-5-mini, кредиты: AITunel (или аналог) |

**Связи:**
- `When chat message received` → `AI Agent` (тип: main)
- `OpenAI Chat Model` → `AI Agent` (тип: ai_languageModel)

**Что проверять у студента:**
1. Есть ли триггер чата (нода типа Chat Trigger; имя может отличаться)
2. Нода с языковой моделью подключена к AI Agent через **ai_languageModel**
3. В AI Agent есть **системный промпт** с ролью куратора и упоминанием курса
4. Подключены **кредиты** в ноде с моделью

**Типичные ошибки:**
- Нода с моделью отсутствует или не подключена к AI Agent
- Нет системного промпта - агент не знает свою роль
- Не подключены кредиты
- Связь между нодами неверного типа
- Нода AI Agent не получает сообщение от триггера

---

### Фабрика клонов — Урок 5 (Клон-Империя)

**Структура воркфлоу (3 рабочих ноды + Sticky Note):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Telegram Trigger` | Telegram Trigger (typeVersion 1.2) | updates: message; кредиты: Telegram bot |
| `OpenWeatherMap` | OpenWeatherMap (typeVersion 1) | cityName: taganrog, language: ru; кредиты: OpenWeatherMap |
| `Send a text message` | Telegram (typeVersion 1.2) | chatId, text с прогнозом; кредиты: Telegram bot |

**Связи:**
- `Telegram Trigger` → `OpenWeatherMap` (тип: main)
- `OpenWeatherMap` → `Send a text message` (тип: main)

**Текст сообщения эталон** (поле text в `Send a text message`):
```
Привет, твой прогноз на сегодня: {{ $now.format('dd-MM-yyyy') }} в {{ $json.name }}
Прогноз: {{ $json.weather[0].description }}
Температура: {{ $json.main.temp }}  С
Ощущается как: {{ $json.main.feels_like }} С
Ветер: {{ $json.wind.speed }} м/с
```

**chatId в эталоне:**
`{{ $('НАЗВАНИЕ_ТРИГГЕРА').item.json.message.chat.id }}`
(в эталоне: `Telegram Trigger` - у студента будет стоять его название ноды)

**Что проверять у студента:**
1. Триггер - Telegram Trigger с events: message, кредиты подключены
2. Нода OpenWeatherMap с кредитами; город и язык могут отличаться - это нормально
3. Нода отправки сообщения - те же кредиты Telegram
4. **chatId**: выражение содержит имя ноды-триггера студента - проверить совпадение с фактическим названием ноды
5. **Текст сообщения** содержит все поля: дата, город, описание погоды, температура, ощущаемая, ветер

**Типичные ошибки:**
- Не подключены кредиты в OpenWeatherMap или Telegram
- В `Send a text message` не заполнен chatId (не берётся ID чата из триггера)
- Имя ноды-триггера в выражении chatId не совпадает с фактическим названием ноды
- Отсутствуют поля в тексте (например, температура или ветер не передаются)
- Неправильный порядок нод: OpenWeatherMap стоит перед Telegram Trigger

---

### Фабрика клонов — Урок 7 (Клон-Система)

**Тема:** ТГ-бот для конкретного бизнеса (пример эталона — автосервис СТО) с Redis-памятью и fallback-веткой при ошибке.

**Структура воркфлоу (7 нод):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Telegram Trigger` | telegramTrigger v1.2 | updates: message; кредиты: Telegram bot |
| `Edit Fields` | set v3.4 | поля: tg_id, username, message.text, now_iso, now_human |
| `AI Agent` | langchain.agent v3.1 | systemMessage: роль в конкретном бизнесе студента; onError: continueErrorOutput |
| `OpenAI Chat Model` | lmChatOpenAi v1.3 | model: gpt-4o; кредиты: AITunel |
| `Redis Chat Memory` | memoryRedisChat v1.5 | sessionKey: `{{ "tg:" + $('Telegram Trigger').item.json.message.from.id }}`; TTL: 604800; contextWindow: 50 |
| `Send a text message` | telegram v1.2 | success-ветка; text: `{{ $json.output }}`; chatId из Telegram Trigger |
| `Send a text message1` | telegram v1.2 | fallback/error-ветка; текст заглушки об ошибке |

**Связи:**
- `Telegram Trigger` → `Edit Fields` → `AI Agent` (main)
- `AI Agent` output[0] → `Send a text message` (success)
- `AI Agent` output[1] → `Send a text message1` (error/fallback)
- `OpenAI Chat Model` → `AI Agent` (ai_languageModel)
- `Redis Chat Memory` → `AI Agent` (ai_memory)

**chatId в обеих нодах отправки:**
`{{ $('Telegram Trigger').item.json.message.chat.id }}`
(имя ноды должно совпадать с фактическим именем триггера у студента)

**Что проверять у студента:**
1. Нода `Edit Fields` присутствует и извлекает поля: tg_id, username, message.text и временны́е метки
2. AI Agent имеет **системный промпт** с описанием роли в **конкретном бизнесе студента** (не скопирован пример СТО из урока)
3. AI Agent настроен на **onError: continueErrorOutput** — иначе fallback-ветка не работает
4. `Redis Chat Memory` подключена к AI Agent через **ai_memory**; sessionKey содержит tg_id пользователя
5. TTL в Redis задан (рекомендуется 604800 = 7 дней), contextWindow задан
6. Два узла отправки сообщений: один для нормального ответа (`$json.output`), другой для ошибок
7. `chatId` в обеих нодах берётся из `Telegram Trigger` — имя ноды в выражении должно совпадать с фактическим

**Типичные ошибки:**
- Нет ноды `Edit Fields` — поля tg_id и временны́е метки не извлекаются
- `Redis Chat Memory` отсутствует или не подключена — бот не помнит контекст диалога
- `onError` на AI Agent не выставлен — нет fallback-ветки при ошибке LLM
- sessionKey не содержит tg_id пользователя — все пользователи пишут в одну «память»
- `chatId` содержит имя ноды из эталона («Telegram Trigger»), а не фактическое имя ноды студента
- Системный промпт скопирован из примера (СТО/автосервис) без адаптации под свою нишу
- Одна нода отправки вместо двух — нет обработки ошибок

---

### Фабрика клонов — Урок 8 (Клон-Система)

**Тема:** Google Sheets Trigger — отслеживание изменений в таблице по столбцу tg_id; студент показывает OUTPUT в формате Table.

**Структура воркфлоу (1 нода):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Google Sheets Trigger` | googleSheetsTrigger v1 | pollTimes: everyMinute; documentId: таблица n8n order1; sheetName: inbox (gid=0); columnsToWatch: ["tg_id"]; кредиты: Google Sheets01 (OAuth2) |

**Связи:** нет (одиночный триггер)

**Параметры эталона:**
- documentId: `1bA-O1zwY6U7xmDYO5W0ipe_Sk1tq_8XtwaS9wQnoIv8` (таблица «n8n order1»)
- sheetName: `inbox` (gid=0)
- columnsToWatch: `["tg_id"]` — триггер срабатывает при появлении нового значения в столбце tg_id
- pollTimes: `everyMinute`
- credentials: Google Sheets OAuth2 (у студента может быть другое название)

**Что проверять у студента:**
1. Нода типа Google Sheets Trigger присутствует
2. Подключена Google-таблица (любая — студент может использовать свою)
3. Указан лист (sheetName)
4. Заполнен параметр columnsToWatch (хотя бы один столбец)
5. Подключены кредиты (Google Sheets OAuth2)
6. **Студент прислал скриншот OUTPUT** в формате Table — это обязательное условие задания

**Типичные ошибки:**
- Не выбрана таблица или лист
- Не заполнен columnsToWatch — триггер не знает, за каким столбцом следить
- Не подключены кредиты
- Студент прислал скриншот не в формате Table (а JSON или другой)
- Нет скриншота OUTPUT вообще

---

### Фабрика клонов — Урок 9 (Клон-Система)

**Тема:** ТГ-бот с Redis-памятью + CRM-логика: каждый диалог сохраняется в Google Sheets (новый пользователь — append, повторный — update с накоплением истории).

**Структура воркфлоу (11 нод):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Telegram Trigger` | telegramTrigger v1.2 | updates: message |
| `Edit Fields` | set v3.4 | tg_id, username, message.text, now_human, now_iso |
| `AI Agent` | langchain.agent v3.1 | systemMessage: роль в конкретном бизнесе; onError: continueErrorOutput |
| `OpenAI Chat Model` | lmChatOpenAi v1.3 | model: gpt-4o; responsesApiEnabled: false |
| `Redis Chat Memory` | memoryRedisChat v1.5 | sessionKey: `{{ "tg:" + $('Telegram Trigger').item.json.message.from.id }}`; TTL: 604800; contextWindow: 50 |
| `Send a text message` | telegram v1.2 | success; text: `{{ $json.output }}` |
| `Send a text message1` | telegram v1.2 | error; text: `{{ $json.error }}` (реальный текст ошибки) |
| `Edit Fields1` | set v3.4 | собирает: output, username, tg_id, message.text, messege.time, now_human |
| `Get row(s) in sheet` | googleSheets v4.7 | read; фильтр по tg_id; returnFirstMatch: true |
| `If` | if v2.3 | условие: `$json.row_number` exists |
| `Update row in sheet` | googleSheets v4.7 | update; matchBy: tg_id; поле dialog накапливает историю |
| `Append row in sheet` | googleSheets v4.7 | append; новая строка для нового пользователя |

**Связи:**
- `Telegram Trigger` → `Edit Fields` → `AI Agent`
- `AI Agent` output[0] → `Send a text message` + `Edit Fields1` (параллельно)
- `AI Agent` output[1] → `Send a text message1` (error)
- `OpenAI Chat Model` → `AI Agent` (ai_languageModel)
- `Redis Chat Memory` → `AI Agent` (ai_memory)
- `Edit Fields1` → `Get row(s) in sheet` → `If`
- `If` true → `Update row in sheet`; `If` false → `Append row in sheet`

**Google Sheets в эталоне:**
- documentId: `1bA-O1zwY6U7xmDYO5W0ipe_Sk1tq_8XtwaS9wQnoIv8` (n8n order1)
- sheetName: inbox (gid=0); credentials: Google Sheets account 283 (у студента — своя)

**Накопление истории диалога (поле `dialog`) в Update и Append:**
```
($items("Get row(s) in sheet")[0]?.json?.dialog
  ? $items("Get row(s) in sheet")[0].json.dialog + "\n"
  : "")
+ $now.setLocale('ru').toFormat('dd.LL.yyyy HH:mm')
+ " | user: " + $node["Telegram Trigger"].json.message.text
+ "\n"
+ $now.setLocale('ru').toFormat('dd.LL.yyyy HH:mm')
+ " | bot: " + $node["AI Agent"].json.output
```

**Что проверять у студента:**
1. `Edit Fields` присутствует: tg_id, username, message.text, временны́е метки
2. AI Agent имеет системный промпт для своего бизнеса (не скопирован пример СТО); onError: continueErrorOutput
3. `Redis Chat Memory` подключена через ai_memory; sessionKey содержит tg_id
4. Два узла отправки: success (`$json.output`) и error (`$json.error`)
5. `Edit Fields1` присутствует после AI Agent и собирает данные для записи в Sheets
6. `Get row(s) in sheet` ищет пользователя по tg_id
7. `If` проверяет row_number на существование
8. `Update row` и `Append row` присутствуют; поле dialog накапливает историю (не перезаписывает)

**Типичные ошибки:**
- Нет `Edit Fields1` — данные не собираются для записи в Sheets
- Нет `Get row(s) in sheet` или `If` — нет разветвления new/repeat
- `If` проверяет не тот столбец (нужен row_number)
- Поле `dialog` перезаписывается вместо накопления (нет конкатенации с предыдущим значением)
- Имя ноды триггера в chatId или sessionKey не совпадает с фактическим
- Системный промпт скопирован из примера без адаптации
- `Send a text message1` выводит заглушку вместо `$json.error`

---

### Фабрика клонов — Урок 11 (Клон-Империя)

**Тема:** Пакетное обогащение данных пользователей: для каждой записи в Airtable запрашивается REST Countries API по стране пользователя, затем запись обновляется полями region и subregion.

**Структура воркфлоу (4 ноды):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `When clicking 'Execute workflow'` | manualTrigger v1 | ручной запуск |
| `Search records` | airtable v2.1 | operation: search; base: Untitled Base; table: Users; credentials: Airtable Personal Access Token |
| `HTTP Request` | httpRequest v4.3 | URL: `https://api.restcountries.com/countries/v5/names.common/{{ $('Search records').item.json.userCountry }}`; auth: httpBearerAuth; query: response_fields=names.common,region,subregion; credentials: REST Countries |
| `Update record` | airtable v2.1 | operation: update; matchingColumns: customerID; обновляет: region, subregion |

**Связи:**
- `When clicking 'Execute workflow'` → `Search records` → `HTTP Request` → `Update record`

**Ключевые выражения:**
- URL в HTTP Request: `https://api.restcountries.com/countries/v5/names.common/{{ $('Search records').item.json.userCountry }}`
- region в Update record: `{{ $json.data.objects[0].region }}`
- subregion в Update record: `{{ $json.data.objects[0].subregion }}`
- customerID в Update record: `{{ $('Search records').item.json['﻿customerID'] }}` (⚠️ BOM-символ перед именем поля)

**Что проверять у студента:**
1. Manual Trigger присутствует как точка входа
2. `Search records` подключён к Airtable (своя база и таблица — нормально)
3. `HTTP Request` использует Bearer-авторизацию (httpBearerAuth) для REST Countries API
4. URL содержит выражение с `userCountry` из `Search records`
5. Query param `response_fields` задан (хотя бы names.common, region, subregion)
6. `Update record` обновляет нужные поля: region и subregion из ответа API
7. matchingColumns в Update указывает на уникальный идентификатор (customerID или аналог)
8. Кредиты подключены в обеих нодах: Airtable (Personal Access Token) и HTTP Request (Bearer)

**Типичные ошибки:**
- Нет авторизации в HTTP Request (не выбран тип auth)
- URL не содержит динамическое поле страны (захардкожена страна)
- Неправильный путь к данным из ответа API (не `$json.data.objects[0].region`)
- `Update record` не настроен на matchingColumns — запись не находится
- Не подключены кредиты Airtable или REST Countries
- Поля region/subregion не добавлены в маппинг Update record

---

### Фабрика клонов — Урок 12.1 (NanaBanana — Генерация изображений)

**Тема:** Генерация изображения через kie.ai API (модель gpt-image) с паттерном polling: создание задачи → проверка статуса в цикле → скачивание результата.

**Структура воркфлоу (9 нод):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `When clicking 'Execute workflow'` | manualTrigger v1 | ручной запуск |
| `Set prompt1` | set v3.4 | prompt: текст запроса для генерации |
| `HTTP Request` | httpRequest v4.3 | POST createTask; модель: gpt-image/1.5-text-to-image |
| `is Success` | if v2.3 | условие: `$json.msg` == "success" |
| `HTTP Request1` | httpRequest v4.3 | GET recordInfo; taskId из `$('HTTP Request').item.json.data.taskId` |
| `Switch` | switch v3.4 | маршрутизация по `$json.data.state`: success / fail / waiting |
| `HTTP Request2` | httpRequest v4.3 | GET скачивание результата по URL из resultUrls[0] |
| `Stop and Error` | stopAndError v1 | ошибка создания задачи (is Success == false) |
| `Stop and Error1` | stopAndError v1 | ошибка генерации (Switch → fail) |
| `Wait` | wait v1.1 | пауза 30 секунд перед повторным опросом |

**Связи:**
- `When clicking 'Execute workflow'` → `Set prompt1` → `HTTP Request` → `is Success`
- `is Success` true → `HTTP Request1` → `Switch`
- `is Success` false → `Stop and Error`
- `Switch` success → `HTTP Request2`
- `Switch` fail → `Stop and Error1`
- `Switch` fallback (waiting/queuing/generation) → `Wait` → `HTTP Request1` (цикл polling)

**Ключевые параметры HTTP Request (POST createTask):**
```json
{
  "model": "gpt-image/1.5-text-to-image",
  "input": {
    "prompt": "{{ $json.prompt }}",
    "aspect_ratio": "2:3",
    "quality": "medium"
  }
}
```
- Авторизация: httpBearerAuth; кредиты: «Bearer GPT image»

**HTTP Request1 (GET recordInfo):**
- URL: `https://api.kie.ai/api/v1/jobs/recordInfo`
- Query param: `taskId = {{ $('HTTP Request').item.json.data.taskId }}`
- ⚠️ taskId берётся через прямую ссылку на ноду `HTTP Request`, не из текущего `$json`

**Switch условия:**
- output "success": `$json.data.state` == "success"
- output "fail": `$json.data.state` == "fail"
- fallbackOutput: "waiting | queuing | generation" (все остальные состояния)

**HTTP Request2 (скачивание):**
- URL: `{{ JSON.parse($json.data.resultJson).resultUrls[0] }}`

**Что проверять у студента:**
1. Manual Trigger как точка входа
2. Нода Set с промптом — задаёт текст для генерации
3. POST запрос к `createTask` с правильным телом (model, prompt, aspect_ratio, quality)
4. Нода `if` проверяет `$json.msg` == "success" (не `$json.data.state`)
5. GET запрос к `recordInfo` с taskId из ответа createTask
6. Switch с тремя ветками: success / fail / waiting (fallback)
7. Wait настроен (рекомендуется 20-30 сек); петля ведёт обратно к recordInfo
8. Скачивание результата: URL из `JSON.parse($json.data.resultJson).resultUrls[0]`
9. Кредиты Bearer подключены в нодах createTask и recordInfo

**Типичные ошибки:**
- Перепутаны условия: `$json.msg` (для createTask) и `$json.data.state` (для recordInfo)
- taskId в recordInfo берётся из `$json.data.taskId` (текущий) вместо ссылки на ноду createTask
- Wait не подключён обратно в цикл (нет петли polling)
- Switch не настроен на fallback — воркфлоу зависает без обработки состояния «в очереди»
- URL скачивания не парсит JSON из resultJson
- Нет обработки ошибки (Stop and Error) при неудачном createTask

---

### Фабрика клонов — Урок 12.2 (Sora/Grok — Генерация видео)

**Тема:** Генерация видео через kie.ai API (модель grok-imagine/text-to-video) с веб-формой, LLM-улучшением промпта и паттерном polling.

**Структура воркфлоу (13 нод):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Video input Form` | formTrigger v2.4 | веб-форма с полями ввода |
| `Input Mode Router` | switch v3.4 | маршрут по наличию изображения |
| `Prompt Refiner` | chainLlm v1.8 | LLM-улучшение промпта; требует JSON-ответ |
| `Refiner Model` | lmChatOpenAi v1.3 | модель claude-haiku-4.5; кредиты AITunel |
| `JSON Output Parser` | outputParserStructured v1.3 | схема: prompt, aspect_ratio, duration |
| `Text-to-Video Call` | httpRequest v4.3 | POST createTask; модель grok-imagine/text-to-video |
| `If` | if v2.3 | `$json.msg` == "success" |
| `Status Check` | httpRequest v4.3 | GET recordInfo; taskId из `$json.data.taskId` |
| `Status Router` | switch v3.4 | маршрут по `$json.data.state` |
| `HTTP Request` | httpRequest v4.4 | GET скачивание видео |
| `Form` | form v2.5 | completion; показывает HTML-тег video |
| `Stop and Error` | stopAndError v1 | ошибка createTask: `$json.msg` |
| `Stop and Error1` | stopAndError v1 | ошибка генерации: `$json.data.failMsg` |
| `Wait` | wait v1.1 | пауза 70 секунд |

**Связи:**
- `Video input Form` → `Input Mode Router`
- `Input Mode Router` output[0] (Image to Video) → не подключен в эталоне
- `Input Mode Router` output[1] (Text to Video) → `Prompt Refiner`
- `Refiner Model` → `Prompt Refiner` (ai_languageModel)
- `JSON Output Parser` → `Prompt Refiner` (ai_outputParser)
- `Prompt Refiner` → `Text-to-Video Call` → `If`
- `If` true → `Status Check` → `Status Router`
- `If` false → `Stop and Error`
- `Status Router` success → `HTTP Request` → `Form`
- `Status Router` fail → `Stop and Error1`
- `Status Router` fallback (waiting) → `Wait` → `Status Check` (цикл polling)

**Форма (`Video input Form`):**
- Промпт (text)
- Aspect Ratio (dropdown: 9:16 / 16:9)
- Модель (checkbox: Sora-2 / Sora-Pro; limitSelection: exact; required)
- Длина (checkbox: 10s / 15s; limitSelection: exact; required)
- Изображение (file: .jpg/.jpeg/.png; multipleFiles: false)

**Input Mode Router (switch):**
- output[0] "Image to Video": `$json['Изображение']` notEmpty
- output[1] "Text to Video": `$json['Изображение']` empty

**Prompt Refiner (chainLlm v1.8):**
- text: `User Query: {{ $json['Промпт'] }}\nAspect Ratio: {{ $json['Aspect Ratio'] }}\nLength: {{ $json['Длина'] }}`
- systemMessage: инструкция переводить и улучшать промпт как Grok, вернуть JSON без лишнего текста
- hasOutputParser: true (подключён JSON Output Parser)

**JSON Output Parser схема:**
- prompt: string (minLength: 50, maxLength: 4000)
- aspect_ratio: enum ["landscape", "portrait"]
- duration: enum ["10", "15"] (строка, не число)

**Text-to-Video Call (POST createTask):**
```json
{
  "model": "grok-imagine/text-to-video",
  "input": {
    "prompt": "{{ $json.output.prompt }}",
    "aspect_ratio": "2:3",
    "duration": "{{ $json.output.duration }}",
    "resolution": "480p"
  }
}
```
- Авторизация: httpBearerAuth; кредиты: «Bearer GPT image»

**Status Check (GET recordInfo):**
- taskId: `={{ $json.data.taskId }}` (из текущего `$json` — ответ createTask прошёл через If без изменений)

**Status Router условия:**
- output "Sucsess" (опечатка в эталоне): `$json.data.state` == "success"
- output "fail": `$json.data.state` == "fail"
- fallbackOutput: "waiting | queuing | generating"

**Form (completion):**
```html
<video width="600" controls>
  <source src="{{ JSON.parse($json.data.resultJson).resultUrls[0] }}" type="video/mp4">
  Your browser does not support the video tag.
</video>
```

**Что проверять у студента:**
1. formTrigger с нужными полями (Промпт, Aspect Ratio, Модель, Длина, Изображение)
2. Switch по наличию изображения (Image to Video / Text to Video)
3. Цепочка LLM: chainLlm + модель (ai_languageModel) + outputParserStructured (ai_outputParser)
4. LLM возвращает JSON с prompt, aspect_ratio, duration — парсер должен быть подключён
5. POST к createTask с `grok-imagine/text-to-video`, prompt и duration из `$json.output.*`
6. `If` проверяет `$json.msg` == "success"
7. GET recordInfo с taskId; петля Wait → Status Check при ожидании
8. Status Router с тремя ветками (success / fail / waiting)
9. Form completion показывает видео через HTML video-тег
10. Кредиты Bearer подключены в нодах createTask и recordInfo

**Типичные ошибки:**
- Нет LLM-рефайнера — промпт идёт без перевода и улучшения
- JSON Output Parser не подключён — LLM возвращает текст вместо структуры
- Перепутаны `$json.msg` (createTask) и `$json.data.state` (recordInfo)
- duration передаётся как число, а не строка (должно быть "10" или "15")
- Нет Form completion — результат не отображается пользователю
- Wait не зациклен обратно к Status Check
- Image to Video ветка не реализована (в эталоне тоже не подключена — это нормально для базового варианта)

---

### Фабрика клонов — Урок 13.1 (Авто-новостной Telegram-канал)

**Тема:** Автоматизированный новостной канал: по расписанию ищет актуальные новости через Tavily, фильтрует по релевантности, извлекает полный текст, формирует AI-пост и отправляет в Telegram.

**Структура воркфлоу (13 нод):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Schedule Trigger` | scheduleTrigger v1.3 | triggerAtHour: 9 |
| `Edit Fields` | set v3.4 | Prompt: тема канала (пример: "бАНКРОТСТВО ФИЗ ЛИЦ") |
| `HTTP Request` | httpRequest v4.3 | POST `https://api.tavily.com/search`; Bearer «Taveli 02»; query, search_depth=advanced, max_results=10, time_range=week, country=russia |
| `Split Out` | splitOut v1 | fieldToSplitOut: results |
| `Filter` | filter v2.3 | `$json.score` > 0.7 |
| `Aggregate` | aggregate v1 | поле: url |
| `HTTP Request1` | httpRequest v4.3 | POST `https://api.tavily.com/extract`; тело: `{"urls": {{ $json.url.toJsonString() }}, "extract_depth": "advanced"}`; Bearer «Taveli 02» |
| `Split Out1` | splitOut v1 | fieldToSplitOut: results |
| `Summarize` | summarize v1.1 | concatenate row_content; customSeparator: "/n/n NEXT ARTICLE: /n" |
| `AI Agent` | langchain.agent v3.1 | promptType: define; systemMessage: роль редактора ТГ-канала по теме; returnIntermediateSteps: true |
| `OpenAI Chat Model` | lmChatOpenAi v1.3 | model: gpt-4o-mini; кредиты: AITunel |
| `Edit Fields1` | set v3.4 | очистка think-тегов: `={{ $json.output.replace(/<think>[\s\S]*?<\/think>\s*/g, '').trim() }}` |
| `Send a text message` | telegram v1.2 | chatId: ID канала; text: `={{ $json.output }}`; appendAttribution: false |

**Связи:**
- `Schedule Trigger` → `Edit Fields` → `HTTP Request` → `Split Out` → `Filter` → `Aggregate` → `HTTP Request1` → `Split Out1` → `Summarize` → `AI Agent` → `Edit Fields1` → `Send a text message`
- `OpenAI Chat Model` → `AI Agent` (ai_languageModel)

**HTTP Request (POST /search):**
```json
{
  "query": "{{ $json.Prompt }}",
  "search_depth": "advanced",
  "max_results": 10,
  "time_range": "week",
  "country": "russia"
}
```
- Авторизация: httpBearerAuth; тип: Bearer

**HTTP Request1 (POST /extract):**
```json
{
  "urls": {{ $json.url.toJsonString() }},
  "extract_depth": "advanced"
}
```
- ⚠️ `$json.url` — массив URL из ноды Aggregate; `.toJsonString()` преобразует в JSON-строку для вставки в тело

**Summarize:**
- aggregation: concatenate
- field: row_content
- customSeparator: "/n/n NEXT ARTICLE: /n" (нестандартные символы — так в эталоне)

**AI Agent промпт (поле text):**
```
Составь короткий пост для Telegram "[ТЕМА КАНАЛА]".

Используй данные ниже (материалы из интернета):
{{ $json.concatenated_row_content }}

Требования:
— 6–8 новостей
— каждый буллет до 140 символов
— структура: «что произошло — почему важно»
— без лишних слов
```

**AI Agent systemMessage:**
```
Ты редактор Telegram-канала про [ТЕМА].

Пиши кратко, по делу.
Формат:
-жирный заголовок
-список буллитов

Без вводных абзацев.
Без выводов.
Без прогнозов.
Один буллет — одна новость.
```

**Edit Fields1 (очистка think-тегов):**
- `={{ $json.output.replace(/<think>[\s\S]*?<\/think>\s*/g, '').trim() }}`
- ⚠️ Нужна при использовании моделей с CoT (DeepSeek, Qwen и т.п.), которые оборачивают рассуждения в `<think>...</think>`

**Что проверять у студента:**
1. `Schedule Trigger` с расписанием (triggerAtHour или другой интервал)
2. Нода Set с темой запроса (Prompt) — обязательно на тему своего канала
3. POST к Tavily `/search` с параметрами: query, search_depth=advanced, max_results, time_range, country
4. `Split Out` разбивает поле results
5. `Filter` по score > 0.7 (порог может отличаться)
6. `Aggregate` собирает URL-адреса в массив
7. POST к Tavily `/extract` с массивом URL; тело содержит `urls` и `extract_depth`
8. `Split Out1` разбивает results извлечения
9. `Summarize` объединяет row_content (поле и разделитель могут отличаться)
10. `AI Agent` с системным промптом под тему **своего** канала (не скопировано «Банкротство»)
11. `Edit Fields1` очищает think-теги — обязателен при CoT-моделях
12. Telegram нода отправляет результат; кредиты подключены

**Типичные ошибки:**
- Тема промпта и системный промпт не адаптированы (скопированы из эталона «банкротство»)
- Нет `Filter` — все новости идут в извлечение, включая нерелевантные
- `Aggregate` не настроен на поле url — массив URL не формируется
- В теле `/extract` не используется `.toJsonString()` — URL не сериализуется в JSON
- `Split Out` или `Split Out1` указывает не то поле (не results)
- `Summarize` объединяет не то поле (не row_content)
- Нет очистки think-тегов при использовании CoT-модели
- Кредиты Tavily или Telegram не подключены

---

### Фабрика клонов — Урок 13.2 (Webhook-генератор постов с Airtable)

**Тема:** Webhook принимает URL, стиль и ID записи; параллельно обновляет статус в Airtable, загружает стиль и извлекает контент страницы; затем AI-агент генерирует пост и сохраняет в Airtable.

**Структура воркфлоу (11 нод):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Webhook` | webhook v2.1 | получает query params: url, style, id |
| `Edit Fields` | set v3.4 | Url=$json.query.url, Style=$json.query.style, ID=$json.query.id |
| `Update record` | airtable v2.1 | база TG POSTS, таблица Posts; matchBy: id; Select="Process" |
| `Search records` | airtable v2.1 | таблица Style; filterByFormula: `=(Name) = "{{ $json.Style }}"` |
| `HTTP Request` | httpRequest v4.4 | POST `https://api.tavily.com/extract`; `{"urls": ["{{ $json.Url }}"], "extract_depth": "advanced"}`; Bearer «Taveli 02» |
| `Edit Fields1` | set v3.4 | system_prompt = $json.Prompt (из Search records) |
| `Edit Fields2` | set v3.4 | url_content = $json.results[0].raw_content (из HTTP Request) |
| `Merge` | merge v3.2 | mode: combine, combineBy: combineAll |
| `AI Agent` | langchain.agent v3.1 | text: $json.url_content; systemMessage: "You are a helpful assistant {{ $json.system_prompt }}" |
| `OpenAI Chat Model` | lmChatOpenAi v1.3 | model: claude-haiku-4.5; кредиты: AITunel |
| `Update record1` | airtable v2.1 | таблица Posts; Post=$json.output, Select=Done; id из `$('Edit Fields').item.json.ID` |

**Связи:**
- `Webhook` → `Edit Fields`
- `Edit Fields` → `Update record` (параллельно, ветка 0)
- `Edit Fields` → `Search records` (параллельно, ветка 1)
- `Edit Fields` → `HTTP Request` (параллельно, ветка 2)
- `Search records` → `Edit Fields1` → `Merge` (input[0])
- `HTTP Request` → `Edit Fields2` → `Merge` (input[1])
- `Merge` → `AI Agent` → `Update record1`
- `OpenAI Chat Model` → `AI Agent` (ai_languageModel)

**Параметры webhook:**
- Входящий запрос: `?url=...&style=...&id=...`
- Поля читаются через `$json.query.url`, `$json.query.style`, `$json.query.id`

**Параллельные ветки из Edit Fields:**
- `Update record` — сразу помечает запись как «в процессе» (Select = "Process")
- `Search records` — ищет стиль из базы Style по имени
- `HTTP Request` — извлекает контент страницы через Tavily /extract

**⚠️ Опечатка в эталоне:**
В теле HTTP Request написано `"extract.depth"` вместо `"extract_depth"` — ошибка в эталоне, студент должен использовать правильный ключ `"extract_depth"`.

**Merge (combineAll):**
- Ждёт оба потока: Edit Fields1 (стиль) и Edit Fields2 (контент)
- После объединения в `$json` доступны поля из обеих веток: system_prompt и url_content

**AI Agent:**
- text (пользовательский промпт): `$json.url_content`
- systemMessage: `You are a helpful assistant {{ $json.system_prompt }}`
- Динамический system_prompt приходит из Airtable (таблица Style)

**Update record1 (финальный):**
- matchBy: id = `$('Edit Fields').item.json.ID`
- Поле Post: `$json.output`
- Поле Select: `Done`
- ⚠️ ID берётся через прямую ссылку на `Edit Fields`, не из `$json` (Merge мог изменить контекст)

**Что проверять у студента:**
1. Webhook триггер принимает параметры url, style, id через query string
2. `Edit Fields` извлекает три поля: Url, Style, ID из `$json.query.*`
3. Из `Edit Fields` выходят **три параллельные ветки** одновременно
4. `Update record` немедленно помечает запись как «в процессе»
5. `Search records` ищет стиль в таблице Style с filterByFormula по Name
6. `HTTP Request` извлекает контент страницы через Tavily /extract (корректный ключ `extract_depth`)
7. `Edit Fields1` и `Edit Fields2` подготавливают данные для Merge
8. `Merge` в режиме combineAll объединяет оба потока
9. `AI Agent` использует динамический system_prompt из Airtable
10. `Update record1` сохраняет Post и меняет Select на Done; ID берётся из `Edit Fields`
11. Кредиты Airtable и Tavily Bearer подключены

**Типичные ошибки:**
- Ветки из `Edit Fields` не параллельные — выполняются последовательно
- `Search records` не использует filterByFormula — загружает все записи Style
- Нет `Merge` или он настроен не в режиме combineAll — данные из веток не объединяются
- `AI Agent` получает только одну ветку данных (system_prompt или url_content, но не оба)
- В финальном `Update record1` ID берётся из `$json.ID` (может потеряться после Merge)
- Опечатка `extract.depth` не исправлена — параметр не передаётся в Tavily
- `Update record` (статус Process) отсутствует — нет индикации начала обработки

---

### Фабрика клонов — Урок 23 (Telegram Niche Research AI Agent)

**Тема:** Telegram-бот для анализа YouTube/VK-ниш: принимает вопрос пользователя, маршрутизирует по командам, отвечает через AI Agent с инструментами SerpAPI и калькулятором дохода, разбивает длинные ответы на части.

**Структура воркфлоу (12 нод):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Telegram Trigger` | telegramTrigger v1.2 | updates: message; кредиты: «TYnish bot» |
| `SET Telegram Data` | set **v3.3** | chatId, userId, username, messageText, messageId |
| `Check Command` | switch **v3.1** | output "welcome" если messageText startsWith "/start"; fallbackOutput → AI |
| `Welcome Message` | set v3.3 | response=приветственный текст, chatId и messageId |
| `AI Agent - Niche Expert` | langchain.agent **v1.6** | promptType: define; text: `$input.first().json.messageText`; обширный systemMessage |
| `OpenAI Chat Model` | lmChatOpenAi v1.3 | model: **gpt-4.1**; кредиты: AITunel |
| `Redis Memory` | memoryRedisChat **v1.3** | sessionKey: `={{ 'chat_' + $('SET Telegram Data').item.json.chatId }}`; sessionTTL: 604800; contextWindowLength: 20 |
| `SerpAPI` | toolSerpApi v1 | options: gl=us, hl=ru; кредиты: «SerpApi account 75» → подключён к AI Agent через **ai_tool** |
| `Code Tool - Calculator` | toolCode v1.1 | name: revenue_calculator; JS-код расчёта дохода → ai_tool |
| `Format Response` | set v3.3 | finalResponse=$json.output, chatId и messageId из SET Telegram Data |
| `Split Long Message` | code v2 | JS разбивает текст >4000 символов на части с маркировкой «Часть N/Total» |
| `Send to Telegram` | telegram v1.2 | chatId=$json.chatId, text=$json.text\|\|$json.response\|\|$json.finalResponse; reply_to_message_id=$json.messageId; appendAttribution:false |

**Связи:**
- `Telegram Trigger` → `SET Telegram Data` → `Check Command`
- `Check Command` "welcome" → `Welcome Message` → `Send to Telegram`
- `Check Command` fallback → `AI Agent - Niche Expert` → `Format Response` → `Split Long Message` → `Send to Telegram`
- `OpenAI Chat Model` → `AI Agent` (ai_languageModel)
- `Redis Memory` → `AI Agent` (ai_memory)
- `SerpAPI` → `AI Agent` (ai_tool)
- `Code Tool - Calculator` → `AI Agent` (ai_tool)

**⚠️ Версии нод отличаются от других уроков:**
- `set` — typeVersion **3.3** (в уроках 7, 9 и др. — 3.4)
- `switch` — typeVersion **3.1** (в уроках 12 и др. — 3.4)
- `langchain.agent` — typeVersion **1.6** (в уроках 7, 9 и др. — 3.1)
- `memoryRedisChat` — typeVersion **1.3** (в уроках 7, 9 — 1.5)

**SET Telegram Data (поля):**
- chatId = `$json.message.chat.id`
- userId = `$json.message.from.id`
- username = `$json.message.from.username || $json.message.from.first_name`
- messageText = `$json.message.text || ''`
- messageId = `$json.message.message_id`

**Check Command (switch v3.1):**
- output[0] "welcome": messageText startsWith "/start"
- fallbackOutput: всё остальное → AI Agent

**AI Agent (langchain.agent v1.6):**
- text: `={{ $input.first().json.messageText }}` (⚠️ не `$json.messageText` — используется `$input.first()`)
- Обширный systemMessage: эксперт по YouTube/VK нишам, анализирует монетизацию, конкуренцию, тренды

**Redis Memory (memoryRedisChat v1.3):**
- sessionKey: `={{ 'chat_' + $('SET Telegram Data').item.json.chatId }}`
- ⚠️ Префикс `'chat_'` (не `'tg:'` как в уроках 7, 9)
- sessionTTL: 604800 (7 дней); contextWindowLength: 20

**SerpAPI (toolSerpApi v1):**
- options: gl=us, hl=ru (страна поиска — US, язык — русский)
- Подключение: ai_tool к AI Agent

**Code Tool - Calculator (toolCode v1.1):**
- name: `revenue_calculator`
- description: инструмент расчёта дохода YouTube
- JS-код:
```javascript
const dailyViews = $input.first().json.dailyViews || 10000;
const cpm = $input.first().json.cpm || 5;
const partnerPercent = $input.first().json.partnerPercent || 10;
const monthlyViews = dailyViews * 30;
const adRevenue = (monthlyViews / 1000) * cpm * 0.55;
const partnerRevenue = adRevenue * (partnerPercent / 100);
const totalRevenue = adRevenue + partnerRevenue;
return `Расчёт дохода YouTube:\n...`
```
- Подключение: ai_tool к AI Agent

**Split Long Message (code v2):**
- JS-код разбивает `$json.finalResponse` (или `text`) на части по 4000 символов
- Добавляет маркировку «Часть N/Total» к каждой части
- Возвращает массив объектов `[{ chatId, text, messageId }, ...]`

**Send to Telegram:**
- chatId: `$json.chatId`
- text: `$json.text || $json.response || $json.finalResponse` (порядок важен — берёт первое непустое)
- reply_to_message_id: `$json.messageId` (ответ как реплай на сообщение пользователя)
- appendAttribution: false

**Что проверять у студента:**
1. `SET Telegram Data` присутствует и извлекает: chatId, userId, username (с fallback на first_name), messageText (с fallback на ''), messageId
2. `Check Command` (Switch) корректно маршрутизирует /start → ветка приветствия, всё остальное → AI
3. Ветка /start завершается отправкой приветственного сообщения в Telegram
4. `AI Agent` имеет typeVersion **1.6** (не 3.1) и получает текст через `$input.first().json.messageText`
5. `OpenAI Chat Model` подключён через ai_languageModel; модель — gpt-4.1 или аналог
6. `Redis Memory` подключена через ai_memory; sessionKey содержит `chatId` (не `tg_id`), префикс `'chat_'`
7. `SerpAPI` подключён к AI Agent через **ai_tool** (не main)
8. `Code Tool - Calculator` подключён через ai_tool; содержит JS-код расчёта дохода
9. `Format Response` (Set) передаёт finalResponse, chatId и messageId далее
10. `Split Long Message` (Code) разбивает длинные ответы на части
11. `Send to Telegram` использует `reply_to_message_id` для реплая на сообщение пользователя

**Типичные ошибки:**
- AI Agent typeVersion 3.1 вместо 1.6 — может не поддерживать инструменты типа ai_tool в этой конфигурации
- text в AI Agent написан как `$json.messageText` вместо `$input.first().json.messageText`
- SerpAPI или Code Tool подключены к AI Agent через main вместо ai_tool
- sessionKey Redis содержит `tg_id` или `userId` вместо `chatId`
- Нет Split Long Message — длинные ответы обрезаются или вызывают ошибку Telegram
- reply_to_message_id не указан — бот не реплаит на сообщение пользователя
- Нет ветки /start или Welcome Message — бот молчит при первом обращении
- set typeVersion 3.4 вместо 3.3 — может вызвать ошибку несовместимости

---

### Фабрика клонов — Урок 24 (YouTube Parser — двухворкфлоуная архитектура)

**Тема:** Telegram-бот парсит YouTube Shorts через API, анализирует тренды в заданной нише с помощью AI Agent и отправляет ответ в Telegram. Архитектура из двух воркфлоуов: главный (бот) + вспомогательный (парсер, вызывается как toolWorkflow).

#### Главный воркфлоу (9 нод)

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Telegram Trigger` | telegramTrigger v1.2 | updates: message; кредиты: «ParserYT» |
| `AI Agent` | langchain.agent **v1.6** | promptType: define; text: `={{ $json.message.text }}`; обширный systemMessage |
| `Redis Chat Memory` | memoryRedisChat **v1.5** | sessionKey: `={{ $json.message.text }}`; sessionTTL: 604804 |
| `OpenAI Chat Model` | lmChatOpenAi v1.3 | model: **gpt-5**; кредиты: «AITunel Cliaude» |
| `youtube_search` | toolWorkflow **v2.2** | вызывает sub-workflow «Youtube parser second API» (id: lnbR9PDQ6ibhgBx5); подключён через **ai_tool** |
| `Split Long Message` | code v2 | JS разбивает `$json.output` по 4000 символов с маркировкой «📄 Часть N/Total» |
| `Data Matching` | code v2 | извлекает search_term из Telegram Trigger, ищет YouTube-ссылки regex в output |
| `Append row in sheet` | googleSheets v4.7 | append; documentId: `10KG6yLvjTAh7CASulFxg6no-1xgt015H9DiV_F1T3gI`; sheetName: «Youtube» (gid=49621647); колонки: ts, chat_id, user_text, answer_full, search_term, videos |
| `Send a text message` | telegram v1.2 | chatId: `={{ $('Telegram Trigger').item.json.message.from.id }}`; text: `={{ $json.text }}`; parse_mode: HTML; appendAttribution: false; кредиты «ParserYT» |

**Связи главного воркфлоу:**
- `Telegram Trigger` → `AI Agent`
- `AI Agent` → `Split Long Message` (параллельно, ветка 1)
- `AI Agent` → `Data Matching` (параллельно, ветка 2)
- `Split Long Message` → `Send a text message`
- `Data Matching` → `Append row in sheet`
- `OpenAI Chat Model` → `AI Agent` (ai_languageModel)
- `Redis Chat Memory` → `AI Agent` (ai_memory)
- `youtube_search` → `AI Agent` (ai_tool)

**⚠️ Ключевые особенности главного воркфлоу:**
- `langchain.agent` — typeVersion **1.6** (как в Уроке 23)
- `memoryRedisChat` — typeVersion **v1.5** (как в Уроках 7, 9)
- sessionKey Redis = **текст сообщения** (`$json.message.text`), НЕ user ID — нетипичный паттерн
- text в AI Agent = `$json.message.text` (напрямую из триггера, без промежуточной SET-ноды)
- chatId в Telegram = **`from.id`** (не `chat.id`) — `$('Telegram Trigger').item.json.message.from.id`
- parse_mode: **HTML** в ноде отправки
- Параллельные ветки из AI Agent: Split Long Message → Telegram И Data Matching → Google Sheets
- Логирование в Google Sheets (таблица «Копия Дипломный проект выпускника Чернова АВ», лист «Youtube»)

**AI Agent (главный воркфлоу):**
- systemMessage: обширный промпт — эксперт по YouTube-нишам, ищет Shorts, анализирует тренды
- Может вызывать инструмент `youtube_search` до 3 раз
- Формирует ответ в HTML-разметке (для parse_mode: HTML)

**youtube_search (toolWorkflow v2.2):**
- workflowId: id вспомогательного воркфлоу (`lnbR9PDQ6ibhgBx5` в эталоне — у студента будет свой)
- Подключение к AI Agent: **ai_tool** (не main)
- ⚠️ Sub-workflow должен быть **опубликован** (active: true) для работы

**Split Long Message (code v2):**
- Разбивает `$json.output` на части по 4000 символов
- Маркировка: «📄 Часть N/Total»

**Data Matching (code v2):**
- Извлекает `search_term` из Telegram Trigger (текст запроса)
- Ищет YouTube-ссылки regex в `$json.output`
- Возвращает: `{ search_term, videos, answer_full }`

**Append row in sheet:**
- documentId: `10KG6yLvjTAh7CASulFxg6no-1xgt015H9DiV_F1T3gI`
- sheetName: «Youtube» (gid=49621647)
- Колонки: ts (timestamp), chat_id, user_text, answer_full, search_term, videos

#### Вспомогательный воркфлоу (11 нод)

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `When Executed by Another Workflow` | executeWorkflowTrigger v1.1 | inputSource: passthrough |
| `Clean Memory` | code v2 | очищает `workflowStaticData.lastExecution = { response: "" }` |
| `get_videos1` | youTube v1 | resource: video; limit: **7**; publishedAfter: последние **3 дня**; q из входящих данных; regionCode: **RU**; order: relevance |
| `loop_over_items1` | splitInBatches v3 | цикл по видео по одному |
| `retrieve_data_from_memory1` | code v2 | читает `workflowStaticData.lastExecution` |
| `find_video_data1` | httpRequest v4.2 | GET YouTube Data API; part=contentDetails,snippet,statistics; auth: oAuth2Api |
| `if_longer_than_3_` | if v2.2 | парсит ISO 8601 duration → секунды; условие: `durationInSeconds <= 90` (только Shorts!) |
| `group_data1` | set v3.4 | id, viewCount, likeCount, commentCount, description, title, channelTitle, tags (join), channelId |
| `save_data_to_memory1` | code v2 (runOnceForEachItem) | очищает от эмодзи/URL, накапливает с разделителем `### NEXT VIDEO FOUND: ###` |
| `response1` | set v3.4 | response = `JSON.stringify($('retrieve_data_from_memory1').all())` |

**Связи вспомогательного воркфлоу:**
- `When Executed by Another Workflow` → `Clean Memory` → `get_videos1` → `loop_over_items1`
- `loop_over_items1` output[0] (done) → `retrieve_data_from_memory1` → `response1`
- `loop_over_items1` output[1] (each item) → `find_video_data1` → `if_longer_than_3_`
- `if_longer_than_3_` true (≤90 сек) → `group_data1` → `save_data_to_memory1` → `loop_over_items1`
- `if_longer_than_3_` false (>90 сек, не Shorts) → `loop_over_items1` (пропускаем)

**⚠️ Ключевые особенности вспомогательного воркфлоу:**
- Накопление данных между итерациями через `$getWorkflowStaticData('global')` — данные хранятся в памяти воркфлоу
- `Clean Memory` в начале обязательна — очищает данные от предыдущего вызова
- Фильтр Shorts: `durationInSeconds <= 90` — только видео ≤90 секунд
- Поиск за последние **3 дня**: `new Date(Date.now() - 3 * 24 * 60 * 60 * 1000).toISOString()`
- Лимит: **7 видео**; регион: **RU**
- Разделитель между видео: `### NEXT VIDEO FOUND: ###`

**get_videos1 (нативная YouTube-нода):**
- resource: video; limit: 7
- publishedAfter: `={{ new Date(Date.now() - 3 * 24 * 60 * 60 * 1000).toISOString() }}`
- q (поисковый запрос): `={{ $('When Executed by Another Workflow').first().json.query }}`
- regionCode: RU; order: relevance; safeSearch: moderate
- credentials: «YouTube parser» (youTubeOAuth2Api)

**find_video_data1 (HTTP Request к YouTube Data API):**
- URL: `https://www.googleapis.com/youtube/v3/videos?`
- Query params: id=`$json.id.videoId`, part=contentDetails,snippet,statistics
- Auth: oAuth2Api; credentials: «YouTube»

**if_longer_than_3_ (фильтр длительности):**
```javascript
const iso8601ToSeconds = iso8601 => {
  const match = iso8601.match(/PT(?:(\d+)H)?(?:(\d+)M)?(?:(\d+)S)?/);
  const hours = parseInt(match[1] || 0, 10);
  const minutes = parseInt(match[2] || 0, 10);
  const seconds = parseInt(match[3] || 0, 10);
  return hours * 3600 + minutes * 60 + seconds;
};
// Условие: durationInSeconds <= 90
```

**save_data_to_memory1 (накопление):**
```javascript
// Очищает эмодзи regex \u{1F600}-\u{1F64F} и др.
// Удаляет URL (https?://\S+ и www\.\S+)
// Очищает \r, \n, лишние пробелы
// Накапливает с разделителем:
workflowStaticData.lastExecution.response += ' ### NEXT VIDEO FOUND: ### ';
workflowStaticData.lastExecution.response += removeEmojis(sanitizedItem);
```

**Что проверять у студента:**

*Главный воркфлоу:*
1. `Telegram Trigger` присутствует с кредитами
2. `AI Agent` — typeVersion **1.6**; text = `$json.message.text`; обширный systemMessage о YouTube Shorts
3. `Redis Chat Memory` подключена через ai_memory; **sessionKey = текст сообщения** (не user ID)
4. `OpenAI Chat Model` подключён через ai_languageModel; модель gpt-5 (или аналог)
5. `youtube_search` (toolWorkflow) подключён через **ai_tool**; указывает на вспомогательный воркфлоу
6. Из AI Agent выходят **две параллельные ветки**: Split Long Message → Telegram И Data Matching → Sheets
7. chatId в Telegram = `from.id` (не `chat.id`)
8. parse_mode: **HTML** в ноде отправки
9. `Data Matching` возвращает search_term, videos, answer_full для логирования
10. `Append row in sheet` пишет в лист «Youtube» с нужными колонками

*Вспомогательный воркфлоу:*
1. `When Executed by Another Workflow` — входная точка с passthrough
2. `Clean Memory` в самом начале — обязательна
3. `get_videos1` — нативная YouTube-нода; лимит 7; регион RU; фильтр по дате (3 дня); запрос из входящих данных
4. `loop_over_items1` (splitInBatches) — цикл по одному видео
5. `find_video_data1` — HTTP Request к YouTube Data API; получает contentDetails, snippet, statistics
6. `if_longer_than_3_` — фильтрует Shorts: `durationInSeconds <= 90`
7. `group_data1` — собирает поля: id, viewCount, likeCount, commentCount, description, title, channelTitle, tags, channelId
8. `save_data_to_memory1` — накапливает данные с разделителем `### NEXT VIDEO FOUND: ###`
9. `retrieve_data_from_memory1` → `response1` — возвращает накопленные данные
10. Sub-workflow **опубликован** (active: true) — без этого toolWorkflow не может его вызвать

**Типичные ошибки:**
- Sub-workflow не опубликован — toolWorkflow получает ошибку «workflow not found» или «not active»
- Нет `Clean Memory` — данные от предыдущего вызова накапливаются и искажают результат
- sessionKey Redis = `from.id` (user ID) вместо текста сообщения — паттерн нетипичный, но важно сверить с эталоном
- `youtube_search` подключён через main вместо ai_tool — AI Agent не может использовать его как инструмент
- chatId = `chat.id` вместо `from.id` — эталон использует именно `from.id`
- parse_mode не выставлен — HTML-разметка ответа отображается как текст с тегами
- Фильтр длительности: `<= 210` или другое значение вместо `<= 90` — пропускает не-Shorts видео
- `get_videos1` — нативная YouTube-нода (не HTTP Request) — различие важно для кредитов
- Отсутствует одна из параллельных веток из AI Agent (нет Sheets или нет Telegram)

---

### Фабрика клонов — Урок 26 (Main HeyGen WF — сбор Shorts через Apify)

**Тема:** Ручной воркфлоу для сбора новых YouTube Shorts из каналов-конкурентов: загружает уже сохранённые видео для дедупликации, перебирает каналы из Google Sheets, для каждого запрашивает Apify YouTube Scraper, фильтрует новинки и записывает их в лист «Videos».

**Структура воркфлоу (9 нод):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `When clicking 'Execute workflow'` | manualTrigger v1 | ручной запуск |
| `Get Existing Videos` | googleSheets v4.7 | read; sheet «Videos» (gid=901834362); range A2:H; **executeOnce: true; alwaysOutputData: true** |
| `Get channels` | googleSheets v4.7 | read; sheet «Channels» (gid=1695463219); фильтр: enabled=="true"; **executeOnce: true** |
| `Loop Over Items` | splitInBatches v3 | цикл по каналам по одному |
| `Apify YouTube Scraper` | httpRequest v4.4 | POST Apify actor; Bearer auth; credentials: «ApiFy» |
| `Normalize Video Data` | set v3.4 | title, video_id, video_url, views, published_at, channel_name, channel_url |
| `Filter New Videos` | if v2.3 | looseTypeValidation; дедупликация по video_id |
| `Append New Videos (Sheets)` | googleSheets v4.7 | append; sheet «Videos»; status="NEW" |
| `No Operation, do nothing` | noOp v1 | когда цикл завершён (output[0]) |

**Связи:**
- `When clicking 'Execute workflow'` → `Get Existing Videos` → `Get channels` → `Loop Over Items`
- `Loop Over Items` output[0] (done) → `No Operation, do nothing`
- `Loop Over Items` output[1] (each item) → `Apify YouTube Scraper` → `Normalize Video Data` → `Filter New Videos`
- `Filter New Videos` true → `Append New Videos (Sheets)` → `Loop Over Items` (цикл)
- `Filter New Videos` false → (не подключена, пропуск)

**Get Existing Videos (googleSheets v4.7):**
- documentId: `10KG6yLvjTAh7CASulFxg6no-1xgt015H9DiV_F1T3gI`
- sheetName: «Videos» (gid=901834362); range: A2:H
- **executeOnce: true** — загружается один раз на весь цикл (не на каждой итерации)
- **alwaysOutputData: true** — обязательно! При пустом листе нода всё равно возвращает данные, цикл продолжается

**Get channels (googleSheets v4.7):**
- sheetName: «Channels» (gid=1695463219)
- Фильтр: enabled == "true" (только активные каналы)
- **executeOnce: true** — загружается один раз до начала цикла

**Apify YouTube Scraper (httpRequest v4.4):**
- URL: `https://api.apify.com/v2/acts/h7sDV53CddomktSi5/run-sync-get-dataset-items`
- Метод: POST; авторизация: httpBearerAuth; кредиты: «ApiFy»
- Тело запроса:
```json
{
  "startUrls": [{ "url": "{{ $json.channel_url }}" }],
  "maxResults": 0,
  "maxResultsShorts": 10,
  "maxResultsStreams": 0,
  "oldestPostDate": "5 days",
  "sortBy": "NEWEST"
}
```
- ⚠️ `maxResults: 0` — обычные видео не собираются, только Shorts
- `maxResultsShorts: 10` — до 10 Shorts за раз
- `oldestPostDate: "5 days"` — только видео за последние 5 дней
- `sortBy: "NEWEST"` — сортировка по дате публикации

**Normalize Video Data (set v3.4):**
- title = `$json.title`
- video_id = `$json.id` (⚠️ не `$json.videoId` — Apify возвращает поле `id`)
- video_url = `$json.url`
- views = `$json.viewCount`
- published_at = `$json.date`
- channel_name = `$json.channelName`
- channel_url = `$json.channelUrl`

**Filter New Videos (if v2.3):**
- looseTypeValidation: true
- Условие (Boolean):
```javascript
Boolean(
  $items("Get Existing Videos").length === 0
    ? true
    : !$items("Get Existing Videos").map(i => i.json.video_id).includes($json.video_id)
)
```
- ⚠️ Если существующих видео нет (length === 0) — всё записывается как новое
- ⚠️ Ссылка на ноду `Get Existing Videos` — имя должно совпадать точно

**Append New Videos (Sheets) (googleSheets v4.7):**
- sheetName: «Videos» (gid=901834362)
- Операция: append
- Поля при записи: video_id, channel_name, video_url, original_title, views, status="NEW", created_at, updated_at
- Формат дат: `DateTime.now().toFormat("dd.MM.yy HH:mm")`
- Схема листа содержит много дополнительных колонок (summary, script_doc_url, heygen_video_id, heygen_video_url, pub_youtube/vk/instagram и др.) — это первый воркфлоу в HeyGen-пайплайне

**Google Sheets таблица:**
- documentId: `10KG6yLvjTAh7CASulFxg6no-1xgt015H9DiV_F1T3gI` («Копия Дипломный проект выпускника Чернова АВ»)
- Лист «Channels» (gid=1695463219): список каналов-конкурентов с полем channel_url и флагом enabled
- Лист «Videos» (gid=901834362): база собранных видео

**Что проверять у студента:**
1. Manual Trigger как точка входа
2. `Get Existing Videos` присутствует; **executeOnce: true** и **alwaysOutputData: true** выставлены
3. `Get channels` присутствует; **executeOnce: true** выставлен; фильтр по enabled=="true"
4. `Loop Over Items` (splitInBatches) — цикл по каналам
5. `Apify YouTube Scraper` — HTTP Request POST к Apify actor `h7sDV53CddomktSi5`; Bearer auth (кредиты «ApiFy» или аналог)
6. Параметры Apify: `maxResults: 0`, `maxResultsShorts: 10`, `oldestPostDate: "5 days"`, `sortBy: "NEWEST"`
7. `Normalize Video Data` извлекает поля из Apify-ответа: особенно `video_id = $json.id` (не `$json.videoId`)
8. `Filter New Videos` использует `$items("Get Existing Videos")` для дедупликации; обрабатывает случай пустого листа
9. `Append New Videos (Sheets)` пишет в лист «Videos» с полем status="NEW" и датами
10. Цикл после append возвращается к `Loop Over Items`
11. `No Operation` обрабатывает выход из цикла (output[0])

**Типичные ошибки:**
- `alwaysOutputData: true` не выставлен в `Get Existing Videos` — при пустом листе воркфлоу обрывается
- `executeOnce: true` не выставлен — нода читает Sheets на каждой итерации цикла (медленно и лишний расход квоты API)
- Поле `video_id` берётся из `$json.videoId` вместо `$json.id` — Apify возвращает именно `id`
- Фильтр дедупликации использует название ноды, отличное от фактического — ошибка ссылки
- Нет обработки случая `length === 0` в Filter — при пустом листе все видео отфильтровываются
- `maxResults` не равен 0 — собираются обычные видео помимо Shorts
- Нет фильтра по enabled в `Get channels` — неактивные каналы попадают в цикл
- После `Append New Videos` нет возврата к `Loop Over Items` — цикл не продолжается
- `No Operation` не подключён к output[0] цикла — воркфлоу зависает при завершении цикла

---

### Фабрика клонов — Урок 27 (Script Generator — автоматическая генерация сценариев)

**Тема:** Автоматическая генерация сценариев для YouTube Shorts: при обновлении строки в Google Sheets воркфлоу получает транскрипт видео через Apify, классифицирует тему с помощью AI, генерирует сценарий на русском и сохраняет в Google Docs, обновляя запись в Sheets.

**Структура воркфлоу (16 нод):**

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Get Shorts` | googleSheetsTrigger v1 | rowUpdate; sheet «Videos» gid=901834362; credentials: Google Sheets01 |
| `are you ready` | if v2.3 | AND: !!action_make_script==true; script_doc_url empty; status≠"ERROR" |
| `Batch \| Script Queue (1-by-1)` | splitInBatches v3 | цикл по одному |
| `Extract Video ID` | code v2 | парсит /shorts/, ?v=, youtu.be → video_id_extracted |
| `Fix Data` | set v3.4 | video_id=$json.video_id; video_url=$json.video_url |
| `Run an Actor and get dataset` | apify v1 | actor faVsWy9VTSNVIhWpR (Youtube Transcript Scraper by pintostudio); memory:4096; onError:continueErrorOutput |
| `Clear transcript` | code v2 | joins segments: `segments.map(s=>s.text).join(' ')` |
| `AI \| Classify Topic` | langchain.agent v3.1 | claude-haiku-4.5 (AITunel); hasOutputParser:true; onError:continueErrorOutput |
| `Structured Output Parser` | outputParserStructured v1.3 | schema: {category, tone, viral_angle} |
| `AI \| Generate Script+Title+CTA (70/30)` | langchain.agent v3.1 | claude-3.5-haiku (AITunel); onError:continueErrorOutput |
| `Structured Output Parser1` | outputParserStructured v1.3 | schema: {title, script, cta} |
| `Merge` | merge v3.2 | combineByPosition; input[0]=AI Generate, input[1]=Extract Video ID |
| `Create a document` | googleDocs v2 | folder: 1siDEg5lqLC1aho20vS3CFPQIQNjdD8ao; title: ShortScript \| video_id_extracted \| dd-MM-yy |
| `Update a document` | googleDocs v2 | documentURL=$json.id; insert structured text |
| `Update row in sheet` | googleSheets v4.7 | matchBy video_id; status=SCRIPT_DONE; action_make_script="" |
| `If error` | if v2.3 | !!$json.error \|\| !!$json.message \|\| !!$json.stack \|\| !!$json.cause |
| `Update row in sheet error` | googleSheets v4.7 | matchBy video_id из Fix Data; status=ERROR |

**Связи:**
- `Get Shorts` → `are you ready`
- `are you ready` true → `Batch | Script Queue (1-by-1)`
- `Batch | Script Queue` output[1] (each item) → `Extract Video ID` → `Fix Data`
- `Fix Data` → `Run an Actor and get dataset` (параллельно)
- `Fix Data` → `Clear transcript` (параллельно, fan-out)
- `Run an Actor and get dataset` output[0] → `Clear transcript`
- `Run an Actor and get dataset` output[1] → `If error`
- `Clear transcript` → `AI | Classify Topic`
- `AI | Classify Topic` output[0] → `AI | Generate Script+Title+CTA`
- `AI | Classify Topic` output[1] → `If error`
- `AI | Generate Script` output[0] → `Merge` (input[0])
- `AI | Generate Script` output[1] → `If error`
- `Extract Video ID` → `Merge` (input[1])
- `Merge` → `Create a document` → `Update a document` → `Update row in sheet` → `Batch` (цикл)
- `If error` true → `Update row in sheet error` → `Batch` (цикл)
- `Batch` output[0] (done) → (не подключено)

**Trigger: Get Shorts (googleSheetsTrigger v1):**
- event: rowUpdate (триггер на обновление строки, НЕ ручной запуск)
- sheetName: «Videos» (gid=901834362)
- documentId: `10KG6yLvjTAh7CASulFxg6no-1xgt015H9DiV_F1T3gI`
- credentials: Google Sheets01 (OAuth2)

**are you ready (if v2.3) — 3 условия AND:**
- `!!$json.action_make_script` == true (поле не пустое/false)
- `$json.script_doc_url` is empty (документ ещё не создан)
- `$json.status` != "ERROR" (не повторяем ошибочные)

**Extract Video ID (code v2):**
```javascript
const url = $json.video_url;
let videoId = null;
// /shorts/
const shortsMatch = url.match(/shorts\/([^?&/]+)/);
if (shortsMatch) { videoId = shortsMatch[1]; }
// ?v=
if (!videoId) {
  const watchMatch = url.match(/[?&]v=([^?&/]+)/);
  if (watchMatch) { videoId = watchMatch[1]; }
}
// youtu.be/
if (!videoId) {
  const shortUrlMatch = url.match(/youtu\.be\/([^?&/]+)/);
  if (shortUrlMatch) { videoId = shortUrlMatch[1]; }
}
return [{ json: { ...$json, video_id_extracted: videoId } }];
```

**Fix Data (set v3.4):**
- video_id = `$json.video_id`
- video_url = `$json.video_url`
- ⚠️ Сохраняет контекст до fan-out — нужен для error handler, где `$('Fix Data').item.json.video_id`

**Run an Actor and get dataset (apify v1):**
- actor: `faVsWy9VTSNVIhWpR` (Youtube Transcript Scraper by pintostudio)
- memory: 4096
- onError: continueErrorOutput
- Тело запроса:
```json
{
  "targetLanguage": "en",
  "videoUrl": "{{ $json.video_url }}"
}
```

**Clear transcript (code v2):**
```javascript
const segments = $json.data || [];
const fullText = segments.map(s => s.text).join(' ');
return [{ json: { ...$json, transcript: fullText } }];
```

**AI | Classify Topic (langchain.agent v3.1):**
- Модель: claude-haiku-4.5 (AITunel)
- hasOutputParser: true; onError: continueErrorOutput
- systemMessage:
```
Категории: Технологии / AI; Бизнес / Деньги; Скандал / Конфликт; Личность / Лидерство; Образование / Объяснение; Прогноз / Будущее; Ошибка / Разоблачение; История / Драма
Тоны: Провокационный; Тревожный; Воодушевляющий; Нейтрально-экспертный; Драматичный
Вирусный угол (1 предложение)
Ответ строго: {"category":"...","tone":"...","viral_angle":"..."}
```

**Structured Output Parser (outputParserStructured v1.3):**
- schema: `{category: string, tone: string, viral_angle: string}`

**AI | Generate Script+Title+CTA (70/30) (langchain.agent v3.1):**
- Модель: claude-3.5-haiku (AITunel)
- onError: continueErrorOutput
- text (user prompt): `=Вот транскрипция оригинального видео:\n{{ $node["Clear transcript"].json.transcript }}`
  ⚠️ Ссылается на ноду `Clear transcript` напрямую через `$node[...]`, не через `$json`
- systemMessage (ключевые правила):
  - На русском, до 60 секунд
  - Мощный хук в первых 1-2 предложениях
  - 70% вирус / 30% экспертность
  - Скрипт 900-1100 символов
  - CTA с обязательной ссылкой: `https://aimschool.ru/partnerfabrika/?gcpc=1d23f`
  - title ≤70 символов
  - Формат: `{"title":"...","script":"...","cta":"..."}`

**Structured Output Parser1 (outputParserStructured v1.3):**
- schema: `{title: string, script: string, cta: string}`

**Merge (merge v3.2):**
- mode: combineByPosition
- input[0]: из `AI | Generate Script` (title, script, cta)
- input[1]: из `Extract Video ID` (video_id_extracted, исходные данные)
- После Merge доступны поля из обоих потоков

**Create a document (googleDocs v2):**
- folder: `1siDEg5lqLC1aho20vS3CFPQIQNjdD8ao`
- title: `ShortScript | {{ $json.video_id_extracted }} | {{ $now.format('dd-MM-yy') }}`

**Update a document (googleDocs v2):**
- documentURL: `$json.id` (ID созданного документа)
- Вставляемый текст:
```
Заголовок:
{{$node["AI | Generate Script+Title+CTA (70/30)"].json.output.title}}

Оригинал:
{{$node["Extract Video ID"].json.video_url}}

Категория: {{$node["AI | Classify Topic"].json.output.category}}
Тон: {{$node["AI | Classify Topic"].json.output.tone}}
Вирусный угол: {{$node["AI | Classify Topic"].json.output.viral_angle}}

---

Сценарий:
{{$node["AI | Generate Script+Title+CTA (70/30)"].json.output.script}}

---

CTA:
{{$node["AI | Generate Script+Title+CTA (70/30)"].json.output.cta}}
```

**Update row in sheet (success) (googleSheets v4.7):**
- matchBy: video_id = `={{ $('Merge').item.json.video_id }}`
- script_doc_url = `https://docs.google.com/document/d/{{ $json.documentId }}/edit`
- status = "SCRIPT_DONE"
- updated_at = `={{$now.setZone("Europe/Moscow").format("dd.MM.yy HH:mm")}}`
- action_make_script = "" (очищается после обработки)
- row_number = 0 (readOnly, системное)

**Update row in sheet error (googleSheets v4.7):**
- matchBy: video_id = `={{ $('Fix Data').item.json.video_id }}`
- ⚠️ Берётся из `Fix Data`, так как в error path контекст мог измениться
- status = "ERROR"
- updated_at = `={{$now.setZone("Europe/Moscow").format("dd.MM.yy HH:mm")}}`

**If error (if v2.3):**
- Условие: `!!$json.error || !!$json.message || !!$json.stack || !!$json.cause`
- Принимает ошибки от трёх нод: Apify, AI Classify, AI Generate

**Что проверять у студента:**
1. Триггер — `Google Sheets Trigger` с событием **rowUpdate** (не ручной запуск)
2. `are you ready` (If) проверяет три условия AND: action_make_script не пусто; script_doc_url пусто; status ≠ ERROR
3. `Batch | Script Queue` (splitInBatches) — обрабатывает по одному элементу
4. `Extract Video ID` (Code) — парсит все форматы YouTube URL: /shorts/, ?v=, youtu.be/
5. `Fix Data` (Set) сохраняет video_id и video_url до fan-out — критично для error path
6. `Run an Actor` — Apify actor `faVsWy9VTSNVIhWpR`; тело: `{"targetLanguage": "en", "videoUrl": "..."}` ; onError: continueErrorOutput
7. `Clear transcript` (Code) — объединяет сегменты: `segments.map(s=>s.text).join(' ')`
8. `AI | Classify Topic` — возвращает JSON {category, tone, viral_angle}; подключён Structured Output Parser
9. `AI | Generate Script` — text ссылается на `$node["Clear transcript"].json.transcript` (не `$json`); возвращает {title, script, cta}; подключён Structured Output Parser1
10. `Merge` (combineByPosition) объединяет вывод AI Generate и данные Extract Video ID
11. `Create a document` создаёт Google Doc в нужной папке
12. `Update a document` наполняет документ всеми полями: заголовок, оригинал, категория, тон, вирусный угол, сценарий, CTA
13. `Update row in sheet` (success): status=SCRIPT_DONE, script_doc_url заполнен, action_make_script очищен; matchBy через `$('Merge').item.json.video_id`
14. `If error` обрабатывает ошибки от всех трёх нод (Apify, AI Classify, AI Generate)
15. `Update row in sheet error` (error): status=ERROR; matchBy через `$('Fix Data').item.json.video_id`
16. Цикл возвращается к `Batch` после каждой обработки (и успешной, и ошибочной)

**Типичные ошибки:**
- Триггер ручной (Manual) вместо Google Sheets rowUpdate
- `are you ready` отсутствует или проверяет не все три условия — воркфлоу запускается повторно
- `Fix Data` отсутствует — в error handler нет контекста video_id
- `Run an Actor` не имеет `onError: continueErrorOutput` — при ошибке Apify воркфлоу прерывается
- `Clear transcript` не объединяет сегменты — transcript пустой или не тот формат
- AI Generate ссылается на `$json.transcript` вместо `$node["Clear transcript"].json.transcript` — получает пустые данные после Merge
- Structured Output Parser не подключён к одному из AI Agent — JSON не парсится
- `Merge` режим не combineByPosition — данные из двух потоков не объединяются корректно
- `Update row in sheet` (success) не очищает `action_make_script` — воркфлоу повторно срабатывает на ту же строку
- `Update row in sheet error` берёт video_id из `$json` вместо `$('Fix Data')` — в error path контекст потерян
- Нет `If error` или не все три ноды с ошибками подключены к нему
---

### Фабрика клонов — Урок 29 (HeyGen — двухворкфлоуная архитектура генерации видео)

**Тема:** Двухворкфлоуная система генерации аватар-видео через HeyGen: первый воркфлоу (ручной запуск) читает сценарии из Google Sheets, скачивает текст сценария из Google Drive, отправляет задание в HeyGen API с callback_id; второй воркфлоу принимает webhook-callback от HeyGen и записывает ссылку на готовое видео обратно в Sheets.

#### Воркфлоу 5 — Generate Video (12 нод)

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `TRIGGER \| Manual` | manualTrigger v1 | ручной запуск |
| `GS \| Get Videos` | googleSheets v4.7 | read; sheet «Videos» gid=901834362 |
| `IF \| Ready For HeyGen` | if v2.3 | AND: action_send_heygen==true; heygen_video_url empty; script_doc_url not empty; looseTypeValidation |
| `FLOW \| Batch HeyGen` | splitInBatches v3 | batchSize: 1 (по одному) |
| `DRIVE \| Download Script Doc` | googleDrive v3 | download; docsToFormat: text/plain; fileId из script_doc_url |
| `DRIVE \| Extract Script Text` | extractFromFile v1.1 | destinationKey: script_text |
| `SCRIPT \| Parse Doc` | code v2 | парсит секции: Заголовок, Сценарий, CTA |
| `GS \| Get HeyGen Settings` | googleSheets v4.7 | read; sheet «Settings» gid=2046567203; range A1:F2 |
| `FLOW \| Merge Video + Settings` | merge v3.2 | combineByPosition; input[0]=SCRIPT Parse Doc, input[1]=GS Get HeyGen Settings |
| `HTTP \| HeyGen Create Video` | httpRequest v4.4 | POST api.heygen.com/v3/video-agents; callback_url+callback_id |
| `CODE \| Normalize HeyGen Response` | code v2 | извлекает heygen_video_id; сбрасывает action_send_heygen=false |
| `GS \| Mark HeyGen Processing` | googleSheets v4.7 | appendOrUpdate; matchBy: video_id; status=SENT_TO_HEYGEN |

**Связи воркфлоу 5:**
- `TRIGGER | Manual` → `GS | Get Videos` → `IF | Ready For HeyGen` (true) → `FLOW | Batch HeyGen`
- `FLOW | Batch HeyGen` output[1] (each) → `DRIVE | Download Script Doc` → `DRIVE | Extract Script Text` → `SCRIPT | Parse Doc`
- `SCRIPT | Parse Doc` → `FLOW | Merge Video + Settings` (input[0]); параллельно → `GS | Get HeyGen Settings`
- `GS | Get HeyGen Settings` → `FLOW | Merge Video + Settings` (input[1])
- `FLOW | Merge Video + Settings` → `HTTP | HeyGen Create Video` → `CODE | Normalize HeyGen Response` → `GS | Mark HeyGen Processing` → `FLOW | Batch HeyGen` (цикл)
- `FLOW | Batch HeyGen` output[0] (done) → не подключено

**IF | Ready For HeyGen — условия AND:**
- `$json.action_send_heygen` == true
- `$json.heygen_video_url` is empty
- `$json.script_doc_url` is not empty
- looseTypeValidation: true

**HTTP | HeyGen Create Video (тело запроса):**
```
{
  "prompt": "={{ $json.final_script }}",
  "avatar_id": "={{ $json.avatar_id }}",
  "orientation": "={{ $json.orientation }}",
  "callback_url": "https://n8n.vsellm.info/webhook/e8750122-5f63-41ec-85cd-af30a43e14e3",
  "callback_id": "={{ String($('FLOW | Batch HeyGen').item.json.row_number) }}"
}
```
- callback_id = строковое представление row_number из таблицы — именно по нему Workflow 6 найдёт нужную строку
- prompt = поле final_script, собранное нодой SCRIPT | Parse Doc (секция «Сценарий»)
- avatar_id и orientation приходят из листа «Settings»

**SCRIPT | Parse Doc (code v2):**
```javascript
const raw = $json.script_text || "";
let text = raw.replace(/\\n/g, "\n").replace(/\r/g, "");
function extractBlock(startLabel, endLabel = null) {
  const startIndex = text.indexOf(startLabel);
  if (startIndex === -1) return "";
  const from = startIndex + startLabel.length;
  if (!endLabel) return text.substring(from).trim();
  const endIndex = text.indexOf(endLabel, from);
  if (endIndex === -1) return text.substring(from).trim();
  return text.substring(from, endIndex).trim();
}
const title = extractBlock("Заголовок:", "Категория:");
const script = extractBlock("Сценарий:", "CTA:");
const cta = extractBlock("CTA:");
// Возвращает: title_clean, script_clean, final_script (=script_clean), cta_clean
```

**GS | Mark HeyGen Processing:**
- Режим: appendOrUpdate
- matchBy: video_id
- Записывает: heygen_video_id (из CODE Normalize), status=SENT_TO_HEYGEN

#### Воркфлоу 6 — Получаем видео (5 нод)

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Webhook` | webhook v2.1 | path: e8750122-5f63-41ec-85cd-af30a43e14e3 |
| `Code in JavaScript` | code v2 | парсит тело webhook: event_type, video_id, callback_id, video_url, share_url |
| `IF \| Есть video_id` | if v2.3 | video_id is not empty |
| `IF \| Видео готово` | if v2.3 | event_type == 'avatar_video.success' |
| `GS \| Update HeyGen URL` | googleSheets v4.7 | update; matchBy: row_number=Number($json.callback_id); heygen_video_url, status=HEYGEN_DONE |

**Связи воркфлоу 6:**
- `Webhook` → `Code in JavaScript` → `IF | Есть video_id` (true) → `IF | Видео готово` (true) → `GS | Update HeyGen URL`
- Ветки false (нет video_id или видео не готово) — не подключены

**Code in JavaScript (Workflow 6):**
```javascript
const body = $json.body || $json;
const eventData = body.event_data || {};
return [{
  json: {
    raw_body: body,
    event_type: body.event_type || '',
    video_id: eventData.video_id || '',
    callback_id: eventData.callback_id || '',
    status: body.event_type === 'avatar_video.success' ? 'success' : '',
    video_url: eventData.url || '',
    share_url: eventData.video_share_page_url || '',
    error_message: body.message || body.error || ''
  }
}];
```

**GS | Update HeyGen URL:**
- Операция: update
- matchingColumn: row_number = `Number($json.callback_id)`
- heygen_video_url = `$json.video_url`
- updated_at = `new Date().toLocaleString('ru-RU')`
- status = `HEYGEN_DONE`
- callback_id (строка) преобразуется в число через Number() для совпадения с числовым row_number в Sheets

**Что проверять у студента:**

*Воркфлоу 5 (Generate Video):*
1. Manual Trigger как точка входа
2. `GS | Get Videos` читает лист «Videos» (gid=901834362)
3. `IF | Ready For HeyGen` проверяет 3 условия AND: action_send_heygen==true; heygen_video_url пусто; script_doc_url не пусто
4. `FLOW | Batch HeyGen` (splitInBatches) — обрабатывает по одному видео
5. `DRIVE | Download Script Doc` скачивает документ как text/plain по URL из script_doc_url
6. `DRIVE | Extract Script Text` извлекает текст в поле script_text
7. `SCRIPT | Parse Doc` (Code) парсит секции Заголовок, Сценарий, CTA через indexOf; результат: final_script
8. `GS | Get HeyGen Settings` читает лист «Settings» (range A1:F2) — получает avatar_id, orientation
9. `FLOW | Merge Video + Settings` объединяет данные сценария и настроек HeyGen
10. `HTTP | HeyGen Create Video` — POST к HeyGen API; тело содержит prompt (final_script), avatar_id, orientation, callback_url, callback_id (= row_number как строка)
11. `CODE | Normalize HeyGen Response` извлекает heygen_video_id из ответа; сбрасывает action_send_heygen=false
12. `GS | Mark HeyGen Processing` — режим appendOrUpdate, matchBy video_id, status=SENT_TO_HEYGEN
13. Цикл возвращается к `FLOW | Batch HeyGen`

*Воркфлоу 6 (Получаем видео):*
1. `Webhook` принимает callback от HeyGen по пути e8750122-5f63-41ec-85cd-af30a43e14e3
2. `Code in JavaScript` парсит body webhook: извлекает event_type, video_id, callback_id, video_url, share_url
3. `IF | Есть video_id` — проверяет что video_id не пустой (фильтр нерелевантных событий)
4. `IF | Видео готово` — проверяет event_type == 'avatar_video.success'
5. `GS | Update HeyGen URL` — режим update; matchBy row_number = Number($json.callback_id); записывает heygen_video_url и status=HEYGEN_DONE
6. callback_id приходит как строка — обязательно приводить к числу через Number() для поиска по row_number

**Типичные ошибки:**
- `IF | Ready For HeyGen` не все три условия AND — воркфлоу запускает видео повторно или пропускает нужные
- `DRIVE | Download Script Doc` скачивает не в text/plain — текст не извлекается
- `SCRIPT | Parse Doc` неверно парсит секции (неправильные метки или порядок) — final_script пустой
- `GS | Get HeyGen Settings` читает неправильный диапазон — avatar_id или orientation отсутствуют
- `FLOW | Merge Video + Settings` входы перепутаны (input[0] и input[1]) — данные не в том порядке
- В `HTTP | HeyGen Create Video` callback_id не обёрнут в String() — число не превращается в строку
- `GS | Mark HeyGen Processing` режим не appendOrUpdate, а update/append — при первом запуске ошибка
- В воркфлоу 6 `callback_id` не приводится к числу через Number() — matchBy не находит строку
- Нет `IF | Есть video_id` — воркфлоу падает при служебных событиях HeyGen без video_id
- Нет `IF | Видео готово` — URL записывается даже для незавершённых или ошибочных статусов
- Webhook path не совпадает с callback_url в воркфлоу 5 — callbacks не доходят

---

### Фабрика клонов — Урок 30 (двухворкфлоуная система публикации на YouTube)

**Тема:** Двухворкфлоуная архитектура публикации: Воркфлоу 7.1 строит очередь публикации (Publish Queue Builder), Воркфлоу 7.2 запускает публикацию на YouTube по расписанию (YT Publish Runner).

---

#### Воркфлоу 7.1 — Publish Queue Builder (5 нод)

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `Google Sheets Trigger` | googleSheetsTrigger v1 | rowUpdate; sheet «Videos» gid=901834362; columnsToWatch: action_publish, status, pub_youtube, pub_vk, pub_instagram |
| `GS \| Get Settings` | googleSheets v4.7 | read; sheet «Settings» gid=2046567203; range A1:J2; executeOnce: true |
| `GS \| Get Videos For Queue` | googleSheets v4.7 | read; sheet «Videos» gid=901834362; filter: action_publish==true AND status==HEYGEN_DONE; executeOnce: true |
| `CODE \| Build Publish Queue` | code v2 | JS: читает period из Settings, вычисляет scheduled publish_after с интервалом periodHours |
| `GS \| Update Publish Queue` | googleSheets v4.7 | update; matchBy: row_number; записывает: yt_publish_after, vk_publish_after, instagram_publish_after, updated_at |

**Связи 7.1:**
`Google Sheets Trigger` → `GS | Get Settings` → `GS | Get Videos For Queue` → `CODE | Build Publish Queue` → `GS | Update Publish Queue`

**Логика CODE | Build Publish Queue:**
- Читает period из листа Settings
- Фильтрует видео: action_publish==true AND нужна публикация хотя бы на одну платформу (pub_youtube/pub_vk/pub_instagram == true AND статус != DONE)
- Сортирует по row_number
- Назначает дату: now + index * periodHours * 3600 * 1000
- Если платформа уже DONE — берёт существующее значение (не перезаписывает)
- Форматирует дату в московское время (Europe/Moscow)

---

#### Воркфлоу 7.2 — YT Publish Runner (13 нод)

| Нода | Тип | Ключевые параметры |
|---|---|---|
| `TRIGGER \| Every 5 min` | scheduleTrigger v1.3 | interval: field=minutes (каждую минуту, несмотря на название) |
| `Get row(s) in sheet` | googleSheets v4.7 | read; filter: action_publish==true AND status==HEYGEN_DONE; executeOnce: true |
| `CODE \| Pick Due Video` | code v2 | парсит yt_publish_after как МСК время, выбирает один просроченный видео |
| `IF \| Has Due Video` | if v2.3 | strict: `$input.all().length > 0` |
| `IF \| Need YouTube Publish` | if v2.3 | AND: pub_youtube==true AND status_youtube != 'DONE' |
| `GD \| Get Script Doc` | googleDocs v2 | get; documentURL извлекается regex из script_doc_url |
| `MERGE \| Row + Script Doc` | merge v3.2 | combineByPosition; input[0]=GD Get Script Doc, input[1]=IF Need YouTube Publish |
| `CODE \| Parse Script For YouTube` | code v2 | парсит content из Google Doc: Заголовок, Оригинал, Сценарий, CTA |
| `HTTP \| Download HeyGen Video` | httpRequest v4.4 | GET heygen_video_url; responseFormat: file |
| `YT \| Upload Short` | youTube v1 | upload; title=youtube_title; categoryId=22; regionCode=RU; privacyStatus=public; onError: continueErrorOutput |
| `MERGE \| Row + YouTube Result` | merge v3.2 | success path: input[0]=YT Upload, input[1]=CODE Parse Script |
| `Merge` | merge v3.2 | error path: input[0]=YT Upload error, input[1]=CODE Parse Script |
| `GS \| Mark YouTube Done` | googleSheets v4.7 | update; matchBy: row_number; status_youtube=DONE; url_youtube='https://youtube.com/shorts/' + uploadId |
| `GS \| Mark YouTube Error` | googleSheets v4.7 | update; matchBy: row_number; status_youtube=ERROR; url_youtube="" |

**Связи 7.2:**
- `TRIGGER | Every 5 min` → `Get row(s) in sheet` → `CODE | Pick Due Video` → `IF | Has Due Video` (true) → `IF | Need YouTube Publish`
- `IF | Need YouTube Publish` (true) → `GD | Get Script Doc` → `MERGE | Row + Script Doc` (input[0])
- `IF | Need YouTube Publish` (true, параллельно) → `MERGE | Row + Script Doc` (input[1])
- `MERGE | Row + Script Doc` → `CODE | Parse Script For YouTube`
- `CODE | Parse Script For YouTube` → `HTTP | Download HeyGen Video` (и → `MERGE | Row + YouTube Result` input[1]; и → `Merge` input[1])
- `HTTP | Download HeyGen Video` → `YT | Upload Short`
- `YT | Upload Short` output[0] → `MERGE | Row + YouTube Result` (input[0]) → `GS | Mark YouTube Done`
- `YT | Upload Short` output[1] → `Merge` (input[0]) → `GS | Mark YouTube Error`

**GD | Get Script Doc — ключевое выражение:**
```
documentURL = "={{ ($json.script_doc_url || '').match(/\/document\/d\/([^/]+)/)?.[1] }}"
```

**CODE | Parse Script For YouTube — структура:**
- Извлекает блоки из текста Google Doc по меткам: Заголовок, Оригинал, Сценарий, CTA
- youtube_title = title || original_title || 'Untitled'
- youtube_description = cta || ''
- Возвращает: script_title, script_original, script_body, script_cta

**CODE | Pick Due Video — логика парсинга дат:**
- Формат 1: YYYY-MM-DD H:mm → конвертация из МСК в UTC (вычитание 3 часов)
- Формат 2: DD.MM.YY(YY) H:mm → конвертация из МСК в UTC (вычитание 3 часов)
- Фильтрует: needsPublishing AND yt_publish_after <= now
- Берёт только ОДИН (ранний) просроченный видео

**Что проверять у студента (оба воркфлоуа):**

Воркфлоу 7.1:
1. Google Sheets Trigger настроен на sheet «Videos», columnsToWatch включают action_publish и/или status
2. Нода чтения Settings подключена к правильному листу (Settings)
3. Нода чтения Videos фильтрует по action_publish==true AND status==HEYGEN_DONE
4. CODE нода вычисляет расписание с интервалом из поля period
5. Update нода пишет yt_publish_after (и vk/instagram_publish_after) с matchBy: row_number

Воркфлоу 7.2:
1. Триггер по расписанию (каждую минуту или несколько минут)
2. Чтение Videos с фильтром action_publish==true AND status==HEYGEN_DONE
3. CODE | Pick Due Video корректно парсит дату в формате МСК и выбирает один просроченный видео
4. IF проверяет наличие просроченного видео (length > 0)
5. IF проверяет необходимость публикации на YouTube (pub_youtube==true AND status_youtube != DONE)
6. GD | Get Script Doc извлекает ID документа из URL через regex
7. Merge объединяет данные строки и содержимое Google Doc
8. CODE | Parse Script For YouTube корректно парсит блоки (Заголовок, Сценарий, CTA)
9. HTTP скачивает видео по heygen_video_url; responseFormat: file
10. YT | Upload Short настроен с onError: continueErrorOutput (две ветки: success и error)
11. success-ветка: MERGE + GS Mark YouTube Done (status_youtube=DONE, url_youtube с uploadId)
12. error-ветка: MERGE + GS Mark YouTube Error (status_youtube=ERROR)
13. matchBy: row_number в обеих нодах обновления GS — дедупликация по строке

**Типичные ошибки:**
- Воркфлоу 7.1: period не читается из Settings, вычисление дат не учитывает уже опубликованные платформы
- Воркфлоу 7.2: нет парсинга МСК-даты (студент использует стандартный Date.parse без учёта часового пояса)
- Нет двух веток (success/error) у YT | Upload Short — onError не выставлен
- matchBy row_number отсутствует в нодах обновления GS — обновляется не та строка
- GD | Get Script Doc не использует regex для извлечения doc ID из URL
- CODE | Parse Script For YouTube не разбирает структуру Google Doc (нет блоков Заголовок/Сценарий/CTA)
- Merge nodes перепутаны: success-данные уходят в error-ветку и наоборот
- HTTP | Download HeyGen Video не настроен responseFormat: file — загрузка видео не работает
