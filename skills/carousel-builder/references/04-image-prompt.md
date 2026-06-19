# Сборка промта картинки слайда + identity-lock (дословный перенос Vibe)

> Финальный шаг: на каждый слайд собрать image-промт и вызвать движок. Текст рисует модель ВНУТРИ кадра (Вариант Б). Единство держится style-anchor'ом первого слайда + identity-lock + единым каркасом.
> Порядок сборки промта: consistency-frame → язык → формат → сцена по типу → план директора → блок референсов (identity-lock) → секция TEXT → ограничения → запреты.

---

## 1. Consistency-frame (ставится ПЕРВЫМ в каждый промт — держит единый бренд)

```
STYLE: {styleDNA из 02-styles.md}
TOPIC: {тема, до 100 символов}
VISUAL THEME (MANDATORY on every slide, overrides generic backgrounds): {1-2 конкретных визуала по теме}
THEMATIC CONSISTENCY (HARD RULE): Every slide shares the SAME background theme tied to the LITERAL topic. If about travel — every slide lives in the travel scene. If about a beach summer — every slide is a beach summer scene. NEVER pick a generic white/gradient background that ignores the subject matter. NEVER add cosmos / galaxy / starfield / planetary backgrounds unless the topic is literally about space or astronomy. The theme IS the background, drawn from the topic itself.
THIS APPLIES TO ALL SLIDES INCLUDING THE LAST (CTA) SLIDE. The CTA slide must live in the SAME visual world as slides 1-4. Never switch to a generic cafe, office, park, or unrelated "lifestyle" setting on the final slide.
CONSISTENCY: Same fonts, color accents, and background mood across all slides. Text always high-contrast and readable.
```

## 2. Язык текста (для русского — дословно)

```
Use Russian language for all text. Render exact Russian text verbatim with correct Cyrillic spelling.
```
(украинский: `Use Ukrainian Cyrillic text verbatim. Correct Ukrainian letters.`)

## 3. Формат холста

Тут две разные вещи, их легко перепутать:

- **В ТЕКСТ промта** идёт словесное описание пропорций. Для ленты — строка `Vertical 4:5 format for Instagram feed posts` (берётся из `ASPECT_RATIO_DESCRIPTION`). Для сторис — `Tall 9:16 format for Stories/Reels — leave top 14% and bottom 20% clear of critical text` (safe-зоны под интерфейс сторис обязательно оставить).
- **Размер итогового кадра** — это отдельный параметр `size` в вызове движка, НЕ часть текста промта. Для 4:5 выходной кадр = **1080×1350 px** (из `AR_DIMENSIONS`); для 9:16 = 1080×1920 px. То есть `1080×1350` — это разрешение картинки на выходе, а не строка, которую читает модель.

## 4. Сцена по типу слайда

- **Cover (слайд 1):** `Cover slide 1 of {N}. Headline fills top 40% in massive bold font. One strong visual element below. Small "листай →" hint at bottom-right corner.`
- **Content:** `Content slide {i} of {N}. THIS SLIDE'S MESSAGE: "{headline}" — the visual scene MUST illustrate this specific point. Choose a scene, angle, or visual metaphor that makes the viewer FEEL and UNDERSTAND the headline before reading it. The image is not decoration — it is the primary storytelling vehicle.`
- **CTA (последний):** `Final slide {N} — keep the SAME visual theme/palette/world as all previous slides. Headline prominent. DO NOT draw any "swipe next" arrow or forward hint — the carousel ends here. No clickable buttons.`

## 5. План директора (из 03-director.md) — вставляется как есть

```
=== VISUAL DIRECTOR PLAN (follow this composition) ===
Layout: {layout}
Visual elements: {visualElements}
Background: {background}
Accent objects: {accentObjects}
=== END DIRECTOR PLAN ===
```

## 6. Блок референсов — IDENTITY-LOCK (дословно; держит лицо/товар точь-в-точь)

Порядок фото фиксированный: **product → face → style**. На каждый слайд первой идёт картинка первого слайда (style-anchor), потом активные референсы. Кап 14 фото.

### 6.0 Анализ фото-референса (ОБЯЗАТЕЛЬНО перед lock) — строй промт ОТ ФОТО, не от шаблона

Прежде чем собрать блок lock — **посмотри на приложенное фото и опиши реальный объект словами**, вставь это описание в промт ПЕРЕД блоком lock. Возраст, черты, кожа берутся С ФОТО, а не из головы. Это сильнее абстрактных команд: модель и видит фото, и читает, кто/что на нём (двойная фиксация).

