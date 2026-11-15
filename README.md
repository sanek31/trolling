# play.spacestation14.com — JOcker notice

Минималистичная статическая страница для dangling GitHub Pages custom domain `play.spacestation14.com`.

На странице только:

- текст **«Page is now under jurisdiction of JOcker.»**
- кнопка на официальный сайт `https://spacestation14.com/` с подписью **«(DNS not included)»**
- маленький дисклеймер «Not affiliated with Space Wizards. Just a joke.»

Никаких картинок клоуна, сертификатов и таблиц. Favicon — простая буква **J**, не клоун.

## Файлы

```
index.html      — главная страница
styles.css      — минимальные стили
404.html        — страница для неизвестных путей
favicon.svg     — иконка с буквой J
CNAME           — play.spacestation14.com
.nojekyll       — отключает Jekyll, чтобы GitHub Pages отдавал файлы как есть
README.md       — этот файл
```

## Как задеплоить

1. Создай **публичный** репозиторий на GitHub, например `play-spacestation14`.
2. Загрузи **все файлы из этой папки в корень репозитория** — именно файлы, не саму папку. Иначе `index.html` и `CNAME` окажутся в подпапке.
3. Открой **Settings → Pages**.
4. В **Build and deployment**:
   - Source: **Deploy from a branch**
   - Branch: `main` (или `master`)
   - Folder: **`/ (root)`**
   - Save.
5. В **Custom domain** впиши:

   ```
   play.spacestation14.com
   ```

   Нажми **Save**. GitHub должен подхватить `CNAME` из репозитория.
6. Дождись сборки Pages (Actions → Pages build and deployment), обычно 1–5 минут.
7. Когда появится сертификат, включи **Enforce HTTPS**.

## Если что-то не работает

- **`404` после установки домена** — подожди 5–30 минут, проверь, что `index.html` лежит именно в корне выбранной ветки, и что Pages source стоит `/ (root)`.
- **«Domain is already taken»** — значит, домен уже верифицирован/занят другим GitHub-аккаунтом. В этом случае забрать его не получится; это не ошибка деплоя.
- **GitHub просит TXT-запись** — добавь в Cloudflare DNS запись `TXT` с именем `_github-pages-challenge-<твой-github-username>.play.spacestation14.com` и значением, которое покажет GitHub. После верификации можно удалить.
- **Cloudflare proxy (оранжевая тучка)** — если GitHub не может проверить домен, временно переключи запись на **DNS only (серая тучка)**, дождись сертификата, потом можно вернуть proxy.
- **`CNAME` перезаписан** — GitHub Pages сам создаёт `CNAME` при смене custom domain. Содержимое должно быть ровно `play.spacestation14.com` без `https://` и без слэша на конце.

## Настройки контента

- В `index.html` стоит `<meta name="robots" content="noindex">` — страница не будет индексироваться поисковиками. Если хочешь, чтобы её находили, удали эту строку.
- Хочешь другой текст на кнопке — правь блок `<a class="button" ...>` в `index.html` и `404.html`. Сейчас там `Official SS14 site (DNS not included) →`.
- В `index.html` и `404.html` пути к CSS/иконке абсолютные (`/styles.css`, `/favicon.svg`), потому что страница рассчитана на корень custom domain `https://play.spacestation14.com/`. Если будешь тестировать на `https://username.github.io/repo/` до привязки домена, замени их на относительные `styles.css` и `favicon.svg`.
- Не добавляй формы логина, сбора паролей, редиректы на сторонние «похожие» сайты и прочие штуки, которые превращают шутку в подделку. Кнопка должна вести на настоящий `https://spacestation14.com/`.

## Почему это вообще работает

`play.spacestation14.com` — это GitHub Pages custom domain, который сейчас отдаёт `404 Site not found` и не имеет verification TXT. Если домен не верифицирован в GitHub, его можно добавить к своему Pages-репозиторию. Это классический subdomain takeover; здесь он использован для безобидной шутки, а не для кражи данных.
