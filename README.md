РУССКИЙ <img src="https://flagcdn.com/24x18/ru.png" alt="RU" height="14"> 
# gcd-backup-tool
Утилиты на Python: НОД списка чисел (Евклид) и резервное копирование конфигов (tar.gz + SHA-256). Полная документация.
НОД и резервное копирование конфигураций

## 📋 Описание проекта

Работа по программированию. Набор консольных утилит на Python для решения двух задач: нахождение наибольшего общего делителя (НОД) списка чисел и создание/восстановление резервных копий конфигурационных файлов.


## 📚 Теоретическая справка

### Наибольший общий делитель (НОД)

НОД двух целых чисел `a` и `b` — это наибольшее целое число, которое делит и `a`, и `b` без остатка. Для его вычисления используется алгоритм Евклида, основанный на свойстве: `НОД(a, b) = НОД(b, a mod b)`.

Для списка из N чисел НОД вычисляется последовательно: сначала находится НОД первой пары, затем НОД результата и следующего числа, и так далее.

### Резервное копирование конфигураций

Алгоритм создает архив `tar.gz` с конфигурационными файлами (`*.conf`, `*.ini`, `*.cfg`, `*.yaml`, `*.yml`, `*.json`). Внутри архива сохраняется структура каталогов, а также файл `manifest.json` с метаданными (пути, размеры, хеш-суммы SHA-256). При восстановлении проверяется целостность каждого файла по хеш-сумме, а старая версия файла сохраняется с расширением `.bak`.

## 🛠️ Технологии

*   **Python 3.10+** — основной язык программирования.
*   **Стандартная библиотека:** `argparse`, `hashlib`, `json`, `tarfile`, `logging`, `tempfile`, `pathlib`, `shutil`.
*   **Модульное тестирование:** `unittest`.
*   **Система контроля версий:** Git, GitHub.

---

## 🚀 УСТАНОВКА И ЗАПУСК 

> **Инструкция рассчитана на Windows 10/11.** Если у вас macOS или Linux — см. раздел «🍎 macOS и Linux» в конце. Всё, что нужно — компьютер, интернет и 30 минут времени. Пароли и адреса записывайте на бумажку — пригодятся
### Часть 1. Проверка и установка Python

Python — программа, которая умеет «читать» наш код. Без неё ничего не запустится.

#### Шаг 1.1. Проверить, вдруг Python уже есть

1. Нажмите на клавиатуре одновременно **`Win`** (клавиша с флажком, слева внизу) и **`R`**. Появится маленькое окошко **«Выполнить»**.
2. В поле для ввода напечатайте:

   ```
   cmd
   ```

3. Нажмите **`Enter`** (самая большая клавиша справа). Откроется **чёрное окно** — командная строка. Не пугайтесь, это нормально.
4. В чёрном окне напечатайте:

   ```
   python --version
   ```

5. Нажмите **`Enter`**.

**Возможны два результата:**

- **Если появилось** `Python 3.10.x` или больше (например, `Python 3.12.1`) — **Python уже установлен**, переходите к Части 2.
- **Если появилось** `Python не является внутренней или внешней командой...` — **Python не установлен**, идите к шагу 1.2.

#### Шаг 1.2. Скачать Python

1. Откройте браузер (Chrome, Яндекс.Браузер, Edge).
2. В **адресной строке** сверху введите:

   ```
   python.org/downloads
   ```

3. Нажмите **`Enter`**.
4. На сайте найдите **большую жёлтую кнопку** **«Download Python 3.12.x»** и нажмите её. Начнётся скачивание в папку **«Загрузки»**.

#### Шаг 1.3. Установить Python

1. Нажмите **`Win + E`** — откроется «Проводник».
2. В левой колонке выберите **«Загрузки»**.
3. Найдите файл вроде **`python-3.12.x-amd64.exe`** и **двойной клик** по нему.
4. **⚠️ САМОЕ ВАЖНОЕ:** в первом окне установщика **в самом низу** есть галочка:

   ```
   ☐ Add python.exe to PATH
   ```

   **Обязательно поставьте её** (кликните по квадратику, чтобы появилась галочка ✅). Если не поставить — программа не заработает, придётся переустанавливать.

