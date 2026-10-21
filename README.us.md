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
**Completed by:** Guseva Darya Sergeevna, group ISP-31                                                                                                             
**Educational institution:** KGB POU «Khabarovskiy promyshlenno-ekonomicheskiy tekhnikum»                                                                          
**Year:** 2026

