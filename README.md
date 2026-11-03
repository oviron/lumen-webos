# Lumen: русский интерфейс

Форк [ammar027/lumen-webos](https://github.com/ammar027/lumen-webos) с полным русским
переводом. Lumen заменяет главный экран LG webOS: приложения, входы, часы, обои,
пункт управления и заставки. Нужны webOS 6+ (Chromium 79+), root и Homebrew Channel.

Переведены меню, все описания настроек, первоначальная настройка, подсказки пульта,
сообщения об ошибках, режим ожидания, погода, страны и города, названия и подписи
изображений и видеообоев. Русская локаль применяется к датам и предпросмотру часов;
неделя в календаре начинается с понедельника. Формы минут и секунд учитывают число.
Названия сторонних приложений, языков и пользовательских альбомов сохраняются.

Русский выбран по умолчанию при новой установке. После обновления существующего
Lumen выберите **Настройки > Язык и формат времени > Язык > Русский**. Другие языки
доступны. ID приложения сохранён: `com.ammar027.lumen`, версия пакета `1.1.6`.

Длинные подписи прокручиваются после паузы только у выделенного элемента: в пункте
управления, настройках и названиях приложений. При уходе с элемента текст возвращается
в начало. Настройка уменьшения движения отключает прокрутку.

## Установка

Скачайте `.ipk` из [релизов](https://github.com/oviron/lumen-webos/releases/latest)
и установите через [Dev Manager](https://github.com/webosbrew/dev-manager-desktop)
или webOS CLI:

```sh
ares-install --device lgtv com.ammar027.lumen_1.1.6_all.ipk
```

Репозиторий Homebrew Channel:

```
https://raw.githubusercontent.com/oviron/lumen-webos/hbc-repo/stable/apps.json
```

Обновление пакета сохраняет настройки и приложения. Не устанавливайте Developer
Mode на телевизор с root. Установка Lumen сама по себе не переназначает Home:
[выбор главного экрана](docs/native-home.md) и
[существующий способ перенаправления](docs/tv-experience.md).

## Сборка и перевод

Нужны Node 22.13+, Python 3.9+, git. Скрипты исходного Lumen используют путь
`~/Developer/webos-launcher-tvos`: клонируйте туда или создайте симлинк на checkout.

```sh
git clone https://github.com/oviron/lumen-webos ~/Developer/webos-launcher-tvos
cd ~/Developer/webos-launcher-tvos
git clone https://github.com/partridgeworks/webos-launcher app
git -C app checkout 1e2c39b9a988ceb1b258e40e3592bda84a2aa076
npm ci --prefix app
npm ci --prefix tools
python3 tools/rebuild.py
python3 tools/build_release.py
```

`app/` не отслеживается: он собирается из закреплённого исходника и слоёв
[REBUILD.md](REBUILD.md). Перевод: [tools/ru.json](tools/ru.json).
[Последний слой](tools/apply_russian.py) подключает его ко всем экранам.
Проверка полноты и склонений выполняется при каждой сборке; отдельно:

```sh
node tools/check_russian.mjs
```

Готовый пакет и SHA-256 находятся в `release/`. Публичная сборка содержит картины
в общественном достоянии и не содержит частных шрифтов и сторонних логотипов.
Релизный workflow собирает пакет и публикует его в репозитории Homebrew Channel.

## Авторы и лицензия

Основа: [Lumen, ammar027](https://github.com/ammar027/lumen-webos) и
[webos-launcher, partridgeworks](https://github.com/partridgeworks/webos-launcher).
Использованы идеи и код [xcv58](https://github.com/xcv58) и
[Sam Renfrew](https://github.com/samrenfrew/lumen-webos).
[MIT](LICENSE), [уведомления о сторонних материалах](THIRD_PARTY_NOTICES.md).
Проект не связан с LG, Apple и разработчиками приложений.
