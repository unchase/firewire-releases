# Firewire Analytics для Windows, macOS и Linux

Аналитика инвестиционного портфеля в отдельном окне: доходность TWR и XIRR, облигации и купоны,
риск-метрики, налоги и ИИ-Ко-пилот — та же платформа [Firewire](https://fire-wire.ru), что и в браузере.
Здесь публикуются готовые сборки и журнал изменений; исходный код приложения закрыт.

## Скачать

Последняя версия — на странице [последнего релиза](https://github.com/unchase/firewire-releases/releases/latest).
Все версии — в [списке релизов](https://github.com/unchase/firewire-releases/releases), что
в каждой изменилось — в [журнале изменений](https://github.com/unchase/firewire-releases/blob/HEAD/CHANGELOG.md).

| Файл | Система | Когда брать |
|---|---|---|
| `Firewire.Analytics_X.Y.Z_x64-setup.exe` | Windows | обычная установка для себя — без прав администратора |
| `Firewire.Analytics_X.Y.Z_x64_en-US.msi` | Windows | установка для всех пользователей компьютера или через групповые политики |
| `….dmg` | macOS | одна сборка для Apple Silicon (M1 и новее) и Intel |
| `….deb` | Linux | Ubuntu, Debian, Linux Mint и другие системы с `apt` |
| `….rpm` | Linux | Fedora, openSUSE, RHEL и другие системы с `dnf` или `zypper` |
| `….AppImage` | Linux | любой дистрибутив, без установки |
| `SHA256SUMS.txt` | — | суммы SHA-256 всех установщиков релиза — чтобы проверить файл |

Сборки для Windows выходят в каждом релизе, для macOS и Linux — не в каждом. Если в последнем
релизе нет файла для вашей системы, откройте [список релизов](https://github.com/unchase/firewire-releases/releases)
и возьмите самый новый, где он есть. Или откройте [fire-wire.ru](https://fire-wire.ru) в браузере и
установите его как приложение (PWA) — инструкция в [Базе знаний](https://help.fire-wire.ru/guides/desktop-and-pwa).

## Системные требования

- Windows 10 или Windows 11, 64-разрядная, и Microsoft Edge WebView2: в Windows 11 он уже есть,
  установщик доставит его сам, если его нет.
- macOS 10.13 или новее.
- Linux, 64-разрядный (x86_64), с WebKitGTK 4.1: .deb и .rpm ставят его сами как зависимость.
- Аккаунт Firewire: приложение входит в тот же личный кабинет, что и сайт.

## Предупреждение SmartScreen (Windows)

Установщики пока **не подписаны** сертификатом разработчика, поэтому при первом запуске Windows может
показать окно «Система Windows защитила ваш компьютер». Прежде чем нажать «Подробнее» → «Выполнить
в любом случае», убедитесь, что файл тот самый, — сверьте его сумму SHA-256 с `SHA256SUMS.txt` того же
релиза. В PowerShell:

```powershell
(Get-FileHash .\Firewire.Analytics_X.Y.Z_x64-setup.exe -Algorithm SHA256).Hash.ToLower()
```

Строка должна совпасть с хэшем этого файла в `SHA256SUMS.txt` (без `.ToLower()` PowerShell печатает
те же буквы заглавными — регистр не важен). Не совпала — не запускайте файл и скачайте его заново
со страницы релиза.

## macOS: первый запуск

Приложение не нотаризовано Apple, поэтому macOS при первом запуске скажет, что не может проверить
разработчика. Сначала сверьте сумму `.dmg` с `SHA256SUMS.txt` в Терминале:

```sh
shasum -a 256 ~/Downloads/<файл>.dmg
```

Откройте `.dmg` и перетащите Firewire Analytics в «Программы». Запустите приложение один раз, затем
откройте «Системные настройки» → «Конфиденциальность и безопасность» и нажмите «Всё равно открыть»
напротив Firewire Analytics. Если macOS пишет, что приложение «повреждено», снимите с него карантинную
метку и запустите снова:

```sh
xattr -dr com.apple.quarantine "/Applications/Firewire Analytics.app"
```

## Linux: установка

Сначала сверьте сумму скачанного файла с `SHA256SUMS.txt`: `sha256sum <файл>`. Затем, в папке с файлом:

- `.deb` — `sudo apt install ./<файл>.deb`;
- `.rpm` — `sudo dnf install ./<файл>.rpm`;
- `.AppImage` — `chmod +x <файл>.AppImage`, затем запустите файл. На
  системах без FUSE 2 (например, Ubuntu 22.04 и новее) сначала поставьте `libfuse2`
  (в Ubuntu 24.04 — `libfuse2t64`).

## Обновление

Автообновления у приложения нет: скачайте новую версию со страницы релиза и установите поверх
текущей — вход и настройки сохранятся.

## Удаление

- **Windows** — «Параметры» → «Приложения»: найдите Firewire Analytics в списке и нажмите «Удалить».
  Данные приложения остаются в `%APPDATA%\ru.firewire.analytics` и `%LOCALAPPDATA%\ru.firewire.analytics`:
  удалите обе папки, если они больше не нужны.
- **macOS** — перетащите Firewire Analytics из «Программ» в Корзину. Данные приложения — в
  `~/Library/Application Support/ru.firewire.analytics`, `~/Library/Caches/ru.firewire.analytics`
  и `~/Library/WebKit/ru.firewire.analytics`.
- **Linux** — `sudo apt remove firewire-analytics` или `sudo dnf remove firewire-analytics`; у AppImage
  достаточно удалить файл. Данные приложения — в `~/.local/share/ru.firewire.analytics` и
  `~/.cache/ru.firewire.analytics`.

Портфель и настройки аккаунта хранятся на сервере Firewire и с удалением приложения не пропадают.