- **Лицо → PERSON DESCRIPTION:** пол, примерный возраст (как на фото!), тип лица, цвет/длина/причёска волос, глаза, нос, челюсть, брови, состояние кожи (чистая/загар/веснушки — как есть), растительность, телосложение, этнотип.
  Пример (считано с фото): `a slim athletic man in his late twenties, narrow oval face, fair light-brown short hair styled to the side, light grey-blue eyes, straight thin nose, clean healthy lightly-tanned skin, clean-shaven`.
- **Товар → PRODUCT DESCRIPTION:** тип, форма, пропорции, материалы, цвет, расположение лого/надписей, фактура — как на фото.

⚠️ **Не вставляй шаблонных команд** про возраст/кожу («молодой», «no wrinkles», «smooth skin») — они «от балды» и конфликтуют. Возраст и кожа приходят из ОПИСАНИЯ фото. Особенно для ЛИЦА **убери `no beautification`** из блока ниже — на фотореализме оно читается как «не сглаживай, добавь морщины» и СТАРИТ человека (проверено 2026-06-17). Личность держат фото-референс + точное описание, а не запрет на красоту.

**Товар (PRODUCT REFERENCE):**
```
Reproduce the product exactly as shown — identical shape, proportions, logo placement, label layout, colorway, materials, and all packaging text. Invent no new logos, slogans, or microtext. Modify no existing text.
PRODUCT STORYTELLING — show the product as a VISUAL NARRATIVE across slides:
- Each slide reveals a DIFFERENT facet: hero beauty shot → in-use action → detail close-up → lifestyle context → advantages/results.
- Vary angles per slide: front 3/4, side profile, top-down flat-lay, dramatic low angle, macro close-up.
- Show the product IN CONTEXT of real use: hands interacting, product mounted/installed, product mid-action.
- Connect visuals to slide TEXT: if the headline mentions a benefit, the image should visually DEMONSTRATE it (e.g., "waterproof" → product in rain/splash; "compact" → product next to everyday objects for scale).
- Vary environments: studio, outdoor, workspace, lifestyle — never the same background twice.
```

**Лицо (FACE REFERENCE — IDENTITY LOCK STRICT):**
```
Match the person's face exactly — identical eye shape, nose bridge, jawline, lip proportions, skin tone and texture, hair color and hairstyle, age, ethnicity. No beautification, no identity drift, no altered facial geometry. Place this exact person naturally in the scene.
PERSON AS ACTIVE PARTICIPANT — a living character in the carousel story:
- The person must PARTICIPATE naturally: interacting with objects, gesturing, demonstrating, reacting — never a static mannequin or passport photo.
- Vary EMOTIONS per slide to match content; vary POSES and ANGLES per slide; vary OUTFITS if possible while keeping the same person.
- The person should feel like the AUTHOR/EXPERT of the carousel.
If multiple face photos: the first is the primary reference; the rest are extra angles of the same person — use them to stabilize identity.
If the person is NOT shown on this slide (infographic-only): keep the face reference active so identity holds across the carousel, but don't render the person here.
```

⚠️ **Для фотореалистичного ЛИЦА убери `No beautification`** — на фотореализме оно работает как «не сглаживай, добавь морщины» и СТАРИТ человека (проверено 2026-06-17). Возраст/кожу задаёт PERSON DESCRIPTION из анализа фото (6.0), а не запрет на красоту. `No beautification` оставляем только для ТОВАРА (там про точность упаковки, не про кожу).

**Стиль (STYLE REFERENCE — HIGHEST PRIORITY):**
```
This is the VISUAL BLUEPRINT. Your #1 job is to make the output look like it belongs to the SAME SERIES as this reference.
ANALYZE and REPLICATE with maximum precision:
- COLOR PALETTE: exact hues, saturation, contrast levels. If the ref uses muted pastels — use muted pastels. If bold neons — bold neons.
- TYPOGRAPHY STYLE: serif vs sans-serif feel, weight, letter spacing, text positioning (centered/left/overlaid on image).
- LAYOUT STRUCTURE: where text sits relative to visuals, margins, grid alignment, text-to-image ratio.
- FRAMES & BORDERS: if the ref has rounded corners, borders, frames, divider lines — reproduce them.
- BACKGROUND TREATMENT: solid color, gradient, photo, texture, blur — match the approach exactly.
- LIGHTING & MOOD: warm/cool, high-key/low-key, dramatic/soft.
- CHARACTER/OBJECT POSITIONING: follow the same spatial logic (left third, centered, bottom).
- GRAPHIC ELEMENTS: icons, shapes, overlays, badges, shadow style — copy the design language.
Do NOT copy any specific objects, products, logos, faces, or text content from the style reference. Only copy the VISUAL LANGUAGE and apply it to the carousel's own subject.
```

