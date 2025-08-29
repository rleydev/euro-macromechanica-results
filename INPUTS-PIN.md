# 📌 PIN — Binding of Input Data to Results (Euro Macromechanica Backtest Results — EMM)

This file records **exactly which inputs** were used by the annual runs in this repository **euro‑macromechanica‑results** – (*Results*),
and points to the **canonical provenance & integrity artifacts** stored in the **euro‑macromechanica‑backtest‑data** – *Data Hub* repository.

---

## 🧭 What’s Bound

**Inputs for headline/stress runs** are sourced from the data repository:
**euro‑macromechanica‑backtest‑data** (*Data Hub*).

Minimum set for reproducibility:
- **Prepared M1 (UTC, cleaned minute bars)** — archive snapshot (SHA‑256/GPG/OTS).
- **Economic calendars (UTC timestamps of releases)** — archive snapshot (SHA‑256/GPG/OTS).

> **See the canonical binding description in *Data Hub*: [`INPUTS-PROVENANCE.md`](https://github.com/rleydev/euro-macromechanica-backtest-data/blob/main/INPUTS-PROVENANCE.md).**

---

## 🧾 Where artifacts live in this repository (Results)

Mirrored copies of hashes/signatures/OTS for the input **archive snapshots**:
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
  emm_pub_key.asc        # public key for GPG verification
```
> The public key and its fingerprint are also listed in the root `INTEGRITY.md` of this repository.

---

## 🔗 Mirrored anchors (for convenience) — canonical ones are in *euro-macromechanica-backtest-data* (Data Hub)

**Prepared minute data (archive snapshot)**  
- SHA‑256: `e81f26072b48e62eb37dcd4da9919608e05da871b7264d3718e01244a2658d5f`  
- GPG: `integrity/prepared/analyzed_full_2001-2025jul.tar.gz.sha256.asc`  
- OTS:  `integrity/prepared/analyzed_full_2001-2025jul.tar.gz.sha256.ots`  
- Bitcoin: txid `3646771ecc29d275b1b80ead9d5866a3b8867e6488df8d42145e2824a06e2a71`, block `910536`, time (UTC) `2025-08-18T02:06:26Z`

**Economic calendars (archive snapshot)**  
- SHA‑256: `0bd28458c49affc3b052116279827a8c840edf2dc4295d57a0b7e2a7b0b2e045`  
- GPG: `integrity/economic_calendars/jan2001-jul2025.tar.gz.sha256.asc`  
- OTS:  `integrity/economic_calendars/jan2001-jul2025.tar.gz.sha256.ots`  
- Bitcoin: txid `a95e00f437575dad58c5e074352b6f4c9637ace705eccb05aa936e1cb99c6ffb`, block `910177`, time (UTC) `2025-08-15T16:31:10Z`

> **Source of truth (pinned to commit):**  
> https://github.com/rleydev/euro-macromechanica-backtest-data/blob/40e0768e8403d12bec0466a5152175e6df44b00d — file `INPUTS-PROVENANCE.md` in the *Data Hub* repository.

---

## ✅ Quick check (≈60 seconds)

1) **SHA‑256:**  
   Download the input archives from *Data Hub* **or** use local copies, then:
   ```bash
   sha256sum <archive>     # macOS: shasum -a 256 <archive>
   # compare against integrity/inputs/<name>.sha256
   ```

2) **GPG:**  
   ```bash
   gpg --import keys/emm_pub_key.asc
   gpg --verify integrity/inputs/<name>.sha256.asc integrity/inputs/<name>.sha256
   ```

3) **OpenTimestamps (OTS):**  
   ```bash
   ots verify --no-bitcoin integrity/inputs/<name>.sha256.ots integrity/inputs/<name>.sha256
   ots info                integrity/inputs/<name>.sha256.ots   # block height / txid
   ```
> Record moments in **UTC** — some explorers display your local time zone by default.

---

## 🔗 Links

- Canonical input‑binding scheme in **euro‑macromechanica‑backtest‑data** (*Data Hub*):  
 [`euro‑macromechanica‑backtest‑data/INPUTS-PROVENANCE.md`](https://github.com/rleydev/euro-macromechanica-backtest-data/blob/main/INPUTS-PROVENANCE.md). 
- Integrity verification guide (Results):  
  [`INTEGRITY.md`](https://github.com/rleydev/euro-macromechanica-results/blob/main/INTEGRITY.md) (note about absolute paths in manifests)
- Annual result manifests:  
  `results/**/artifacts_YYYY.sha256` (+ `.asc`, `.ots` for headline)

---

## 📝 Notes

- This **PIN** is a short “staple” between **euro-macromechanica-results** (*Results*) and **euro-macromechanica-backtest-data** (*Data Hub*).
  The canonical artifacts for inputs live in the *Data Hub*; this repo keeps mirrored copies for convenience.
- Annual result manifests are **not** modified because of this PIN.
  They already enumerate the **exact input files** (prepared minutes, calendars) used for verification.
- If manifests contain **absolute paths**, this **does not** affect hash correctness.
  For local checks you can rebase to relative paths — see `INTEGRITY.md`.