5. Нажмите **«Install Now»** — верхняя кнопка в окне.
6. Подождите 1–2 минуты. Появится надпись **«Setup was successful»** — установка завершена.
7. Нажмите **«Close»**.

#### Шаг 1.4. Проверить, что Python работает

1. Закройте старое чёрное окно (крестик в правом верхнем углу).
2. Снова **`Win + R`** → `cmd` → `Enter`.
3. Введите:

   ```
   python --version
   ```

4. Должно появиться `Python 3.12.x` (или другая цифра 3.10 и выше).

✅ **Python установлен.**

---

### Часть 2. Проверка и установка Git

Git — программа для отправки файлов на GitHub.

#### Шаг 2.1. Проверить, вдруг Git уже есть

В том же чёрном окне введите:

```
git --version
```

`Enter`.

**Если появилось** `git version 2.x.x` — **Git уже установлен**, переходите к Части 3.

**Если появилось** «не является внутренней...» — устанавливаем.

#### Шаг 2.2. Скачать Git

1. Откройте браузер.
2. Введите в адресной строке:

   ```
   git-scm.com/download/win
   ```

3. `Enter`. На странице нажмите **«Click here to download...»** (или подождите 2 секунды, начнётся сам).

#### Шаг 2.3. Установить Git

1. Откройте «Загрузки» (`Win + E` → «Загрузки»).
2. Найдите файл вроде **`Git-2.43.x-64-bit.exe`**, **двойной клик**.
3. Нажимайте **«Next»** (внизу окна) **раз 10 подряд** — все настройки по умолчанию правильные.
4. Когда дойдёте до кнопки **«Install»** — нажмите её.
5. Подождите 1 минуту. Появится **«Finish»** — нажмите её.

#### Шаг 2.4. Проверить Git

1. Закройте чёрное окно, откройте новое: `Win + R` → `cmd` → `Enter`.
2. Введите:

   ```
   git --version
   ```

3. Должно быть `git version 2.4x.x`.

✅ **Git установлен.**

---

### Часть 3. Скачать проект

Есть два способа.

#### Способ А (если преподаватель дал ссылку на репозиторий)

1. Откройте чёрное окно: `Win + R` → `cmd` → `Enter`.
2. Перейдите на Рабочий стол:

   ```
   cd %USERPROFILE%\Desktop
   ```

3. Скачайте проект:

   ```
   git clone https://github.com/ваш-username/gcd-backup-tool.git
   ```

   Замените `ваш-username` на имя из ссылки.
4. Перейдите в папку проекта:

   ```
   cd gcd-backup-tool
   ```

#### Способ Б (если создаёте проект вручную)

1. На Рабочем столе создайте папку **`gcd-backup-tool`** (правый клик → «Создать» → «Папку»).
2. Войдите в неё (двойной клик).
3. Внутри создайте четыре подпапки: **`docs`**, **`src`**, **`tests`**, **`images`** (правый клик → «Создать» → «Папку» — и вводите имя).
4. Создайте в них файлы по структуре (см. ниже «Структура проекта»). Для этого в каждой папке: правый клик → «Создать» → «Текстовый документ» → введите имя с расширением (например, `TZ.md`). Затем правый клик по файлу → «Открыть с помощью» → «Блокнот» — и вставьте содержимое.

**Проверка, что вы в правильной папке:**

В чёрном окне введите `dir`. Должны увидеть папки `docs`, `src`, `tests`, `images` и файлы `README.md`, `LICENSE`, `.gitignore`.

---

### Часть 4. Запуск программы НОД

#### Способ 1. Интерактивный ввод (числа вводите вручную)

