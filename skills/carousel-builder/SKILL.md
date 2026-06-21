---
name: carousel-builder
description: "Собирает saveable-карусель или сторис из источника, source brief или темы: выбирает архетип, строит slide ladder, пишет короткие тексты, планирует сцены, готовит image prompts или HTML/CSS fallback."
argument-hint: "[source brief/тема/текст] + [число слайдов] + [стиль/референсы, опционально]"
allowed-tools: Read, Write, Edit, Bash
version: 2.0
---

# Carousel Builder v2026.06

## Роль

Ты собираешь карусель, которую хочется досвайпать, сохранить или отправить. Это не PowerPoint и не пересказ статьи по слайдам. Это визуальная аргументация: каждый слайд двигает мысль вперед.

Ты работаешь в двух слоях:

1. Copy and structure: angle, hook, slide ladder, saveability, CTA.
2. Visual direction: сцены, layout, style anchor, identity-lock, prompts or code layout.

## Главный принцип

Карусель должна иметь причину быть каруселью.

Если мысль лучше работает как один пост, не растягивай ее на 7 слайдов. Если карусель нужна, выбери архетип и сделай полезный артефакт.

## Вход

Принимай:

- тему;
- короткий текст;
- source brief;
- статью или расшифровку;
- список тезисов;
- отзыв клиента;
- оффер;
- фото лица, товара или стиля;
- бренд-файл.

Дефолты:

- 7 слайдов;
- русский язык;
- формат 4:5 для ленты;
- image-text mode, если движок поддерживает текст;
- code-text fallback, если нужна точная типографика;
- если аудитория смешанная или неизвестная, писать без рода.

## Reference-файлы

Используй:

```text
references/01-text-phase.md
references/02-styles.md
references/03-director.md
references/04-image-prompt.md
references/05-text-as-code.md
references/06-engine-passport.md
references/07-лицо-identity.md
references/08-saveable-strategy.md
```

Если `06-engine-passport.md` отсутствует, используй `06-модели-возможности.md` как совместимый fallback.

## Hard rules

1. Не выдумывать claims, цифры, кейсы и результаты.
2. Cover не должен быть просто названием темы.
3. Один слайд = одна мысль.
4. Нельзя ставить 4 абзаца на слайд.
5. Последний слайд должен давать артефакт, вывод или следующий шаг, а не только "подпишись".
6. Перед генерацией картинок всегда stop-gate: текст, архетип, сцены, движок, количество картинок.
7. Если image-движок недоступен, не останавливайся. Выдай текст слайдов, сцены, prompts и layout notes.
8. Если есть лицо или товар, используй identity-lock и не меняй узнаваемые признаки.

## Step 1. Source and angle

Если пришел source brief, возьми из него:

- core thesis;
- claim ledger;
- proof ledger;
- VOC ledger;
- POV;
- forbidden assumptions;
- best angle.

Если пришла только тема, собери мини-brief:

```markdown
## Mini carousel brief
- Audience:
- Main pain:
- Core thesis:
- Proof available:
- POV:
- Cannot claim:
- Desired action:
```

## Step 2. Choose carousel archetype

Прочитай `references/08-saveable-strategy.md`.

Выбери один архетип:

1. Checklist.
2. Myth vs reality.
3. Decision tree.
4. Before / after / bridge.
5. Teardown.
6. Swipe lesson.
7. Proof carousel.
8. Script / template.

Для выбранного архетипа сформулируй:

```markdown
## Archetype
- Selected archetype:
- Why this fits the source:
- Save reason:
- Screenshot slide:
- Final artifact:
```

## Step 3. Hook and slide ladder

Сначала придумай 10 cover hooks или используй Hook Lab winners от `content-pipeline`.

Выбери лучший cover по критериям:

- recognition;
- tension;
- specificity;
- payoff honesty;
- visual potential.

Потом собери slide ladder:

```markdown
| Slide | Job | Headline | Subtext | Proof/VOC | Visual idea | Saveability role |
|---|---|---|---|---|---|---|
```

Типовая лестница:

1. Cover: tension.
2. Context: человек узнает себя.
3. Wrong enemy: почему старый подход не работает.
4. Mechanism: что реально происходит.
5. Proof or example: показать на конкретике.
6. Diagnostic check or template: практический слайд.
7. Final: next step, checklist, CTA или summary.

Если слайдов больше, расширяй mechanism, proof, example или template. Не добавляй воду.

## Step 4. Stop-gate before images

Перед генерацией картинок выдай:

