# Anthology MO2 Modpack

Этот репозиторий является update channel для MO2-модпака Anthology 2.1.

Лаунчер скачивает ZIP ветки `main` и устанавливает из него только разрешённые
файлы `gamedata/configs` и `gamedata/scripts`.

## Как Это Работает Для Игрока

Лаунчер читает:

```text
version.json
```

Затем скачивает:

```text
https://github.com/sysliveprime-ctrl/anthology-mo2-modpack/archive/refs/heads/main.zip
```

После установки он сохраняет список файлов в:

```text
.launcher_update_state.json
```

При следующем обновлении файлы, которые раньше ставил лаунчер, но которых больше
нет в новом ZIP, будут удалены.

## Что Хранится В Git

Репозиторий хранит только лёгкие файлы модпака:

- `gamedata/configs/**`
- `gamedata/scripts/**`
- `version.json`
- служебные Git-файлы

Большие файлы, ассеты, архивы, exe, dll, pdb, изображения и аудио в Git не
добавляются.

## R.A.K Weapon Pack

Папки R.A.K являются ручной локальной частью сборки и специально игнорируются:

```text
*R.A.K Weapon Pack Adaptation Global A.N.T.H.O.L.O.G.Y*/**
```

Лаунчер должен сохранять эти папки и не удалять их при обновлении.

## Релиз Модпака

```powershell
py -3 E:\dev\Anthology-Work-Git\skills\anthology-release-ops\scripts\anthology_release_ops.py modpack --version YYYY.MM.DD.N --notes "Описание обновления"
```

Скрипт:

1. обновляет `version.json`;
2. коммитит изменения модпака;
3. пушит `main` в `sysliveprime-ctrl/anthology-mo2-modpack`.

Release assets для модпака не нужны: лаунчер скачивает `main.zip`.

## Перед Публикацией

```powershell
git status --short --branch
```

Проверить:

- нет случайных R.A.K-файлов в tracked changes;
- нет тестовых файлов `anthology_release_*`;
- `version.json` содержит понятные русские notes;
- рабочее дерево чистое после push.