1. Откройте чёрное окно **прямо в папке проекта** — простой способ:
   - Откройте папку `gcd-backup-tool` в Проводнике (двойной клик).
   - Вверху окна есть **адресная строка** с путём, например `C:\Users\Иван\Desktop\gcd-backup-tool`.
   - **Кликните один раз** по ней — она выделится синим.
   - Напечатайте вместо выделенного:

     ```
     cmd
     ```

   - Нажмите **`Enter`**. Откроется чёрное окно, но уже «внутри» папки проекта. В начале строки будет `C:\...\gcd-backup-tool>`.

2. Запустите программу:

   ```
   python src\gcd_tool.py
   ```

3. `Enter`. Программа покажет:

   ```
   Введите числа через пробел или запятую (пустая строка — завершить):
     Пример: 12, 18, 24
   ```

4. Напечатайте числа:

   ```
   12, 18, 24
   ```

5. `Enter`. Появится:

   ```
   ==================================================
   Входной список: [12, 18, 24]
   Количество чисел: 3
   НОД: 6
   ==================================================
   ```

✅ **Программа работает.**

#### Способ 2. Ввод из файла, вывод в консоль

1. В папке `gcd-backup-tool` создайте файл `numbers.txt` (через Блокнот).
2. Впишите в него числа, например:

   ```
   36 48 60
   ```

3. Сохраните и закройте.
4. В чёрном окне (в папке проекта) введите:

   ```
   python src\gcd_tool.py --input numbers.txt
   ```

5. `Enter`. Появится результат:

   ```
   ==================================================
   Входной список: [36, 48, 60]
   Количество чисел: 3
   НОД: 12
   ==================================================
   ```

#### Способ 3. Ввод из файла, вывод в файл

1. В чёрном окне введите:

   ```
   python src\gcd_tool.py --input numbers.txt --output result.txt
   ```

2. `Enter`. Программа напишет:

   ```
   Результат записан в файл: result.txt
   ```

3. Откройте файл `result.txt` в блокноте — там будет результат.

#### Коды выхода (что они означают)

| Код | Что это значит |
|-----|----------------|
| 0 | Всё хорошо |
| 1 | Пустой список чисел |
| 2 | Файл не найден |
| 3 | Ошибка ввода (буквы вместо чисел) |

---

### Часть 5. Запуск резервного копирования

#### Шаг 5.1. Подготовить тестовые конфиги

В чёрном окне (в папке проекта) введите по одной команде, после каждой — `Enter`:

```
mkdir config
```

```
echo key=value > config\app.ini
```

Появится папка `config` с файлом `app.ini` — это тестовый «конфиг».

#### Шаг 5.2. Создать резервную копию

Введите:

```
python src\backup_tool.py backup --source .\config --dest .\backups
```

`Enter`. Появится:

```
[INFO] Найдено 1 конфигов в config
[INFO]   + app.ini (10 байт)
[INFO] Архив создан: backups/config_backup_20261021_143022.tar.gz
Резервная копия: backups\config_backup_20261021_143022.tar.gz
```

**Имя архива с датой и временем** — у вас будет своё. Запишите его, оно понадобится дальше.

**Где найти результат:** откройте папку `gcd-backup-tool/backups` в Проводнике — там лежит файл `.tar.gz`.

#### Шаг 5.3. Проверить целостность

Введите (замените имя архива на своё из шага 5.2):

```
python src\backup_tool.py verify --archive backups\config_backup_20261021_143022.tar.gz
```

`Enter`. Появится:

```
[INFO]   OK: app.ini
Целостность: OK
```

#### Шаг 5.4. Восстановить файлы из архива

```
python src\backup_tool.py restore --archive backups\config_backup_20261021_143022.tar.gz --target .\config
```

`Enter`. Появится:

```
[INFO]   резерв: config\app.ini -> app.ini.bak
[INFO]   восстановлен: app.ini
Восстановлено файлов: 1
```

