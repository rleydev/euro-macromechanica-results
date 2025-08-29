# 📊 Политика качества данных (M1→M5, intraday стратегия EMM на 5 мин)

---

## 📄 Пререгистрация и происхождение

Этот документ фиксирует, что **Политика качества данных** (v1.0) — в частности **гейт по разрывам 5–10 минут** — была
**заморожена до генерации headline‑результатов** и **независимо от PnL**.  
В качестве пререгистрации использована **CSV‑таблица**, которая материализует пороги и годовые метки.

## Каноничные артефакты
- **Каноничный текст политики (EN):** `data_quality_policy/policy_v1.0.md`  
- **Анкер пререгистрации (CSV):** `data_quality_policy/data_quality_table.csv`

### Доказательство якорения (Bitcoin) для CSV
- **TABLE_SHA256:** `4dc3fb3cb02354ae686829180fb02b064c221426de9817b4d3751cb8248d8c6b`  
- **Подпись GPG:** `integrity/data_quality_policy/data_quality_table.csv.sha256.asc`  
- **OpenTimestamps (OTS):** `integrity/data_quality_policy/data_quality_table.csv.sha256.ots`  
- **Запись в Bitcoin:** **блок 911 080**,  
  **txid** `a93495aa3fe087d999893241d01a56cf5067680afa04b61afe71f4ce454c305c`,  
  **время** **2025‑08‑21T20:27:52Z (UTC)**.

> Некоторые обозреватели показывают локальную зону. В этой документации время фиксируется в **UTC**.

## Как проверить
```bash
# 1) GPG (проверка подписи файла с SHA‑256)
gpg --verify data_quality_policy/data_quality_table.csv.sha256.asc \
            data_quality_policy/data_quality_table.csv.sha256

# 2) SHA‑256 (пересчитать и сравнить)
sha256sum data_quality_policy/data_quality_table.csv
# macOS: shasum -a 256 data_quality_policy/data_quality_table.csv

# 3) OpenTimestamps (без локальной ноды Bitcoin)
ots verify --no-bitcoin data_quality_policy/data_quality_table.csv.sha256.ots \
           data_quality_policy/data_quality_table.csv.sha256
ots info   data_quality_policy/data_quality_table.csv.sha256.ots
```

## Связь между текстом политики и якорем CSV
- **Текст политики** (`policy_v1.0.md`) описывает обоснование и **гейтинг‑правило** (разрывы 5–10 мин, `< 120`, плюс ±10% для пометки «погранично»).  
- **CSV‑таблица** — это пререгистрированная, машиночитаемая **материализация** этого правила (годовые метки и счётчики).  
- Будущие правки (если будут) должны повышать **версию** политики и выпускать новый CSV **с новыми хэшами/OTS**; текущий якорь остаётся неизменяемым доказательством того, что было зафиксировано **на тот момент**.

- **Текст перевода:** [`policy_v1.0.ru.md`](https://github.com/rleydev/euro-macromechanica-results/tree/main/data_quality_policy/policy_v1.0.ru.md)  
- **Назначение:** только для удобства чтения. **Юридически значимым** остаётся английский оригинал `policy_v1.0.md`.

> **Важно:** для русской версии **не публикуются** отдельные SHA-256/GPG/OTS.  
> Все проверки целостности выполняются **по английскому каноничному файлу** и таблице: см. артефакты в `../integrity/data_quality_policy/` и инструкцию в `INTEGRITY.md`.