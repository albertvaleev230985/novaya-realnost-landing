# novaya-realnost-landing
Лендинг курса «ИИ. Новая реальность» на start.neovida.ai: онлайн-поток 4 (старт 21 ноября 2026) и офлайн-поток в Уфе.

## Даты, цены, номера потоков
Всё в объекте `FMT` в `index.html` (онлайн и офлайн отдельно) плюс статические значения в HTML для онлайна: мета-описание, шапка, программа, форма записи, текст заявки в Telegram.

## Видео и картинки: страница должна оставаться лёгкой
- В карусели отзывов и в блоке оценок играют **короткие превью** из папок `testimonials/preview/` и `ratings/preview/` (5 секунд, 480 px, без звука, 150–750 КБ). Грузятся и играют только карточки, которые сейчас на экране.
- Полный ролик со звуком открывается по нажатию: у отзыва путь в `data-full`, у оценки в `data-r-src`.
- Обложки карточек и фото ведущего в WebP (`preview/*.webp`, `albert.webp`).
- Шрифты лежат в `fonts/`, правила `@font-face` вписаны в начало `index.html`. Google Fonts не используем.

Новый отзыв `NN-имя.mp4` (вертикальный 720×1280) добавлять так:

```bash
ffmpeg -ss 1 -t 5 -i testimonials/NN-имя.mp4 -an -vf "scale=480:-2:flags=lanczos,fps=30" -c:v libx264 -profile:v high -pix_fmt yuv420p -crf 26 -preset slow -movflags +faststart testimonials/preview/NN-имя.mp4
cwebp -q 80 -resize 480 0 testimonials/NN-имя.jpg -o testimonials/preview/NN-имя.webp
```

Карточку вставить дважды (вторая копия с `aria-hidden="true"` для бесконечной ленты):

```html
<article class="t-card" data-full="testimonials/NN-имя.mp4">
  <video data-src="testimonials/preview/NN-имя.mp4" poster="testimonials/preview/NN-имя.webp" muted loop playsinline preload="none"></video>
  ...
</article>
```

Никогда не ставить в карточки полный ролик с `autoplay`: до 30 сентября 2026 это давало 15 МБ загрузки за первые 8 секунд на телефоне.