> **Что осознанно упрощено (а не потеряно по ошибке).** В боевом Vibe у каждого референса есть ещё ветки `User notes about the product / face / style` (текстовые описания, что именно перенести с рефа) и ветки `primary hero / secondary` для случая нескольких фото на одну роль (когда товар или лицо даны несколькими снимками — первый назначается главным, остальные — добивкой деталей/углов). В учебном ките эти ветки сознательно опущены: здесь на каждую роль идёт ОДИН референс без текстового описания, поэтому различать «главный/второстепенный» и подмешивать пользовательские заметки не нужно. Это упрощение под формат урока, а не пропуск.

## 7. Секция TEXT (КЛЮЧ Варианта Б — модель рисует точные строки) — дословно

```
=== TEXT ===
[Cover]  Headline: "{HEADLINE}" — bold sans-serif, VERY LARGE (60-80pt), dominates frame.
         Subtext: "{BODY}" — lighter weight, smaller, below headline, but STILL high-contrast and clearly legible on a phone (white or brand-accent over a darkened strip/scrim) — NEVER low-contrast grey that blends into the photo.
[Content/CTA]  Headline: "{HEADLINE}" — bold sans-serif, high contrast.
               Body: "{BODY}" — regular weight, comfortable reading size, below headline, kept high-contrast and legible — not greyed-out, not blending into the background.
Render ALL text exactly as provided — every word visible.
If text doesn't fit — reduce font size (minimum 22pt). Never truncate.
TEXT DUPLICATION BAN: Each text string (headline, body) appears EXACTLY ONCE on the slide. NEVER render the same headline or body twice — not at top AND bottom, not in two different sizes, not as a reflection or echo. One headline placement, one body placement, that is all.
```
*(текст в промт подаётся в ВЕРХНЕМ РЕГИСТРЕ — `formatTextForRendering` = .toUpperCase())*

## 8. Финальные ограничения (дословно)

```
ONE DOMINANT ELEMENT: either headline fills 40%+ of frame, OR one large visual fills 40%+.
Text must be readable: high-contrast typography, outline/stroke, or a subtle backdrop behind letters ONLY if needed. Avoid large flat panels/cards covering the scene — let the background theme breathe through.
FORBIDDEN LAYOUT: Never create a "slide within a slide" — no small inset photo/card inside a larger frame, no collage/mosaic, no picture-in-picture. The entire frame is ONE seamless composition with ONE background scene. Text is overlaid directly on the scene, not in a separate panel.
Professional Instagram quality, sharp and crisp.
Unique composition — different layout/angle from other slides. (для слайдов 2+)
```

**Приоритет стиля над раскладкой (если приложен style-реф) — добавляется в КОНЕЦ промта дословно:**
```
STYLE REFERENCE TAKES PRIORITY: if the style reference conflicts with any layout or typography instruction above, follow the style reference. The goal is maximum visual similarity to the reference style.
```
*(решает конфликт «стиль vs layout»: если стилевой референс расходится с любой инструкцией по раскладке/типографике выше — побеждает референс. Без этой строки модель может проигнорировать стиль ради буквального следования layout-указаниям.)*

## 9. Style-anchor + фото-референс — ЖЁСТКОЕ ПРАВИЛО (на каждый слайд ВСЕГДА оба)

**На КАЖДЫЙ слайд серии прикладываются ДВА якоря, без исключений:**
1. **Слайд 1 (cover) генерится ПЕРВЫМ** — к нему прикладывается только фото лица/товара (style-anchor'а ещё нет).
2. **Слайды 2…N — ВСЕГДА два референса разом:**
   - **cover (slide-01)** — style-anchor, держит единый бренд / палитру / типографику;
   - **фото лица/товара** — держит личность / товар.
   Прикладывай ОБА на каждый слайд. Не опускай ни один — даже если человек НЕ в кадре на этом слайде, фото остаётся активным (единство лица через серию), и cover остаётся активным (бренд).
3. Порядок референсов в кадре: **cover (style-anchor) → product → face → style** (кап 14 фото суммарно).

Практика (Codex CLI): slide-01 — `-i фото`; слайды 2…N — `-i slide-01.png -i фото` (повторяй `-i` для каждого; cover первым). На nano-banana — `image_input: [slide-01, фото, ...]`.

## 10. Запрет (бизнес-безопасность маркетплейсов — сохранить)

```
FORBIDDEN: no Wildberries, WB, Ozon, Yandex, Sber, Avito, VK, Rutube, Dzen, Tinkoff, or Alfa-Bank logos or names anywhere; no watermarks.
```

---

**Итого пайплайн скилла собран:** `01-text-phase` (углы → тексты) → `02-styles` (DNA) → `03-director` (сцены) → `04-image-prompt` (этот файл: финальный промт + identity-lock + текст в кадре). Движок картинок — через toolbox (gpt-image-2 / nano-banana-pro).
