# Железный круг: приложение для Android и iOS

Сайт теперь работает как приложение (PWA): ставится на экран «Домой», открывается без адресной строки, на весь экран. Это бесплатно и работает на обоих телефонах. Сборку в APK и IPA для магазинов см. в разделе 4.

## 1. База данных и регистрация (Supabase, бесплатно)
1. Создайте проект на supabase.com (тариф Free).
2. SQL Editor → вставьте весь файл schema.sql → Run.
3. Authentication → Providers → Email → отключите «Confirm email» (для быстрого старта).
4. Project Settings → API → скопируйте Project URL и anon public key.
5. Вставьте их в блок CFG в начале скрипта в index.html. Ключ anon публиковать безопасно.

## 2. Размещение (нужен адрес с https)
Самый простой путь: app.netlify.com/drop. Перетащите на страницу папку iron-circle целиком, файл index.html должен лежать в её корне. Netlify выдаст адрес вида имя.netlify.app. Альтернативы: Cloudflare Pages (Upload assets) или GitHub Pages.

## 3. Установка на телефон
- Android (Chrome): меню ⋮ → «Установить приложение» или «Добавить на главный экран».
- iPhone (только Safari): кнопка «Поделиться» → «На экран “Домой”».

## 4. Настоящие нативные приложения (для App Store и Google Play)
Оборачиваются тем же кодом через Capacitor. Собирать нужно на своём компьютере:
1. Установите Node.js. Создайте папку проекта и положите все файлы из iron-circle в подпапку www.
2. Выполните: npm init -y, затем npm i @capacitor/core @capacitor/cli @capacitor/android @capacitor/ios
3. npx cap init "Железный круг" com.ваше.имя --web-dir=www
4. Android: npx cap add android, npx cap sync, npx cap open android. В Android Studio соберите APK (Build → Build APK).
5. iOS: нужен Mac с Xcode. npx cap add ios, npx cap sync, npx cap open ios.
Для публикации нужны аккаунты разработчика: Google Play (разовый платёж около 25 долларов) и Apple Developer (около 99 долларов в год). Проверьте актуальные цены. APK для себя и друзей можно раздавать файлом бесплатно.

## Ограничения бесплатного уровня
Supabase Free ограничивает размер базы и хранилища, а неактивный проект могут приостановить (включается в панели). Приложение грузит последние 300 постов целиком, для большой аудитории нужна постраничная загрузка.
