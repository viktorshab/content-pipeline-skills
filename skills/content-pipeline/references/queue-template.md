# Шаблон папки-очереди

Очередь нужна не для автоматической публикации, а для управляемого пакета черновиков.

## Правила

- Одна единица контента = один файл текста плюс список нужных ассетов.
- Карусель хранится как отдельный `03-carousel.md` или папка `03-carousel/` со слайдами.
- Статус новых единиц всегда `draft`.
- Статус `approved` ставит только человек.
- Если факт не проверен, у единицы должен быть статус `needs fact check`.
- Если нужна картинка, укажи размер, prompt и статус генерации.

## Таблица

```markdown
| Date | Platform | Format | Angle | File | Asset need | Status | Notes |
|---|---|---|---|---|---|---|---|
| Mon | Instagram | Feed post | <angle> | 01-post.md | 4:5 cover | draft | ... |
| Tue | X / Threads | Thread or post | <angle> | 02-thread.md | optional 16:9 | draft | ... |
| Wed | Instagram | Carousel | <angle> | 03-carousel.md | slides 4:5 | draft | stop-gate before images |
| Thu | Reels / TikTok / Shorts | Short video | <angle> | 04-reels.md | 9:16 cover or first frame | draft | ... |
| Fri | Telegram | Channel post | <angle> | 05-telegram.md | optional | draft | ... |
| Sat | Email | Value email or mini-sequence | <angle> | 06-email.md | none | draft | compliance reminder |
```

## Структура папки

```text
project_<name>/
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

## Metadata в каждом файле

```markdown
---
platform:
format:
source_angle:
audience:
goal:
status: draft
needs_fact_check: false
asset_need:
---
```