Рядом со старым `app.ini` появится `app.ini.bak` — это сохранённая старая версия.

#### Шаг 5.5. Посмотреть список архивов

```
python src\backup_tool.py list --dest .\backups
```

`Enter`. Появится:

```
config_backup_20261021_143022.tar.gz  (163 байт)
Всего архивов: 1
```

#### Коды выхода backup_tool

| Код | Что это значит |
|-----|----------------|
| 0 | Всё хорошо |
| 1 | Ошибка создания копии |
| 2 | Ошибка восстановления |
| 3 | Ошибка проверки |

---

### Часть 6. Запуск тестов

Тесты — это готовые проверки, что всё работает правильно.

1. Убедитесь, что чёрное окно открыто **в папке проекта** (`C:\...\gcd-backup-tool>`).
2. Введите:

   ```
   python -m unittest discover -s tests -v
   ```

3. `Enter`. Подождите 2 секунды. Появится:

   ```
   test_backup_creates_archive ... ok
   test_manifest_in_archive ... ok
   test_verify_ok ... ok
   test_restore_same_content ... ok
   test_restore_keeps_bak ... ok
   test_backup_no_configs ... ok
   test_two_positive ... ok
   test_two_coprime ... ok
   test_two_with_zero ... ok
   test_two_both_zero ... ok
   test_two_negative ... ok
   test_list_empty ... ok
   test_list_single ... ok
   test_list_multiple ... ok
   test_list_with_one ... ok
   test_list_with_zeros ... ok
   test_parse_spaces ... ok
   test_parse_commas ... ok
   test_parse_mixed ... ok
   test_parse_invalid ... ok
   ----------------------------------------------------------------------
   Ran 20 tests in 0.087s

   OK
   ```

**Если в конце `OK`** — все 20 тестов прошли, программа работает корректно. 🎉

---


### 🍎 macOS и Linux (кратко)

1. **Python:** проверьте `python3 --version`. Если нет — `brew install python3` (macOS) или `sudo apt install python3` (Ubuntu).
2. **Git:** проверьте `git --version`. Если нет — `brew install git` или `sudo apt install git`.
3. **Папки:** `mkdir -p ~/Desktop/gcd-backup-tool/{docs,src,tests,images}`.
4. **Файлы** — в любом текстовом редакторе (TextEdit, VS Code).
5. **Скриншоты:** `Cmd + Shift + 4` (macOS) или `Shift + Print Screen` (Linux).
6. **Git-команды** те же самые.

---

## 📁 Структура проекта

```
gcd-backup-tool/
├── README.md
├── README.en.md
├── LICENSE
├── .gitignore
├── docs/
│   ├── TZ.md
│   ├── MAINTENANCE.md
│   └── TESTCASES.md
├── src/
│   ├── gcd_tool.py
│   └── backup_tool.py
├── tests/
│   ├── test_gcd.py
│   └── test_backup.py
└── images/
    ├── gcd_demo.png
    └── backup_demo.png
```

## 💻 Использование модуля

### Базовое использование (НОД)

```python
from src.gcd_tool import gcd_list, parse_numbers

numbers = parse_numbers("12, 18, 24")
result = gcd_list(numbers)
print(f"НОД: {result}")  # НОД: 6
```

### Расширенное использование (Резервное копирование)

```python
from pathlib import Path
from src.backup_tool import backup, restore, verify

archive = backup(Path("./config"), Path("./backups"))
print(f"Архив создан: {archive}")

if verify(archive):
    print("Архив цел.")

restored_count = restore(archive, Path("./config"))
print(f"Восстановлено файлов: {restored_count}")
```

## 🔧 Основные функции

### `gcd_tool.py`

*   `gcd_two(a, b)` — НОД двух чисел (алгоритм Евклида).
*   `gcd_list(numbers)` — НОД списка чисел.
*   `parse_numbers(text)` — парсит строку с числами (пробелы, запятые, `;`).
*   `read_from_console()` — читает числа из консоли.
*   `read_from_file(path)` — читает числа из файла.
*   `write_to_console(numbers, result)` — выводит в консоль.
*   `write_to_file(path, numbers, result)` — записывает в файл.

