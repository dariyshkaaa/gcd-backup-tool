# gcd-backup-tool
Утилиты на Python: НОД списка чисел (Евклид) и резервное копирование конфигов (tar.gz + SHA-256). Полная документация.
# 🐍 gcd-backup-tool

Консольные утилиты на Python для вычисления НОД и резервного копирования конфигурационных файлов.

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Tests](https://img.shields.io/badge/Tests-20%2F20-brightgreen)](tests/)

## 📖 О проекте

Две независимые CLI-утилиты на **Python 3.10+**, без внешних зависимостей:

| Утилита | Назначение |
|---------|-----------|
| 🔢 `src/gcd_tool.py` | НОД списка из N чисел (алгоритм Евклида) |
| 💾 `src/backup_tool.py` | Резервное копирование конфигов в `tar.gz` + SHA-256 |

Проект выполнен в рамках производственной практики в **КГБ ПОУ «Хабаровский промышленно-экономический техникум»**, специальность 09.02.07 «Информационные системы и программирование».

## ✨ Возможности

### 🔢 gcd_tool
- НОД списка из N ≥ 1 чисел
- Ввод/вывод через консоль или файл
- Обработка граничных случаев: пустой ввод, нули, отрицательные, нечисловые данные
- Ранний выход при НОД = 1

### 💾 backup_tool
- Рекурсивный поиск `*.conf`, `*.ini`, `*.cfg`, `*.yaml`, `*.yml`, `*.json`
- Timestamp-архивы `config_backup_YYYYMMDD_HHMMSS.tar.gz`
- `manifest.json` с SHA-256 хэшами
- Проверка целостности без распаковки
- Сохранение `*.bak` при конфликтах
- Логирование
- 4 команды: `backup`, `restore`, `verify`, `list`

## 🚀 Установка

```bash
git clone https://github.com/<username>/gcd-backup-tool.git
cd gcd-backup-tool
```

## 🔢 Использование — НОД

```bash
# Интерактивно
python src/gcd_tool.py

# Из файла → в консоль
python src/gcd_tool.py --input numbers.txt

# Из файла → в файл
python src/gcd_tool.py -i numbers.txt -o result.txt
```

**Коды выхода:** `0` успех · `1` пустой список · `2` файл не найден · `3` ошибка формата.

## 💾 Использование — Backup

```bash
python src/backup_tool.py backup  --source ./config --dest ./backups
python src/backup_tool.py verify  --archive backups/cfg_XXX.tar.gz
python src/backup_tool.py restore --archive backups/cfg_XXX.tar.gz --target ./config
python src/backup_tool.py list    --dest ./backups
```

## 🗂 Структура

```
gcd-backup-tool/
├── README.md, README.en.md, LICENSE, .gitignore
├── docs/     (TZ.md, MAINTENANCE.md, TESTCASES.md)
├── src/      (gcd_tool.py, backup_tool.py)
└── tests/    (test_gcd.py, test_backup.py)
```

## 🧪 Тестирование

```bash
python -m unittest discover -s tests -v
```

Ожидаемый результат: `Ran 20 tests · OK`.

## 📚 Документация

| Файл | Назначение |
|------|-----------|
| [`docs/TZ.md`](docs/TZ.md) | Техническое задание |
| [`docs/MAINTENANCE.md`](docs/MAINTENANCE.md) | Регламент обслуживания |
| [`docs/TESTCASES.md`](docs/TESTCASES.md) | Тест-кейсы |
| [`README.en.md`](README.en.md) | English version |

## 📋 Матрица соответствия ТЗ

| ID | Модуль | Требование | Статус |
|----|--------|-----------|:---:|
| Ф-01 | gcd_tool | Ввод из консоли | ✅ |
| Ф-02 | gcd_tool | Ввод из файла | ✅ |
| Ф-03 | gcd_tool | НОД (Евклид) | ✅ |
| Ф-04 | gcd_tool | Вывод в консоль/файл | ✅ |
| Ф-05 | gcd_tool | Обработка ошибок | ✅ |
| Б-01…06 | backup_tool | Поиск, tar.gz, manifest, restore, *.bak, логи | ✅ |
| Д-01…04 | docs | README RU/EN, MAINTENANCE, TESTCASES | ✅ |

## 📄 Лицензия

MIT — см. [LICENSE](LICENSE).

---

**Выполнил:** ФИО студента, группа ИС-31  
**КГБ ПОУ ХПЭТ**, 2026
# 🐍 gcd-backup-tool

Python CLI: GCD of N numbers + backup/restore of config files.

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Tests](https://img.shields.io/badge/Tests-20%2F20-brightgreen)](tests/)

## About

Two independent CLI tools in **Python 3.10+**, no external dependencies:

- 🔢 `src/gcd_tool.py` — GCD of N numbers (Euclidean algorithm)
- 💾 `src/backup_tool.py` — timestamped `tar.gz` backups, SHA-256 verification, restore with `*.bak`

Practicum project at **KhPET College**, Khabarovsk.

## Features

- GCD of N ≥ 1 numbers, console/file input & output
- Handles edge cases: empty input, zeros, negatives, invalid tokens
- Recursive config search: `*.conf`, `*.ini`, `*.cfg`, `*.yaml`, `*.yml`, `*.json`
- Commands: `backup`, `restore`, `verify`, `list`
- SHA-256 integrity check without extraction
- Saves `*.bak` on restore conflicts
- Logging of all operations

## Installation

```bash
git clone https://github.com/<username>/gcd-backup-tool.git
cd gcd-backup-tool
```

## Usage — GCD

```bash
python src/gcd_tool.py
python src/gcd_tool.py --input numbers.txt
python src/gcd_tool.py -i numbers.txt -o result.txt
```

Exit codes: `0` success · `1` empty list · `2` file not found · `3` format error.

## Usage — Backup

```bash
python src/backup_tool.py backup  --source ./config --dest ./backups
python src/backup_tool.py verify  --archive <archive>
python src/backup_tool.py restore --archive <archive> --target ./config
python src/backup_tool.py list    --dest ./backups
```

## Testing

```bash
python -m unittest discover -s tests -v
```

Expected: `Ran 20 tests · OK`.

## Documentation

- [`docs/TZ.md`](docs/TZ.md) — Technical specification
- [`docs/MAINTENANCE.md`](docs/MAINTENANCE.md) — Maintenance regulation
- [`docs/TESTCASES.md`](docs/TESTCASES.md) — Test cases
- [`README.md`](README.md) — Русская версия

## License

MIT — see [LICENSE](LICENSE).

---

**Author:** Student Name, group IS-31  
**KhPET College**, 2026
