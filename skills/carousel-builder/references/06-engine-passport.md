# Engine Passport

Этот файл нужно проверять перед генерацией картинок. Модели, названия, цены, лимиты, aspect ratios и возможности быстро меняются. Не прошивай эти данные в SKILL.md как вечную истину.

Verified at: 2026-06-21.
Status: template. Перед уроком или продакшеном обновить под текущий стек.

## Как заполнять

```markdown
## Engine: <name>
- Provider:
- Access path: ChatGPT / API / Codex / Replicate / local / other
- Supports text rendering: yes/no/partial
- Supports Cyrillic text: yes/no/partial
- Supports reference images: yes/no/partial
- Supports image edit: yes/no/partial
- Supports multiple references: yes/no/partial
- Best for: face / product / background / typography / illustration / photoreal
- Aspect ratios:
- Output sizes:
- Cost note:
- Limits note:
- Verified at:
- Verification source:
- Risks:
```

## Decision rule

### Use image-text mode when

- текст короткий;
- движок надежно держит кириллицу;
- важнее дизайн внутри кадра, чем пиксельная типографика;
- правок немного.

### Use code-text mode when

- текст должен быть точным;
- нужен брендовый шрифт;
- есть много правок;
- важно одинаковое расположение текста;
- image engine плохо держит буквы.

### Use text-only fallback when

- image engine не подключен;
- лимит исчерпан;
- нет подтвержденного engine passport;
- пользователь пока утверждает логику.

## Safe areas

Для social assets всегда проверяй:

- 4:5 feed: не ставить ключевой текст у краев;
- 9:16 video/story: учитывать UI сверху и снизу;
- 1:1: текст крупнее, меньше строк;
- 16:9: не перегружать центр, если превью будет маленьким.

## Prompt contract

Каждый prompt должен включать:

- format and aspect ratio;
- scene;
- composition;
- text zone;
- exact text, если image-text mode;
- style anchor;
- reference images list;
- identity-lock, если лицо/товар;
- negative constraints;
- output naming.

## Never do

- не указывать устаревшую цену как факт;
- не обещать, что один движок всегда лучше другого;
- не менять лицо ради "улучшения";
- не генерировать картинки до stop-gate;
- не продолжать image generation, если пользователь просил только текстовый план.