### `backup_tool.py`

*   `backup(source, dest_dir)` — создаёт `tar.gz` с конфигами.
*   `restore(archive, target)` — восстанавливает с проверкой целостности.
*   `verify(archive)` — проверяет целостность.
*   `sha256_of(path)` — SHA-256 хеш файла.
*   `find_config_files(root, patterns)` — поиск конфигов по шаблонам.


## ✅ Тестирование

Проект покрыт 20 модульными тестами. Все тесты проходят успешно.

```
Ran 20 tests in 0.087s

OK
```
**Выполнила:** Гусева Дарья Сергеевна, группа ИСП-31  
**Учебное заведение:** КГБ ПОУ «Хабаровский промышленно-экономический техникум»  
**Год:** 2026
ENGLISH <img src="https://flagcdn.com/24x18/gb.png" alt="GB" height="14">
# gcd-backup-tool

Python utilities: GCD of a list of numbers (Euclidean algorithm) and backup of configuration files (tar.gz + SHA-256). Full documentation.

## 📋 Project description

Programming assignment. A set of Python console utilities for two tasks: computing the greatest common divisor (GCD) of a list of numbers and creating/restoring backups of configuration files.

---

## 📚 Theory

### Greatest common divisor (GCD)

The GCD of two integers `a` and `b` is the largest integer that divides both `a` and `b` without a remainder. It is computed using the Euclidean algorithm, based on the property: `GCD(a, b) = GCD(b, a mod b)`.

For a list of N numbers, the GCD is computed sequentially: first the GCD of the first pair, then the GCD of the result and the next number, and so on.

### Configuration backup

The algorithm creates a `tar.gz` archive containing configuration files (`*.conf`, `*.ini`, `*.cfg`, `*.yaml`, `*.yml`, `*.json`). The archive preserves the directory structure and includes a `manifest.json` file with metadata (paths, sizes, SHA-256 checksums). During restore, the integrity of each file is verified against its checksum, and the previous file version is saved with a `.bak` extension.

---

## 🛠️ Technologies

*   **Python 3.10+** — main programming language.
*   **Standard library:** `argparse`, `hashlib`, `json`, `tarfile`, `logging`, `tempfile`, `pathlib`, `shutil`.
*   **Unit testing:** `unittest`.
*   **Version control:** Git, GitHub.

---

## 🚀 INSTALLATION AND RUNNING

> **This guide is written for Windows 10/11.** If you use macOS or Linux, see the "🍎 macOS and Linux" section at the end. All you need is a computer, internet access, and 30 minutes of your time. Write down your passwords and addresses on paper — you will need them.

### Part 1. Checking and installing Python

Python is a program that can "read" our code. Nothing will run without it.

#### Step 1.1. Check whether Python is already installed

1. Press **`Win`** (the key with the Windows flag, bottom left) and **`R`** at the same time. A small **"Run"** window will appear.
2. In the input field, type:

   ```
   cmd
   ```

3. Press **`Enter`** (the largest key on the right). A **black window** will open — the command prompt. Don't be alarmed, this is normal.
4. In the black window, type:

   ```
   python --version
   ```

5. Press **`Enter`**.

**There are two possible outcomes:**

- **If you see** `Python 3.10.x` or higher (for example, `Python 3.12.1`) — **Python is already installed**, move on to Part 2.
- **If you see** `Python is not recognized as an internal or external command...` — **Python is not installed**, go to step 1.2.

#### Step 1.2. Download Python

1. Open your browser (Chrome, Firefox, Edge).
2. In the **address bar** at the top, type:

   ```
   python.org/downloads
   ```

3. Press **`Enter`**.
4. Find the **large yellow button** **"Download Python 3.12.x"** and click it. The download will start and the file will be saved to the **"Downloads"** folder.

