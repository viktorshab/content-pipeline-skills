# Контент-конвейер v2026.06

Набор skills для код-агента, который превращает один источник в пакет контента под разные площадки: посты, треды, Telegram, Reels/TikTok/Shorts, карусели и письма.

Главная идея версии v2026.06: агент не просто "переписывает один текст шесть раз". Он сначала строит карту источника, отделяет факты от догадок, вытаскивает голос аудитории, формулирует POV автора, прогоняет хуки через Hook Lab и только потом пишет форматы под конкретные площадки.

## Что изменилось в этой сборке

1. Добавлен Source Intelligence Layer: `source-brief`, `claim ledger`, `proof ledger`, `VOC ledger`, `freshness check`, `angle map`.
2. Добавлен Hook Lab 2026: не три случайных хука, а 25 кандидатов, скоринг и выбор победителей под охват, доверие и конверсию.
3. `reels-scriptwriter` переписан как нишенезависимый skill для Reels, TikTok и Shorts.
4. `email-sequence-writer` переписан под современные письма: single email, 3-email bridge, 5-email launch, welcome, re-engagement, event follow-up.
5. Добавлен deliverability gate для email: один CTA, минимум ссылок, честная срочность, plain-text-first, unsubscribe reminder.
6. Добавлены platform playbooks 2026 для Instagram, X, Threads, Telegram, LinkedIn, Reels, TikTok, Shorts и email.
7. `carousel-builder` усилен saveability-логикой: архетип карусели, причина сохранить, slide-to-screenshot, финальный практический слайд.
8. Убраны жесткие зависимости от конкретных image-моделей и цен. Теперь есть engine passport, который нужно обновлять перед уроком или продакшеном.
9. Исправлено имя skill: теперь `reels-scriptwriter`, без старого snake_case имени.
10. Обновлены учебные примеры по растяжке: исправлен мужской род по умолчанию и добавлены source/hook/QA элементы.

## Что внутри

| Skill | Что делает |
|---|---|
| `content-pipeline` | Оркестратор: один источник + тема -> пакет контента, папка недели, очередь публикаций, QA. |
| `carousel-builder` | Карусель/сторис: текстовая логика, saveable-архетип, визуальная режиссура, промты, fallback в текстовый или HTML/CSS режим. |
| `reels-scriptwriter` | Сценарии Reels/TikTok/Shorts: платформа, длина, retention map, visual plan, sound/text overlays. |
| `email-sequence-writer` | Письма: single value email, 3-email mini-sequence, 5-email launch, welcome, re-engagement, event follow-up. |

Главный skill для урока: `content-pipeline`. Остальные подключаются как специалисты.

## Правильная цепочка урока

Не проси агента: "сделай 10 постов из видео".

Проси так:

```text
Из этого источника собери source brief: claims, proof, VOC, forbidden assumptions, freshness check и angle map. Потом через content-pipeline сделай пакет недели под Instagram, Reels/TikTok, Telegram и email. Не выдумывай факты. Где данных не хватает, ставь placeholder и помечай, что уточнить.
```

Рабочая цепочка:

```text
источник -> claims -> proof -> VOC -> POV -> angle map -> Hook Lab -> platform strategy -> формат -> QA -> очередь публикаций
```

## Быстрый старт

1. Скопируйте папки из `skills/` в папку skills вашего агента.
2. Откройте проект с источником: расшифровка видео, заметка, статья, эфир, аудитория, отзывы, лендинг.
3. Запустите `content-pipeline`.
4. На стоп-гейте проверьте source brief, углы и форматный план.
5. Разрешите развернуть форматы и картинки.

Подробно: `УСТАНОВКА.md`.

## Важная граница

Skills создают черновики и промты. Они не публикуют контент наружу, не нажимают кнопку отправки письма и не обещают алгоритмический результат. Финальную проверку фактов, юридических формулировок, медицинских/финансовых обещаний, оффера и публикации делает человек.
