# Сборка image prompt для слайда

Этот файл отвечает за финальный prompt к картинке. Он не выбирает стратегию карусели, а превращает утвержденный slide copy и scene plan в prompt для выбранного image-движка.

Перед использованием прочитай:

```text
06-engine-passport.md
07-лицо-identity.md, если есть лицо или товар
```

## Prompt contract

Каждый prompt должен содержать:

1. Format and aspect ratio.
2. Visual scene.
3. Composition and camera.
4. Lighting and mood.
5. Text zone.
6. Exact text, если выбран image-text mode.
7. Style continuity.
8. Reference images.
9. Identity-lock, если есть лицо или товар.
10. Negative constraints.
11. Output name.

## 1. Consistency frame

В начало каждого prompt добавляй:

```text
Create one slide for a cohesive social media carousel. Keep the same visual system across all slides: consistent color palette, lighting, typography mood, spacing, brand feel and composition logic. Each slide must feel unique in scene and camera angle, but part of the same carousel set.
```

## 2. Canvas

```text
Canvas: vertical 4:5 social carousel slide. Keep important text inside safe margins. Avoid placing key text or faces at the extreme edges.
```

Если другой формат:

```text
Canvas: 9:16 story/reel cover. Keep key text away from top and bottom UI zones.
```

## 3. Scene

Вставь из scene plan:

```text
Scene: <specific scene>
Subject: <person/product/object>
Environment: <place>
Camera: <shot type, angle, lens feel>
Lighting: <natural/studio/dramatic/soft>
Composition: <where subject and text sit>
Mood: <calm/sharp/premium/playful/etc>
```

## 4. Text zone

Даже если текст накладывается кодом, prompt должен оставить место под текст.

```text
Text zone: leave a clean readable area in the upper third / left side / right side / center card. Do not place detailed objects behind the text zone.
```

## 5. Exact text section for image-text mode

Использовать только если engine passport подтверждает, что выбранный движок держит нужный язык.

```text
TEXT TO RENDER EXACTLY:
Headline: "<headline>"
Subtext: "<subtext>"
Language: Russian.
Render the text exactly as written. Do not translate, paraphrase, add words, remove words or change punctuation. Text must be large, sharp, readable and placed only inside the defined text zone.
```

Если engine плохо держит текст, не проси его писать текст. Используй code-text mode.

## 6. Code-text mode prompt

Если текст накладывается HTML/CSS, генерируй чистый фон:

```text
Do not render any text, letters, logos, captions, UI, watermarks or signs. Leave the defined text zone clean for later typography overlay.
```

## 7. Identity-lock

Если есть лицо:

```text
Use the attached face reference as identity source. Preserve recognizable facial structure, proportions, hair, age range and natural expression. Do not beautify into a different person. Change only pose, lighting, framing and scene as specified.
```

Если есть товар:

```text
Use the attached product reference as source of truth. Preserve exact shape, material, proportions, color, logo placement and packaging details. Do not invent labels or turn it into a generic object.
```

## 8. Style anchor

Для слайдов 2..N использовать:

```text
Use slide 01 as style anchor. Match its visual language, color palette, lighting, typography mood and composition logic while creating a new scene for this slide.
```

Если style reference есть отдельно:

```text
Use the attached style reference only for visual mood, color, lighting and composition. Do not copy its content or text.
```

## 9. Negative constraints

Добавляй в каждый prompt:

```text
Avoid: extra text, misspelled text, watermark, random logos, distorted hands, distorted face, duplicated face, generic stock photo look, cluttered background, low readability, overprocessed beauty filter, incorrect product details, text outside safe margins.
```

## 10. Prompt template

```text
Create slide <number> of <total> for a cohesive social media carousel.

Canvas: <aspect ratio and safe area>.
Style: <style name or custom visual direction>.
Consistency: match the approved carousel style and keep brand continuity.

Scene: <scene>.
Subject: <subject>.
Environment: <environment>.
Camera and composition: <camera, angle, framing, text zone>.
Lighting and mood: <lighting, mood>.

<Text section, only for image-text mode>

<Identity-lock, if needed>
<Style anchor, if slide 2..N>

Avoid: <negative constraints>.
Output: slide-<NN>.png.
```

## 11. QA after generation

Проверить каждый слайд:

- текст точный;
- текст читается на телефоне;
- нет лишних букв и водяных знаков;
- лицо/товар узнаваемы;
- safe margins соблюдены;
- стиль совпадает с набором;
- сцена отличается от соседних;
- слайд выполняет свою роль в slide ladder.

Если текст ошибся, переключиться на code-text mode или перегенерировать только проблемный слайд.