#### Step 1.3. Install Python

1. Press **`Win + E`** — File Explorer will open.
2. In the left column, select **"Downloads"**.
3. Find the file named something like **`python-3.12.x-amd64.exe`** and **double-click** it.
4. **⚠️ THE MOST IMPORTANT PART:** in the first installer window, **at the very bottom**, there is a checkbox:

   ```
   ☐ Add python.exe to PATH
   ```

   **You must check it** (click on the box so that a ✅ tick appears). If you skip it, the program will not run and you will have to reinstall.

5. Click **"Install Now"** — the top button in the window.
6. Wait 1–2 minutes. A message **"Setup was successful"** will appear — installation is complete.
7. Click **"Close"**.

#### Step 1.4. Verify that Python works

1. Close the old black window (the X in the top right corner).
2. Press **`Win + R`** → `cmd` → `Enter` again.
3. Type:

   ```
   python --version
   ```

4. You should see `Python 3.12.x` (or any version 3.10 or higher).

✅ **Python is installed.**

---

### Part 2. Checking and installing Git

Git is a program for uploading files to GitHub.

#### Step 2.1. Check whether Git is already installed

In the same black window, type:

```
git --version
```

Press `Enter`.

**If you see** `git version 2.x.x` — **Git is already installed**, move on to Part 3.

**If you see** "is not recognized..." — proceed with the installation below.

#### Step 2.2. Download Git

1. Open your browser.
2. Type in the address bar:

   ```
   git-scm.com/download/win
   ```

3. Press `Enter`. On the page, click **"Click here to download..."** (or wait 2 seconds — the download starts automatically).

#### Step 2.3. Install Git

1. Open "Downloads" (`Win + E` → "Downloads").
2. Find the file named something like **`Git-2.43.x-64-bit.exe`** and **double-click** it.
3. Click **"Next"** (bottom of the window) **about 10 times in a row** — all default settings are correct.
4. When you reach the **"Install"** button — click it.
5. Wait 1 minute. A **"Finish"** button will appear — click it.

#### Step 2.4. Verify Git

1. Close the black window and open a new one: `Win + R` → `cmd` → `Enter`.
2. Type:

   ```
   git --version
   ```

3. You should see `git version 2.4x.x`.

✅ **Git is installed.**

---

### Part 3. Download the project

There are two options.

#### Option A (if the instructor provided a repository link)

1. Open the black window: `Win + R` → `cmd` → `Enter`.
2. Go to the Desktop:

   ```
   cd %USERPROFILE%\Desktop
   ```

3. Clone the project:

   ```
   git clone https://github.com/your-username/gcd-backup-tool.git
   ```

   Replace `your-username` with the username from the link.
4. Enter the project folder:

   ```
   cd gcd-backup-tool
   ```

#### Option B (if you are creating the project manually)

1. On the Desktop, create a folder **`gcd-backup-tool`** (right-click → "New" → "Folder").
2. Open it (double-click).
3. Inside, create four subfolders: **`docs`**, **`src`**, **`tests`**, **`images`** (right-click → "New" → "Folder" — then enter the name).
4. Create files in them according to the structure (see "Project structure" below). For each folder: right-click → "New" → "Text Document" → type the name with an extension (for example, `TZ.md`). Then right-click the file → "Open with" → "Notepad" — and paste the content.

**Check that you are in the right folder:**

In the black window, type `dir`. You should see the folders `docs`, `src`, `tests`, `images` and the files `README.md`, `LICENSE`, `.gitignore`.

---

### Part 4. Running the GCD program

#### Method 1. Interactive input (type numbers manually)

