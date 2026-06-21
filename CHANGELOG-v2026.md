# Changelog v2026.06

## Главные изменения

- `content-pipeline` стал source-first: перед генерацией он обязан собрать `source-brief`, `claim ledger`, `proof ledger`, `VOC ledger`, `freshness check`, `angle map` и `format fit`.
- Добавлены новые reference-файлы:
  - `source-intelligence.md`
  - `hook-lab-2026.md`
  - `platform-playbooks-2026.md`
  - `quality-gates.md`
  - `freshness-sources-2026.md`
- `reels-scriptwriter` переписан как универсальный skill для Reels, TikTok и Shorts. Убрана жесткая ниша "нейронки".
- `email-sequence-writer` переписан под разные типы последовательностей и deliverability.
- `carousel-builder` получил saveable-архетипы и stop-gate перед генерацией картинок.
- `posts-threads-telegram.md` оставлен как совместимый указатель на новый `platform-playbooks-2026.md`.
- Исправлено старое имя snake_case имя на `reels-scriptwriter`.
- Убраны устаревающие утверждения про конкретные image-модели, цены и лимиты. Для этого добавлен engine passport.
- Учебный пример по растяжке обновлен: мужской род по умолчанию заменен на нейтральный или женский, где это нужно.

## Логика версии

Версия v2026.06 решает три проблемы, которые чаще всего ломают AI-контент:

1. Агент додумывает факты вместо работы с источником.
2. Форматы выглядят одинаково на разных платформах.
3. Тексты звучат шаблонно, потому что нет POV, proof и живого языка аудитории.

Новая цепочка:

```text
source -> source brief -> POV -> Hook Lab -> platform playbook -> format draft -> QA -> queue
```

## Что проверять перед записью урока

- Актуальность правил платформ в `freshness-sources-2026.md`.
- Актуальность image-движков в `skills/carousel-builder/references/06-engine-passport.md`.
- Наличие нужных skills в агенте.
- Работоспособность ссылок между файлами reference.
