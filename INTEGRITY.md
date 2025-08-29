# Integrity & Provenance

Public key in the repo **euro-macromechanica-results**: [`keys/emm_pub_key.asc`](https://github.com/rleydev/euro-macromechanica-results/tree/main/keys/emm_pub_key.asc) (ASCII‑armored)  
**GPG key fingerprint (rleydev — thelaziestcat):** `4E53 DA03 D1A1 644E 6479  3C47 EEEC 0AFA 4D8A F0A7`

SHA-256, GPG signatures, OpenTimeStamps anchores - [/integrity/...](https://github.com/rleydev/euro-macromechanica-backtest-data/tree/main/integrity)

Import and inspect:
```bash
gpg --import keys/emm_pub_key.asc
gpg --show-keys --with-fingerprint keys/emm_pub_key.asc
```

---

## Quick Verify (any result folder)
```bash
# 1) Verify the signed manifest
gpg --verify artifacts.sha256.asc artifacts.sha256

# 2) Check file hashes
sha256sum -c artifacts.sha256
# macOS without sha256sum: shasum -a 256 -c artifacts.sha256
# (optional) OpenTimestamps:
ots verify artifacts.sha256   # or: ots verify artifacts.sha256.ots
```

> **Note:** A manifest line has the form `HASH␠␠FILENAME`. The hash is for **file contents** only; the filename/path is just a label for the checker.

---

# Verifying SHA‑256 Manifests That Contain Absolute Paths (EN)

Sometimes a published `artifacts.sha256` was created with **absolute file paths** (e.g., `/Users/name/.../file.svg`).  
The **hashes are still valid** — the path is only a label used by `sha256sum -c` to locate files.  
This guide shows how to verify signatures and hashes on **any machine**.

### TL;DR
1) Verify the **GPG signature on the original** `artifacts.sha256`.  
2) Create a **local copy** of the manifest with **relative names** and run `sha256sum -c` on that copy.

### 1) Verify the signature (original manifest)
```bash
gpg --verify artifacts.sha256.asc artifacts.sha256
# (Optional) OpenTimestamps
ots verify artifacts.sha256   # or: ots verify artifacts.sha256.ots
```

### 2) Rebase paths locally and check hashes

**Linux / macOS (bash)**
```bash
sed -E 's#^([0-9a-f]{64})  .*/([^/]+)$#  #' artifacts.sha256 > artifacts.local.sha256
sha256sum -c artifacts.local.sha256
```
> The `sed` command keeps the 64‑hex digest and replaces the path with just the filename.

**Windows (PowerShell)**
```powershell
Get-Content artifacts.sha256 | % {
  if ($_ -match '^([0-9a-f]{64})\s\s(.+)$') {
    "$($matches[1])  $(Split-Path $matches[2] -Leaf)"
  }
} | Set-Content artifacts.local.sha256

# In Git Bash / WSL:
# sha256sum -c artifacts.local.sha256
```

### Notes & FAQs
- **Why doesn’t it match automatically?**  
  `sha256sum -c` tries to open files _by the path in the manifest_. If that path is absolute and doesn’t exist on your machine, it prints `No such file or directory`. The **digest itself is still correct**.
- **Do paths affect the hash?**  
  No. The SHA‑256 is computed **only from file contents**.
- **Can I verify a single file manually?**  
  Yes:
  ```bash
  sha256sum somefile.svg
  # Compare the 64‑hex digest with the first column in artifacts.sha256
  ```
- **GPG/OTS best practice**  
  Verify **GPG** on the original `artifacts.sha256`. For convenience, you may keep both files side‑by‑side:
  - `artifacts.sha256` (original, signed; may contain absolute paths)  
  - `artifacts.local.sha256` (your local rebased copy for `-c` checks)

### (Optional) macOS without GNU tools
```bash
# Create a simple, sorted manifest with relative names
ls -1 | grep -v '^artifacts\.sha256$' | LC_ALL=C sort | xargs shasum -a 256 > artifacts.local.sha256

# Verify a single file’s digest:
shasum -a 256 somefile.svg
```

---

# Проверка SHA‑256‑манифестов с абсолютными путями (RU)

Иногда опубликованный `artifacts.sha256` создан с **абсолютными путями** (например, `/Users/name/.../file.svg`).  
**Хэши при этом корректны** — путь в строке служит лишь «ярлыком» для `sha256sum -c`, чтобы найти файл.  
Ниже — как проверить подписи и хэши на **любой машине**.

### TL;DR
1) Проверьте **подпись GPG** исходного `artifacts.sha256`.  
2) Создайте **локальную копию** манифеста с **относительными именами** и выполните `sha256sum -c` по этой копии.

### 1) Проверка подписи (исходный манифест)
```bash
gpg --verify artifacts.sha256.asc artifacts.sha256
# (опционально) OpenTimestamps
ots verify artifacts.sha256   # или: ots verify artifacts.sha256.ots
```

### 2) «Перебазирование» путей локально и проверка хэшей

**Linux / macOS (bash)**
```bash
sed -E 's#^([0-9a-f]{64})  .*/([^/]+)$#  #' artifacts.sha256 > artifacts.local.sha256
sha256sum -c artifacts.local.sha256
```
> Команда `sed` сохраняет 64‑символьный hex‑хэш и заменяет путь на одно имя файла.

**Windows (PowerShell)**
```powershell
Get-Content artifacts.sha256 | % {
  if ($_ -match '^([0-9a-f]{64})\s\s(.+)$') {
    "$($matches[1])  $(Split-Path $matches[2] -Leaf)"
  }
} | Set-Content artifacts.local.sha256

# В Git Bash / WSL:
# sha256sum -c artifacts.local.sha256
```

### Примечания и FAQ
- **Почему «не совпадает» автоматически?**  
  `sha256sum -c` пытается открыть файл **по пути из манифеста**. Если путь абсолютный и его нет на вашей машине — будет `No such file or directory`. **Сами хэши при этом верны**.
- **Влияет ли путь на хэш?**  
  Нет. SHA‑256 считается **только от содержимого** файла.
- **Можно проверить один файл вручную?**  
  Да:
  ```bash
  sha256sum somefile.svg
  # Сравните 64‑символьный хэш с первой колонкой в artifacts.sha256
  ```
- **Практика GPG/OTS**  
  Подпись **GPG** проверяйте на исходном `artifacts.sha256`. Для удобства держите рядом обе версии:
  - `artifacts.sha256` (исходный, подписанный; может содержать абсолютные пути)  
  - `artifacts.local.sha256` (ваша локальная копия для проверок `-c`)

### (Опционально) macOS без GNU‑утилит
```bash
# Создать простой отсортированный манифест с относительными именами
ls -1 | grep -v '^artifacts\.sha256$' | LC_ALL=C sort | xargs shasum -a 256 > artifacts.local.sha256

# Проверка отдельного файла:
shasum -a 256 somefile.svg
```

---