```markdown
# Carousel Stop-gate

## Source angle
...

## Archetype
...

## Slides
| # | Headline | Subtext | Visual scene | Notes |
|---|---|---|---|---|

## Image generation plan
- Mode: image-text / code-text / text-only
- Engine passport checked: yes/no
- Slides count:
- Aspect ratio:
- Reference images needed:
- Risks:
```

Если пользователь явно просит сразу сделать файлы, включи stop-gate как первый блок результата и продолжай.

## Step 5. Copywriting

Короткий текст. Слайд должен считываться за 1-2 секунды.

Рекомендации:

- headline: до 7-10 слов;
- subtext: 1-2 короткие строки;
- один смысл на слайд;
- не использовать одинаковые начала;
- не дублировать headline в subtext;
- сохранять голос автора;
- род и обращение по аудитории.

Пиши так, чтобы headline и visual scene работали вместе.

## Step 6. Visual direction

Прочитай `references/03-director.md` и `references/02-styles.md`.

На каждый слайд дай:

- subject;
- environment;
- camera angle;
- composition;
- lighting;
- layout zone for text;
- style continuity;
- what changes from previous slide.

Карусель должна быть единым набором, но не набором одинаковых кадров.

## Step 7. Text rendering mode

Выбери режим.

### Mode A. Image-text

Image-модель рисует текст внутри кадра.

Использовать, если:

- движок надежно держит кириллицу;
- нужен дизайнерский кадр;
- текст короткий;
- небольшие ошибки можно перегенерировать.

### Mode B. Code-text

Фон или иллюстрация генерируется отдельно, а текст накладывается HTML/CSS.

Использовать, если:

- текст должен быть идеально точным;
- нужен фирменный шрифт;
- есть много правок;
- студент работает в среде, где можно рендерить PNG.

### Mode C. Text-only

Если генерация недоступна, выдай:

- slide copy;
- scene descriptions;
- prompts;
- layout notes;
- QA.

## Step 8. Engine passport

Перед image generation прочитай `references/06-engine-passport.md`.

Проверь:

- current engine name;
- supports text rendering;
- supports reference images;
- supports edit;
- aspect ratios;
- safe areas;
- limits and cost note;
- verified_at.

Если данные старше 30 дней, пометь `needs current verification`.

Не прошивай конкретную модель как вечную истину.

## Step 9. Identity-lock

Если пользователь дал фото лица или товара, прочитай `references/07-лицо-identity.md`.

Правила:

- не "тот же человек" абстрактно, а признаки лица;
- не менять возраст, этничность, форму лица, волосы, мимику слишком сильно;
- не beauty-filter, если он ломает узнаваемость;
- на следующих слайдах использовать style-anchor и identity reference;
- лучше сгенерировать несколько вариантов и отбраковать слабые.

## Step 10. Output

Выдай или создай:

```markdown
# Carousel

## Strategy
- Source angle:
- Audience:
- POV:
- Archetype:
- Save reason:
- Screenshot slide:
- Final artifact:
- Mode:

## Slide copy
| # | Headline | Subtext | Notes |
|---|---|---|---|

## Scene plan
| # | Scene | Composition | Text zone | Style continuity |
|---|---|---|---|---|

## Image prompts
### Slide 01
...

### Slide 02
...

## Code-text notes, if needed
...

## CTA options
1. Save:
2. Share:
3. Lead:

## QA
- Source fidelity:
- Hook payoff:
- Saveability:
- Visual consistency:
- Risks:
```

Если генерируешь файлы, структура:

```text
03-carousel/
  carousel-plan.md
  slide-copy.md
  scene-plan.md
  image-prompts.md
  slide-01.png
  slide-02.png
  ...
```

## QA

Перед финалом проверь:

- cover не является названием темы;
- слайд 2 продолжает tension;
- каждый слайд добавляет новую мысль;
- есть proof, example или practical check;
- есть причина сохранить;
- есть screenshot slide;
- CTA не слабее и не агрессивнее температуры аудитории;
- визуал не повторяет один и тот же кадр;
- текст не перегружен;
- claims честны;
- род и обращение проверены.

## Anti-patterns

Переписать, если:

- карусель называется "5 советов" и не дает нового угла;
- каждый слайд это абзац текста;
- нет visual scene;
- последний слайд только "подпишись";
- нет save reason;
- image prompts не учитывают text zone;
- лицо/товар меняется от слайда к слайду;
- стиль каждого слайда случайный;
- карусель повторяет Instagram caption 1-в-1.
