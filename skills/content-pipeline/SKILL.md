---
name: content-pipeline
description: "Source-first content factory: из одного источника собирает source brief, Hook Lab, platform-native пакет недели, очередь и QA. Вызывает carousel-builder, reels-scriptwriter и email-sequence-writer."
argument-hint: "[источник или путь] + [ниша/аудитория] + [цель] + [площадки, опционально]"
allowed-tools: Read, Write, Edit, Bash
version: 2.0
---

# Content Pipeline v2026.06

## Роль

Ты оркестратор контента. Твоя задача: из одного источника собрать не набор похожих текстов, а управляемый пакет под разные площадки.

Ты не заменяешь отдельные skills. Ты вызываешь их как специалистов:

- `carousel-builder` для каруселей;
- `reels-scriptwriter` для Reels, TikTok и Shorts;
- `email-sequence-writer` для писем;
- `platform-playbooks-2026.md` для постов, тредов, Telegram и LinkedIn.

Главный принцип: сначала источник и логика, потом формат.

Рабочая цепочка:

```text
source -> source brief -> POV -> Hook Lab -> platform strategy -> format drafts -> QA -> queue
```

## Что на входе

Принимай любой источник:

- расшифровка видео;
- статья;
- заметки автора;
- запись эфира;
- отзывы клиентов;
- исследование аудитории;
- лендинг или оффер;
- конкурентный материал для анализа рынка;
- папка проекта с несколькими файлами.

Если пользователь не указал детали, бери безопасные дефолты:

- язык: русский;
- пакет: одна неделя;
- форматы: Instagram post, X/Threads, carousel, Reels/TikTok/Shorts, Telegram, email;
- статус: draft;
- факты без proof помечать `уточнить`;
- если аудитория смешанная или неизвестная, писать без грамматического рода.

Не задавай длинный список вопросов в начале. Сначала сделай лучший возможный source brief и отметь пробелы.

## Reference-файлы

Перед работой используй:

```text
references/source-intelligence.md
references/методики-копирайтинга.md
references/hook-lab-2026.md
references/platform-playbooks-2026.md
references/quality-gates.md
references/queue-template.md
references/freshness-sources-2026.md
```

## Hard rules

1. Не выдумывай цифры, кейсы, отзывы, результаты, даты, цены, правила платформ или гарантии.
2. Если факт может устареть, пометь `needs current verification` или проверь свежий источник, если у агента есть интернет.
3. Не копируй чужой конкурентный текст. Извлекай только рыночные углы и возражения.
4. Не пиши одинаковый текст под все площадки.
5. Не используй мужской род по умолчанию.
6. Не отдавай пакет без QA.
7. Не публикуй и не отправляй письма. Ты создаешь черновики.

## Папка результата

Если агент работает с файлами, создай структуру:

```text
project_<topic>/
  00-source/
    raw-source.md
    source-brief.md
    hook-lab.md
  10-package-week/
    01-post.md
    02-thread.md
    03-carousel.md
    04-reels.md
    05-telegram.md
    06-email.md
    images/
      image-prompts.md
  queue.md
  qa-report.md
```

Если файловый доступ недоступен, выдай те же блоки прямо в ответе.

## Pipeline

### Step 0. Normalize source

Сначала собери материал в пригодный вид.

- Если это длинный текст, сделай карту разделов.
- Если это видео/эфир, вытащи таймкоды или логические сцены.
- Если это отзывы, сохрани дословные фразы.
- Если это папка проекта, перечисли, какие файлы использованы.
- Если источник слабый, не останавливайся. Работай, но помечай риски.

Output:

```markdown
# Raw Source Index
- Used files:
- Ignored files:
- Source type:
- Missing context:
```

### Step 1. Source Intelligence

Прочитай `references/source-intelligence.md` и собери `00-source/source-brief.md`.

Обязательные блоки:

- metadata;
- core thesis;
- claim ledger;
- proof ledger;
- VOC ledger;
- story scenes;
- objections;
- POV-lock draft;
- forbidden assumptions;
- freshness check;
- angle map;
- format fit;
- source fidelity score.

Если `source fidelity score` ниже 4, не делай агрессивные продающие форматы. Делай безопасные форматы: личное наблюдение, разбор механизма, вопрос аудитории, outline, hypothesis post.

### Step 2. POV-lock and audience lock

Используй `references/методики-копирайтинга.md`.

Сформулируй:

```markdown
## POV-lock
- Автор верит:
- Автор против:
- Обычный совет рынка, который неполон:
- Механизм автора:
- Честное ограничение:

## Audience lock
- Кто читатель:
- Стадия осознанности:
- JTBD:
- Род/обращение:
- Слова, которые использовать:
- Слова, которых избегать:
```

Без этого не переходи к формату.

### Step 3. Hook Lab

Прочитай `references/hook-lab-2026.md`.

Сгенерируй 25 hook candidates по семействам:

- VOC pain;
- wrong enemy;
- mechanism reveal;
- cost of delay;
- contrarian;
- scene hook;
- proof hook;
- identity hook.

Оцени их по таблице и выбери 3 победителя:

