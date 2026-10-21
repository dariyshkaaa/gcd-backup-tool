# gcd-backup-tool
Утилиты на Python: НОД списка чисел (Евклид) и резервное копирование конфигов (tar.gz + SHA-256). Полная документация.
# gcd-backup-tool

Консольные утилиты на Python: НОД списка чисел и резервное копирование конфигурационных файлов.

## Что это?

Две программы на Python:

- **gcd_tool.py** — находит наибольший общий делитель (НОД) списка чисел
- **backup_tool.py** — делает резервные копии конфигов и восстанавливает их

Обе работают без установки дополнительных программ. Только Python.

## Требования

- Python 3.10 или новее
- Windows, Linux или macOS

## Как запустить

### Проверка Python

Откройте командную строку (`Win + R`, введите `cmd`, Enter) и введите:

```
python --version
```

Должно появиться `Python 3.10` или больше. Если нет — установите Python с сайта python.org.

### Программа НОД

Откройте командную строку и перейдите в папку проекта:

```
cd Desktop\gcd-backup-tool
```

Интерактивный режим (вводите числа вручную):

```
python src\gcd_tool.py
```

Программа попросит ввести числа. Напишите, например, `12, 18, 24` и нажмите Enter. Появится результат — `НОД: 6`.

Из файла в консоль:

```
python src\gcd_tool.py --input numbers.txt
```

Из файла в файл:

```
python src\gcd_tool.py --input numbers.txt --output result.txt
```

### Программа резервного копирования

Создать резервную копию:

```
python src\backup_tool.py backup --source .\config --dest .\backups
```

Проверить целостность архива:

```
python src\backup_tool.py verify --archive backups\config_backup_20261021_120000.tar.gz
```

Восстановить файлы из архива:

```
python src\backup_tool.py restore --archive backups\config_backup_20261021_120000.tar.gz --target .\config
```

Показать список архивов:

```
python src\backup_tool.py list --dest .\backups
```

## Как запустить тесты

Откройте командную строку в папке проекта и введите:

```
python -m unittest discover -s tests -v
```

Появится список из 20 тестов, все должны быть `ok`, и в конце — `OK`.

## Структура проекта

```
gcd-backup-tool/
├── README.md            это описание
├── README.en.md         английская версия
├── LICENSE              лицензия MIT
├── .gitignore           служебный файл Git
├── docs/                документация
│   ├── TZ.md            техническое задание
│   ├── MAINTENANCE.md   регламент обслуживания
│   └── TESTCASES.md     тест-кейсы
├── src/                 исходный код
│   ├── gcd_tool.py      программа НОД
│   └── backup_tool.py   программа резервного копирования
├── tests/               тесты
│   ├── test_gcd.py
│   └── test_backup.py
└── images/              скриншоты
    ├── gcd_demo.png
    └── backup_demo.png
```