1. Open the black window **directly in the project folder** — a simple trick:
   - Open the `gcd-backup-tool` folder in File Explorer (double-click).
   - At the top of the window there is an **address bar** with the path, for example `C:\Users\John\Desktop\gcd-backup-tool`.
   - **Click once** on it — it will be highlighted in blue.
   - Type the following instead of the highlighted text:

     ```
     cmd
     ```

   - Press **`Enter`**. The black window will open, but already "inside" the project folder. The beginning of the line will be `C:\...\gcd-backup-tool>`.

2. Run the program:

   ```
   python src\gcd_tool.py
   ```

3. Press `Enter`. The program will display:

   ```
   Enter numbers separated by spaces or commas (empty line — finish):
     Example: 12, 18, 24
   ```

4. Type the numbers:

   ```
   12, 18, 24
   ```

5. Press `Enter`. You will see:

   ```
   ==================================================
   Input list: [12, 18, 24]
   Number count: 3
   GCD: 6
   ==================================================
   ```

✅ **The program works.**

#### Method 2. File input, console output

1. In the `gcd-backup-tool` folder, create a file named `numbers.txt` (using Notepad).
2. Enter the numbers, for example:

   ```
   36 48 60
   ```

3. Save and close.
4. In the black window (inside the project folder), type:

   ```
   python src\gcd_tool.py --input numbers.txt
   ```

5. Press `Enter`. You will see:

   ```
   ==================================================
   Input list: [36, 48, 60]
   Number count: 3
   GCD: 12
   ==================================================
   ```

#### Method 3. File input, file output

1. In the black window, type:

   ```
   python src\gcd_tool.py --input numbers.txt --output result.txt
   ```

2. Press `Enter`. The program will print:

   ```
   Result written to file: result.txt
   ```

3. Open the `result.txt` file in Notepad — the result will be there.

#### Exit codes (what they mean)

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Empty list of numbers |
| 2 | File not found |
| 3 | Input error (letters instead of numbers) |

---

### Part 5. Running the backup tool

#### Step 5.1. Prepare test configurations

In the black window (inside the project folder), type the following commands one at a time, pressing `Enter` after each:

```
mkdir config
```

```
echo key=value > config\app.ini
```

A folder `config` will appear with a file `app.ini` — this is a test configuration file.

#### Step 5.2. Create a backup

Type:

```
python src\backup_tool.py backup --source .\config --dest .\backups
```

Press `Enter`. You will see:

```
[INFO] Found 1 config files in config
[INFO]   + app.ini (10 bytes)
[INFO] Archive created: backups/config_backup_20261021_143022.tar.gz
Backup: backups\config_backup_20261021_143022.tar.gz
```

**The archive name contains a date and time** — yours will be different. Write it down; you will need it further.

**Where to find the result:** open the `gcd-backup-tool/backups` folder in File Explorer — the `.tar.gz` file is there.

#### Step 5.3. Verify the integrity

Type (replace the archive name with your own from step 5.2):

```
python src\backup_tool.py verify --archive backups\config_backup_20261021_143022.tar.gz
```

Press `Enter`. You will see:

```
[INFO]   OK: app.ini
Integrity: OK
```

#### Step 5.4. Restore files from the archive

```
python src\backup_tool.py restore --archive backups\config_backup_20261021_143022.tar.gz --target .\config
```

Press `Enter`. You will see:

```
[INFO]   backup: config\app.ini -> app.ini.bak
[INFO]   restored: app.ini
Files restored: 1
```

Next to the old `app.ini` file, a new `app.ini.bak` will appear — this is the saved previous version.

#### Step 5.5. List all archives

```
python src\backup_tool.py list --dest .\backups
```

Press `Enter`. You will see:

```
config_backup_20261021_143022.tar.gz  (163 bytes)
Total archives: 1
```

#### backup_tool exit codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Backup creation error |
| 2 | Restore error |
| 3 | Verification error |

---

### Part 6. Running tests

Tests are ready-made checks that everything works correctly.

1. Make sure the black window is open **inside the project folder** (`C:\...\gcd-backup-tool>`).
2. Type:

   ```
   python -m unittest discover -s tests -v
   ```

