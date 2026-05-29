# Статус: sysadmin

## Сейчас в фокусе
Локальный CSRF-fix для 3X-UI v3.0.2 ждёт ответ Василия (vefmvai/sysadmin PR #2). Семейный VPN на новой подписке Vento работает. До merge upstream — VPN-задачи на ветке `fix/csrf-login-3xui-v3`, на `main` API-логин в панель сломан.

## Последнее действие
2026-05-29 — реализован CSRF fix `scripts/lib-api/3xui.sh` для 3X-UI v3.0.2 по спецификации CHANGELOG v1.8.5 (issue #1, PR #2 в `vefmvai/sysadmin`). Обнаружен и описан архитектурный сдвиг API-эндпоинтов на v3.0.2 — issue #3 с картой переезда. Обновлён UUID `upstream-vento-nl` на новой подписке через прямую правку БД 3X-UI (backup + UPDATE + verify), VPN мамы работает.

## Следующий шаг
1. Ждать ответ Василия на issue #1 + ревью PR #2 в `vefmvai/sysadmin`.
2. Если PR примут — `git pull` на main, удалить локальную feature-ветку, отметить ADR-0004 как «выполнено».
3. Параллельно: настроить Bitwarden CLI через `/setup-secrets-vault`, чтобы убрать пароль панели из `infra/3xui.txt`.

## Блокеры / сигналы
- Локальный fix CSRF доступен только на ветке `fix/csrf-login-3xui-v3` (push'нута в `fork` = `ndudko-byte/sysadmin`). На `main` любые VPN-скиллы будут падать с HTTP 403 — нужно `git checkout fix/csrf-login-3xui-v3` перед работой с панелью.
- API-эндпоинты v3.0.2 переехали (issue #3): `inbounds/getXrayConfig` → `server/getConfigJson`, `inbounds/updateXrayConfig` удалён. Скилл `/configure-vpn-routing` нужно будет переучить под дельта-операции — после ответа Василия.
- Push на `origin` (vefmvai/sysadmin) не работает — для PR используется fork. Не блокер (решено).

## Прогресс
- Версия мозга: 1.9.0 (свежее upstream).
- Локальный CSRF-patch: коммит `b1c7666` на ветке `fix/csrf-login-3xui-v3`, PR #2 открыт.
- VPN: outbound `upstream-vento-nl` подключён с новым UUID, клиент `mama` (iPhone) ходит через NL.
- Инфра: бэкап БД 3X-UI до правки UUID — `/etc/x-ui/x-ui.db.backup-20260529-180745` (на сервере).
- `infra/`: первый коммит сделан, `.gitignore` защищает секреты, `decisions/ADR-0001..0004` в истории.

## Активность (последние 7 дней)
31 коммит:

- ea45465 chore: STATUS проекта + vpn-clients в .gitignore
- 0ae19cf feat(networking): 1.9.0 — эталон серверных сетей по умолчанию + рефлекс 3.8.12
- 9ccc862 feat(vpn): webroot-методы TLS как дефолт + рефлексы 3.8.8/3.8.9 в персону
- 832b10e feat(persona): 1.8.4 — регистр взрослого технического языка (§1 + рефлекс 3.9)
- 44b1127 feat(vpn): 1.8.3 — достроена полная картина портов в эталоне (3X-UI и порт 80)
- ed050a0 chore(release): 1.8.2 — knowledge-эталон сосуществования сайтов и VPN на 443
- 8f61646 feat(vpn): knowledge-эталон сосуществования сайтов и VPN на 443 + рефлекс 3.8.7
- d32b8c2 fix(security): секрет в прямой сессии с агентом — рабочая передача, не компрометация (1.8.1)
- 9c151e1 feat(vpn): защита от «скачущего IP по странам» в балансире — 3 слоя (1.8.0)
- 4e91459 feat(vpn): скилл /extract-subscription-servers — извлечение из закрытых подписок «под ключ» (1.7.0)
- 62d6fad feat(vpn): HWID-locked подписки — диагностика заглушки + добыча HWID (1.6.0)
- 96f5131 feat(vpn): скилл-дирижёр /finalize-vpn-routing — доктор для застрявшей настройки
- 201749c fix(inventory): разделение stdout/stderr в dump-snapshot + заглушение ssh-шума — 1.4.3
- 8db7443 fix(self-test): резолв относительного root_path от каталога конфига — 1.4.2
- 4e33892 fix(brain): универсальный язык в активном мозге + redaction секретов v2 — 1.4.1
- 6202c6e feat(vpn): UX маршрутизации для новичка — выбор страны выхода + стабильный IP
- a12df85 fix(inventory): сбор автоматизаций в dump-snapshot — фиксы по прогону на selectel
- b4ae654 fix(docs): синхронизация sysadmin-meet и шаблона с ADR-0007 и релизом 1.2.0
- 1764238 fix(skills): redaction секретов в dump-snapshot до записи на диск
- 9b9a50f fix(vpn): гибкая маршрутизация 3X-UI приведена к рабочему эталону
- 9218f0d feat(vpn): Happ — основной рекомендованный клиент — версия 1.3.0
- ac653ea feat(inventory): автоматизации на карте инфраструктуры — версия 1.2.0
- 3e7f4dd fix(init): гибкие менеджеры паролей (keepassxc + other) — версия 1.1.1
- 2f3c97a chore: версия мозга 1.0.1 → 1.1.0 + CHANGELOG + динамический клон последнего тега
- c360164 feat(init): адаптивный гейт окружения + самопроверка с честным вердиктом
- a2e2b66 fix(init): кроссплатформенность setup на Windows + запрет суррогатов конфига
- e0b0b34 docs(knowledge): зеркалирование платной подписки на свой сервер (обход лимита устройств)
- 81a0e53 refactor(vpn): Reality на РФ-сервере — менторская развилка вместо жёсткого запрета
- c499f26 fix(vpn): guard «Reality на РФ-сервере запрещён» в коде + server_role в config
- f1b3a60 fix(vpn): развязка агента от курса + стоп-знак этапов + жёсткое правило протокола
- 0c0275a docs(vpn): обновлена ссылка на урок курса после переименования

Плюс на ветке `fix/csrf-login-3xui-v3`: `b1c7666 fix(vpn): CSRF-аутентификация в lib-api/3xui.sh для 3X-UI v3.0+`.

В соседнем `infra/`: `da51e65 chore: .gitignore` + `174855b docs(decisions): начальный набор ADR (0001..0004)`.

---
*Обновлён: 2026-05-29 18:30*
