# Лицо и товар в кадре: identity-lock

Эта памятка нужна, если у пользователя есть фото-референс лица, товара, места или стиля.

## Принцип

Не проси модель "сделать того же человека". Опиши узнаваемые признаки и запрети усреднение.

## Перед prompt

Сначала проанализируй референс:

- форма лица;
- пропорции глаз;
- нос;
- губы;
- линия челюсти;
- волосы;
- возрастной диапазон;
- мимика;
- особенности кожи;
- стиль одежды;
- аксессуары;
- что нельзя менять.

Для товара:

- форма;
- материал;
- цвет;
- логотип;
- пропорции;
- упаковка;
- маркировка;
- что нельзя менять.

## Identity block

```text
Identity lock:
Use the attached reference as identity source. Preserve recognizable facial structure, proportions, hair, age range and natural expression. Do not beautify, stylize into a different person, change ethnicity, change age, alter jawline, nose, eye shape or lips. Change only pose, lighting, framing and scene as specified.
```

Для товара:

```text
Product identity lock:
Use the attached product reference as the source of truth. Preserve exact shape, proportions, material, color, logo placement and packaging details. Do not invent labels, change brand marks, alter proportions or replace the product with a generic object.
```

## Style-anchor

Если генерируется серия слайдов:

1. Сначала сделать cover или style-anchor.
2. Для следующих слайдов использовать style-anchor plus identity reference.
3. Менять сцену и композицию, но сохранять свет, цвет, настроение, визуальный язык.

## Отбраковка

Сгенерированный кадр не проходит, если:

- лицо стало другим;
- модель "улучшила" человека до неузнаваемости;
- товар потерял форму или логотип;
- стиль слайда выбивается из набора;
- текст залез на лицо или товар;
- руки, глаза, зубы или важные детали заметно сломаны;
- кадр выглядит как stock image вместо бренда автора.

## Важное ограничение

Один фото-референс не гарантирует стабильное лицо на потоке. Для постоянного персонажа или большого объема может потребоваться отдельная модель, обученный identity workflow или ручная отбраковка. В skill не обещать стабильность как гарантию.