3. Press `Enter`. Wait 2 seconds. You will see:

   ```
   test_backup_creates_archive ... ok
   test_manifest_in_archive ... ok
   test_verify_ok ... ok
   test_restore_same_content ... ok
   test_restore_keeps_bak ... ok
   test_backup_no_configs ... ok
   test_two_positive ... ok
   test_two_coprime ... ok
   test_two_with_zero ... ok
   test_two_both_zero ... ok
   test_two_negative ... ok
   test_list_empty ... ok
   test_list_single ... ok
   test_list_multiple ... ok
   test_list_with_one ... ok
   test_list_with_zeros ... ok
   test_parse_spaces ... ok
   test_parse_commas ... ok
   test_parse_mixed ... ok
   test_parse_invalid ... ok
   ----------------------------------------------------------------------
   Ran 20 tests in 0.087s

   OK
   ```

**If the last line says `OK`** — all 20 tests passed, the program works correctly. 🎉

---

### 🍎 macOS and Linux (short version)

1. **Python:** check `python3 --version`. If not installed — `brew install python3` (macOS) or `sudo apt install python3` (Ubuntu).
2. **Git:** check `git --version`. If not installed — `brew install git` or `sudo apt install git`.
3. **Folders:** `mkdir -p ~/Desktop/gcd-backup-tool/{docs,src,tests,images}`.
4. **Files** — in any text editor (TextEdit, VS Code).
5. **Screenshots:** `Cmd + Shift + 4` (macOS) or `Shift + Print Screen` (Linux).
6. **Git commands** are the same.

---

## 📁 Project structure

```
gcd-backup-tool/
├── README.md
├── README.en.md
├── LICENSE
├── .gitignore
├── docs/
│   ├── TZ.md
│   ├── MAINTENANCE.md
│   └── TESTCASES.md
├── src/
│   ├── gcd_tool.py
│   └── backup_tool.py
├── tests/
│   ├── test_gcd.py
│   └── test_backup.py
└── images/
    ├── gcd_demo.png
    └── backup_demo.png
```

## 💻 Using the module

### Basic usage (GCD)

```python
from src.gcd_tool import gcd_list, parse_numbers

numbers = parse_numbers("12, 18, 24")
result = gcd_list(numbers)
print(f"GCD: {result}")  # GCD: 6
```

### Advanced usage (backup)

```python
from pathlib import Path
from src.backup_tool import backup, restore, verify

archive = backup(Path("./config"), Path("./backups"))
print(f"Archive created: {archive}")

if verify(archive):
    print("Archive is intact.")

restored_count = restore(archive, Path("./config"))
print(f"Files restored: {restored_count}")
```

## 🔧 Main functions

### `gcd_tool.py`

*   `gcd_two(a, b)` — GCD of two numbers (Euclidean algorithm).
*   `gcd_list(numbers)` — GCD of a list of numbers.
*   `parse_numbers(text)` — parses a string of numbers (spaces, commas, `;`).
*   `read_from_console()` — reads numbers from the console.
*   `read_from_file(path)` — reads numbers from a file.
*   `write_to_console(numbers, result)` — prints to the console.
*   `write_to_file(path, numbers, result)` — writes to a file.

### `backup_tool.py`

*   `backup(source, dest_dir)` — creates a `tar.gz` archive with config files.
*   `restore(archive, target)` — restores files with integrity checking.
*   `verify(archive)` — verifies archive integrity.
*   `sha256_of(path)` — computes the SHA-256 hash of a file.
*   `find_config_files(root, patterns)` — finds configuration files by patterns.

---

## ✅ Testing

The project is covered by 20 unit tests. All tests pass successfully.

```
Ran 20 tests in 0.087s

OK
```
Completed by: Guseva Darya Sergeevna, group ISP-31
Educational institution: KGB POU «Khabarovskiy promyshlenno-ekonomicheskiy tekhnikum» 
Year: 2026