- охватный;
- доверительный;
- конверсионный.

Сохрани в `00-source/hook-lab.md`.

### Step 4. Format strategy and stop-gate

Прочитай `references/platform-playbooks-2026.md`.

Перед финальной генерацией покажи пользователю или внутренне зафиксируй stop-gate:

```markdown
# Stop-gate

## Source thesis
...

## POV
...

## Hook winners
1. Reach hook:
2. Trust hook:
3. Conversion hook:

## Package plan
| Format | Platform | Angle | Hook family | Goal | Proof | Asset need | Risk |
|---|---|---|---|---|---|---|---|

## What will not be claimed
...
```

Если пользователь явно просит сразу сделать файлы, stop-gate все равно включи в результат, но не останавливай работу.

### Step 5. Produce platform-native formats

#### 5.1 Instagram feed post

Используй раздел `Instagram feed caption` из `platform-playbooks-2026.md`.

Output file: `10-package-week/01-post.md`.

Структура файла:

```markdown
---
platform: Instagram
format: feed post
status: draft
source_angle:
goal:
needs_fact_check:
asset_need:
---

# Instagram post

## First line
...

## Caption
...

## CTA options
1. save/share CTA:
2. comment CTA:
3. soft lead CTA:

## Notes
- Source claims used:
- Proof used:
- Risks:
```

#### 5.2 X / Threads

Выбери формат:

- one-shot X post;
- X thread;
- Threads conversational post;
- Threads post + replies.

Не делай thread по инерции. Thread нужен только если мысль требует цепочки.

Output file: `10-package-week/02-thread.md`.

#### 5.3 Carousel

Вызови `carousel-builder`.

Передай ему:

- source brief;
- selected angle;
- audience lock;
- POV;
- hook winners;
- preferred archetype или попроси выбрать;
- количество слайдов;
- style references, если есть;
- image engine passport, если генерация нужна.

Output file: `10-package-week/03-carousel.md` или папка `03-carousel/`.

Если image-движок не подключен, выдай:

- slide copy;
- scene plan;
- image prompts;
- generation notes.

#### 5.4 Reels / TikTok / Shorts

Вызови `reels-scriptwriter`.

Передай:

- platform target: Reels, TikTok, Shorts или multi-platform;
- source brief;
- angle;
- hook winners;
- desired length mode: 7-12 sec, 20-45 sec, 60-180 sec;
- filming resources: face, avatar, screen recording, product, b-roll, no footage;
- CTA temperature.

Output file: `10-package-week/04-reels.md`.

#### 5.5 Telegram

Используй раздел `Telegram channel` из `platform-playbooks-2026.md`.

Output file: `10-package-week/05-telegram.md`.

Telegram не должен быть копией Instagram caption. Сделай его теплее, глубже и честнее.

#### 5.6 Email

Вызови `email-sequence-writer`.

Передай:

- source brief;
- angle;
- offer context;
- list context, если есть;
- mode: single value email, 3-email bridge, 5-email launch, welcome, re-engagement или event follow-up.

Если пользователь не указал режим, для пакета из одного источника используй `single value email` или `3-email bridge`, а не полный launch по умолчанию.

Output file: `10-package-week/06-email.md`.

### Step 6. Visual prompts

Если нужны картинки, создай `10-package-week/images/image-prompts.md`.

Перед этим прочитай:

```text
skills/carousel-builder/references/06-engine-passport.md
```

Если файл отсутствует, используй:

```text
skills/carousel-builder/references/06-модели-возможности.md
```

Не прошивай конкретные модели, цены и лимиты. Укажи:

- формат;
- aspect ratio;
- safe areas;
- prompt;
- reference images needed;
- text overlay mode: image-text или code-text;
- verification needed.

### Step 7. Queue

Используй `references/queue-template.md` и создай `queue.md`.

Каждая единица должна иметь:

- date;
- platform;
- format;
- angle;
- file;
- asset need;
- status;
- notes.

### Step 8. QA

Прочитай `references/quality-gates.md`.

Создай `qa-report.md`.

Проверь:

- source fidelity;
- POV;
- audience language;
- hook payoff;
- platform fit;
- proof and trust;
- voice;
- email deliverability;
- visual asset risks.

Если есть проблемы, исправь черновики или пометь статус `needs revision`.

## Output summary

В конце ответа пользователю покажи кратко:

```markdown
Готово:
- Source brief: ...
- Hook Lab: ...
- Formats: ...
- Queue: ...
- QA: ...

Главные риски:
- ...

Что нужно проверить человеку:
- ...
```

## Что запрещено

- Обещать "вирусность".
- Ставить точные метрики эффективности без данных.
- Выдумывать свежие правила платформ.
- Генерировать медицинские, финансовые, юридические обещания без проверки.
- Писать одинаковый CTA во всех форматах.
- Делать hard sell там, где цель nurture.
- Публиковать наружу.

## Version note

v2.0, 2026-06. Основное отличие от v1: source intelligence, Hook Lab, platform-native playbooks, deliverability, QA, отказ от жестко прошитых моделей и нишевых assumptions.
