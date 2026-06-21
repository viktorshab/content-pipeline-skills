# Upgrade Report v2026.06

## Что было доработано

1. `content-pipeline` перестроен в source-first оркестратор.
   - Добавлены source brief, claim ledger, proof ledger, VOC ledger, forbidden assumptions, freshness check и angle map.
   - Добавлен stop-gate перед финальной генерацией.
   - Добавлена финальная QA-логика.

2. `reels-scriptwriter` переписан полностью.
   - Убрана привязка к нише "обучение нейронкам".
   - Добавлены режимы Reels, TikTok, Shorts и multi-platform.
   - Добавлены length modes: 7-12 sec, 20-45 sec, 60-180 sec.
   - Добавлены Hook Lab, retention map, on-screen text, visual action, cut/movement и sound cue.

3. `email-sequence-writer` переписан полностью.
   - Убрана жесткая схема "5 писем всегда".
   - Добавлены режимы: single value email, 3-email bridge, 5-email launch, welcome nurture, event follow-up, re-engagement.
   - Убраны прогнозы open rate.
   - Добавлен deliverability gate.

4. `carousel-builder` усилен.
   - Добавлены saveable-архетипы.
   - Добавлен stop-gate перед генерацией картинок.
   - Добавлен engine passport вместо жестких названий моделей и цен.
   - Обновлены правила identity-lock.

5. Добавлены новые reference-файлы.
   - `source-intelligence.md`
   - `hook-lab-2026.md`
   - `platform-playbooks-2026.md`
   - `quality-gates.md`
   - `freshness-sources-2026.md`
   - `06-engine-passport.md`
   - `08-saveable-strategy.md`

6. Обновлен учебный пример.
   - Добавлены `source-brief.md`, `hook-lab.md`, `qa-report.md`.
   - Исправлено обращение и род: мужской род по умолчанию заменен на нейтральный или женский, где это уместно.
   - Добавлены platform-native версии поста, треда, Reels, Telegram и email.

## Что теперь умеет пакет

- Делать контент не "из головы", а из проверенной карты источника.
- Разделять факты, мнения, VOC, proof и assumptions.
- Создавать разные форматы под разные площадки, а не копировать один текст.
- Генерировать больше и лучше хуков через Hook Lab.
- Писать письма с учетом доверия, сегмента, CTA и доставляемости.
- Проектировать короткое видео как visual-first сценарий.
- Делать карусели с причиной для сохранения.
- Отмечать риски и факты, которые нужно проверить человеку.

## Что осталось на человеке

- Проверить текущие правила платформ перед записью урока.
- Проверить claims в health/finance/legal/medical нишах.
- Выбрать и подтвердить image-движок.
- Утвердить стоп-гейты.
- Публиковать и отправлять письма только вручную.
