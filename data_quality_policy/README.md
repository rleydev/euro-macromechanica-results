# 📏 Data Quality Policy (M1→M5, EURUSD M5)

This folder contains the **canonical** English policy text (with integrity artifacts) and an **informational** Russian translation.

---

## EN — Canonical

**Canonical policy text:** [`data_quality_policy/policy_v1.0.md`](https://github.com/rleydev/euro-macromechanica-results/tree/main/data_quality_policy/policy_v1.0.md)  
**Gating table:** [`data_quality_policy/data_quality_table.csv`](https://github.com/rleydev/euro-macromechanica-results/tree/main/data_quality_policy/data_quality_table.csv)

## Policy Preregistration & Provenance — Data Quality Policy (EMM Backtest)

This note documents that the **Data Quality Policy** (v1.0) — specifically the gate based on **5–10 minute gaps** —
was **pre‑registered before generating headline results** and **independently of PnL**.  
The preregistration anchor is the **CSV table** that operationalizes the policy thresholds and year labels.

**Headline rule (short):**
- 2001–2008 → ❌ DROP (used only as STRESS).
- For 2009+ → ✅ OK if yearly **5–10-minute gap** count `cnt_5_10 < 120`.  
- ⚠️ BORDERLINE if `|cnt_5_10 − 120| ≤ 12` (label only; gating still `< 120`).

---

## Canonical artifacts

- **Canonical policy text (EN):** `data_quality_policy/policy_v1.0.md`
- **Preregistration anchor (CSV):** `data_quality_policy/data_quality_table.csv`

### Bitcoin‑anchored proof for the CSV table
- **TABLE_SHA256:** `4dc3fb3cb02354ae686829180fb02b064c221426de9817b4d3751cb8248d8c6b`  
- **GPG signature:** `integrity/data_quality_policy/data_quality_table.csv.sha256.asc`  
- **OpenTimestamps (OTS):** `integrity/data_quality_policy/data_quality_table.csv.sha256.ots`  
- **Anchored (Bitcoin):** **block 911,080**,  
  **txid** `a93495aa3fe087d999893241d01a56cf5067680afa04b61afe71f4ce454c305c`,  
  **timestamp** **2025‑08‑21T20:27:52Z (UTC)**.

> Some explorers display local time. For clarity, all timestamps here are in **UTC**.

---

## How to verify

```bash
# 1) GPG (verify the signed SHA256 file)
gpg --verify data_quality_policy/data_quality_table.csv.sha256.asc \
            data_quality_policy/data_quality_table.csv.sha256

# 2) SHA‑256 (recompute and compare)
sha256sum data_quality_policy/data_quality_table.csv
# macOS: shasum -a 256 data_quality_policy/data_quality_table.csv

# 3) OpenTimestamps (no local Bitcoin node required)
ots verify --no-bitcoin data_quality_policy/data_quality_table.csv.sha256.ots \
           data_quality_policy/data_quality_table.csv.sha256
ots info   data_quality_policy/data_quality_table.csv.sha256.ots
```
If your OTS toolkit shows a human “X hours ago” label, remember it reflects **your local clock**; prefer the explicit **UTC** above.

---

## Relationship between policy text and CSV anchor
- The **policy text** (`policy_v1.0.md`) explains the rationale and the **gate** (5–10m gaps, `< 120`, with ±10% label tolerance).  
- The **CSV anchor** is the preregistered, machine‑readable **instantiation** of that rule (per‑year labels and counts).  
- Future updates (if any) should bump the policy **version** and publish a fresh CSV **with new hashes/OTS**; the existing anchor remains an immutable record of what was decided **at that time**.

> **Versioning:** `v1.0` · Status: **FROZEN** · Published: `2025-08-21 (UTC)`  
> **Canonical SHA-256 (policy EN):** `PASTE_SHA256_HERE`

---

## Quick links

- Canonical policy (EN): [`policy_v1.0.md`](https://github.com/rleydev/euro-macromechanica-results/tree/main/data_quality_policy/policy_v1.0.md)  
- Gating table (CSV): [`data_quality_table.csv`](https://github.com/rleydev/euro-macromechanica-results/tree/main/data_quality_policy/data_quality_table.csv)  
- Integrity artifacts: [`integrity/data_quality_policy/`](https://github.com/rleydev/euro-macromechanica-results/tree/main/integrity/data_quality_policy/)  
- Verification guide: [`INTEGRITY.md`](https://github.com/rleydev/euro-macromechanica-results/tree/main/INTEGRITY.md)
