# Лицо в кадре — как держать своё лицо (identity-lock)

Памятка под слайды/обложки с вашим лицом. Движок лица — **Image 2 (gpt-image-2, в Codex)**: по тесту он держит лицо, Flux-reference — нет, nano-banana-pro умеет, но с возни. Постоянное своё лицо «на потоке» (пачки контента) — это обучение модели (Flux LoRA / Soul ID), отдельный путь Урока 2; одиночный фото-референс его не заменяет.

## 1. Роли референсов
В промте явно скажи модели, ЧТО за фото ты дал:
- загруженные фото — это **identity-референсы (только лицо)**, не копировать их фон/одежду/позу;
- если есть отдельное фото-стиль — пометь `style reference only, do not copy the face`.

## 2. Полный landmark-lock (перечисляй, не «тот же человек»)
Общее «same person» модель усредняет. Перечисляй неизменяемые черты:
`face shape, facial proportions, bone structure, eye shape and spacing, eyelids, brow, nose bridge, nose tip, nostrils, cheekbones, jawline, chin, mouth shape, lips, smile lines, skin tone, natural skin texture, hairline, hairstyle outline, facial hair, moles, freckles, scars, natural asymmetry` → `SAME exact person, instantly recognizable`.

## 3. Анти-усреднение (иначе модель «улучшит» тебя в незнакомца)
**НЕ ставь голое `no beautification`** — на фотореализме оно читается как «не сглаживай» и СТАРИТ лицо. Ставь:
`no over-beautified influencer face`, `no plastic/waxy skin`, и явный запрет дрейфа:
`do NOT make the person younger / more generic / more symmetrical / more handsome — keep the real face`.
Кожа: `natural skin texture with visible pores, subtle asymmetry, believable imperfections`.

## 4. Структура промта лица
`Image roles → Identity lock (landmark list) → Realism → Change (что меняем: сцена/свет/одежда) → Constraints (запреты дрейфа)`. Identity-блок НЕ меняется от кадра к кадру — меняется только сцена.

## 5. Эталонный identity-блок (вставлять вместе с описанием сцены)

```text
IMAGE ROLES: The uploaded photos are IDENTITY REFERENCES ONLY of the same real person. Use them strictly to reproduce the exact face and head; do NOT copy their backgrounds, outfits, lighting or poses.
IDENTITY LOCK: face shape, facial proportions, bone structure, eye shape and spacing, eyelids, brow, nose bridge, nose tip, nostrils, cheekbones, jawline, chin, mouth shape, lips, smile lines, skin tone, natural skin texture, hairline, hairstyle outline, facial hair, moles, freckles, scars, natural asymmetry. SAME exact person, instantly recognizable.
REALISM: real photograph, natural skin texture with visible pores, subtle asymmetry, believable imperfections, realistic hair. NO plastic or waxy skin, NO airbrushing, NO over-beautified influencer face, NO anime, NO CGI.
CONSTRAINTS: do NOT make the person younger, more generic, more symmetrical, more glamorous or more handsome; keep the real face exactly. No extra people, no text, no watermark, no distorted eyes, no face-swap artifacts.
```

Подавай 3–6 чистых фото лица (разные ракурсы: фронт / три четверти / профиль), без фильтров и тяжёлого макияжа.

## 6. Несколько вариантов + отбраковка — это норма
Лицо с первого кадра может «уплыть» — не провал, а часть процесса: **сгенерируй несколько → отбракуй по landmark → перегенерируй**. Не гони серию цепочкой из уже-сгенерированных кадров (артефакты копятся) — возвращайся к исходным фото. Для серии — сначала сделай «лист-эталон» (несколько ракурсов одного лица) и подавай его референсом.

## 7. Размеры под лицо
- Image 2 / Codex вертикаль = **максимум 2:3 (1024×1536)**.
- Ровное **4:5** ленты — кропни кадр Image 2 или генери через nano-banana-pro (`aspect_ratio: "4:5"`).
- Настоящий **9:16** — только через OpenAI API напрямую: **1152×2048** или **1440×2560** (сторона кратна 16; «1080×1920» API отвергнет).
- Лицо при любом формате ведёт **Image 2** — кропим его кадр, движок лица не меняем.

*Меняющиеся числа (размеры, лимиты, цены) сверяй с актуальными доками на день работы.*
