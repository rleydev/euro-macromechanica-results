# 📌 PIN — привязка входных данных к результатам (Euro Macromechanica / EMM)

Этот файл фиксирует, **какими именно входами** пользовались годовые прогоны в этом репозитории **euro‑macromechanica‑results** – (*Results*),  
и отсылает к каноничным артефактам происхождения/целостности в репозитории **euro‑macromechanica‑backtest‑data** – *Data Hub*.

---

## 🧭 Что привязано

**Входы для headline/stress‑прогонов** берутся из репозитория данных:  
**euro‑macromechanica‑backtest‑data** (*Data Hub*).

Минимальный набор для воспроизводимости:
- **Prepared M1 (UTC, очищенные минутки)** — архив‑снимок (SHA‑256/GPG/OTS).  
- **Economic calendars (UTC публикаций)** — архив‑снимок (SHA‑256/GPG/OTS).  

> **Каноничное описание связки входов см. в *Data Hub*: [`INPUT-PROVENANCE.md`](https://github.com/rleydev/euro-macromechanica-backtest-data/blob/main/INPUTS-PROVENANCE.md). Ру версия [`INPUT-PROVENANCE.ru.md`](https://github.com/rleydev/euro-macromechanica-backtest-data/blob/main/INPUTS-PROVENANCE.md).**

---

## 🧾 Где лежат артефакты в этом репозитории (Results)

Зеркальные копии хэшей/подписей/OTS для входных **архивов‑снимков**:
```
integrity/
  inputs/
    analyzed_full_2001-2025jul.tar.gz.sha256
    analyzed_full_2001-2025jul.tar.gz.sha256.asc
    analyzed_full_2001-2025jul.tar.gz.sha256.ots
    jan2001-jul2025.tar.gz.sha256
    jan2001-jul2025.tar.gz.sha256.asc
    jan2001-jul2025.tar.gz.sha256.ots
keys/
  emm_pub_key.asc        # публичный ключ для GPG‑проверки
```
> Публичный ключ и его отпечаток приведены также в корневом `INTEGRITY.md` этого репозитория.

---

### Mirrored anchors (for convenience) — canonical in euro-macromechanica-backtest-data (Data Hub)

**Prepared minute data (archive snapshot)**  
- SHA-256: `e81f26072b48e62eb37dcd4da9919608e05da871b7264d3718e01244a2658d5f`  
- GPG: `integrity/prepared/analyzed_full_2001-2025jul.tar.gz.sha256.asc`  
- OTS:  `integrity/prepared/analyzed_full_2001-2025jul.tar.gz..sha256.ots`  
- Bitcoin: txid `<3646771ecc29d275b1b80ead9d5866a3b8867e6488df8d42145e2824a06e2a71>`, block `<910536>`, time (UTC) `2025-08-18T02:06:26Z`  

**Economic calendars (archive snapshot)**  
- SHA-256: `0bd28458c49affc3b052116279827a8c840edf2dc4295d57a0b7e2a7b0b2e045`  
- GPG: `integrity/economic_calendars/jan2001-jul2025.tar.gz..sha256.asc`  
- OTS:  `integrity/economic_calendars/jan2001-jul2025.tar.gz..sha256.ots`  
- Bitcoin: txid `a95e00f437575dad58c5e074352b6f4c9637ace705eccb05aa936e1cb99c6ffb`, block `910177`, time (UTC) `2025-08-15T16:31:10Z`

> Canonical source of truth (pinned to commit):  
> https://github.com/rleydev/euro-macromechanica-backtest-data/blob/40e0768e8403d12bec0466a5152175e6df44b00d/INPUTS-PROVENANCE.md

---

## ✅ Быстрая проверка (60 секунд)

1) **SHA‑256:**  
   Скачайте архивы входов из *Data Hub* **или** используйте локальные копии, затем:
   ```bash
   sha256sum <archive>     # macOS: shasum -a 256 <archive>
   # сравните с содержимым integrity/inputs/<name>.sha256
   ```

2) **GPG:**  
   ```bash
   gpg --import keys/emm_pub_key.asc
   gpg --verify integrity/inputs/<name>.sha256.asc integrity/inputs/<name>.sha256
   ```

3) **OpenTimestamps (OTS):**  
   ```bash
   ots verify --no-bitcoin integrity/inputs/<name>.sha256.ots integrity/inputs/<name>.sha256
   ots info                integrity/inputs/<name>.sha256.ots   # высота блока / txid
   ```
> Момент времени фиксируйте в **UTC**: некоторые обозреватели показывают локальную зону.

---

## 🔗 Ссылки

- Каноничная схема привязки входов **euro-macromechanica-backtest-data** (Data Hub):  
  [`euro‑macromechanica‑backtest‑data/INPUTS-PROVENANCE.md`](https://github.com/rleydev/euro-macromechanica-backtest-data/blob/main/INPUTS-PROVENANCE.md). Ру перевеод – [`euro‑macromechanica‑backtest‑data/INPUTS-PROVENANCE.ru.md`](https://github.com/rleydev/euro-macromechanica-backtest-data/blob/main/INPUTS-PROVENANCE.ru.md)
- Гайд по проверке целостности (Results):  
  [`INTEGRITY.md`](https://github.com/rleydev/euro-macromechanica-results/blob/main/INTEGRITY.md) (заметка про абсолютные пути в манифестах)
- Годовые манифесты результатов:  
  `results/**/artifacts_YYYY.sha256` (+ `.asc`, `.ots` для headline)

---

## 📝 Примечания

- Этот **PIN** — краткая «скрепка» между **euro-macromechanica-results** (*Results*) и **euro-macromechanica-backtest-data** (*Data Hub*).  
  Каноничными для входов считаются артефакты в *Data Hub*; здесь хранится их зеркальная копия для удобства.
- Годовые манифесты результатов не изменяются под этот PIN.  
  Они уже перечисляют **точные файлы входов** (prepared минутки, календари), по которым проходит верификация.
- Если в манифестах встречаются **абсолютные пути**, это **не влияет** на корректность хэшей.  
  Для локальной проверки можно «перебазировать» пути на относительные — см. `INTEGRITY.md`.
