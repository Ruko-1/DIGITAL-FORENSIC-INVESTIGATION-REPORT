# DIGITAL-FORENSIC-INVESTIGATION-REPORT
Digital forensic investigation, MFT timeline analysis, and deleted data recovery for Case AIT-DF-2026-009 using FTK Imager and Autopsy.
# Digital Forensic Investigation & Data Recovery (Case ID: AIT-DF-2026-009)

[![Forensics](https://img.shields.io/badge/Domain-Digital%20Forensics%20%26%20Incident%20Response-blue.svg)](#)
[![OS](https://img.shields.io/badge/FileSystem-NTFS-green.svg)](#)
[![Status](https://img.shields.io/badge/Status-Completed-success.svg)](#)

## 🏢 Executive Summary

This repository contains the complete forensic evidence processing logs, timeline reconstructions, cross-tool verification analyses, and final investigation documentation for **Case ID: AIT-DF-2026-009** conducted for **Apex Integrated Technologies Ltd.**

The investigation was commissioned to evaluate a data-deletion incident involving six target corporate directories (**SSH**, **My pic**, **Our pic**, **ADDS Project**, **Corel**, and **Corel Draw Work**). Through multi-tool forensic analysis, 1,162 deleted file entries were identified and processed, establishing both file recoverability and a defensible deletion timeframe.

---

## 🛠️ Forensic Tools & Utilities Used

* **Exterro FTK Imager (v8.3.0.27):** MFT structure inspection, unallocated space analysis, and `$RECYCLE.BIN` artifact extraction.
* **Autopsy (v4.23.1):** Forensic disk ingest, PhotoRec file carving, metadata timestamp extraction, and automated event timeline generation.
* **`dd` & R-Drive Image:** Raw sector image verification, container integrity validation, and partition geometry checks.
* **Windows PowerShell (`Get-FileHash`):** Cryptographic verification (SHA-256) for evidence integrity and exported file verification.

---

## 🔍 Key Findings & Analysis Summary

| Target Directory | MFT Status | Recycle Bin Status | Recoverability | Primary Method Used |
| :--- | :--- | :--- | :--- | :--- |
| **`SSH`** | Deleted (`[root]`) | Bypassed / Purged | **Fully Recoverable** | FTK Imager Export / Autopsy FS |
| **`Corel`** | Deleted (`[root]`) | Bypassed / Purged | **Fully Recoverable** | FTK Imager Export / Autopsy FS |
| **`corel draw work`** | Deleted (`[root]`) | Bypassed / Purged | **Fully Recoverable** | FTK Imager Export / Autopsy FS |
| **`My pic`** | Unallocated Pointer | Bypassed / Purged | **Recoverable** | Autopsy PhotoRec File Carving |
| **`Our pic`** | Unallocated Pointer | Bypassed / Purged | **Recoverable** | Autopsy PhotoRec File Carving |
| **`ADDS Project`** | Unallocated Pointer | Bypassed / Purged | **Recoverable** | Autopsy Carving & Keyword Search |

### Critical Timeline Artifacts
* **Primary Deletion Event:** `2026-09-16 11:01:30 WAT` (Recorded via `$STANDARD_INFO` Change Time across MFT records).
* **Recycle Bin Interaction:** `2026-09-24 11:42:43 WAT` (Creation timestamp for user SID `S-1-5-21-1622753870...` `desktop.ini`).

---

## 🔒 Evidence Cryptographic Verification

Mathematical immutability was established by comparing baseline acquisition hashes against working copy computations:

* **Evidence File:** `Evidence.E01`
* **Algorithm:** SHA-256
* **Hash Value:** `6216149FDDF6EB7074349AFAEF226F02C3B246EE6C3C3AE91C5AB7ADEB8C29E0`
* **Integrity Status:** **100% VERIFIED / UNTAMPERED**

To independently verify the evidence image in PowerShell:
```powershell
Get-FileHash -Path ".\Evidence.E01" -Algorithm SHA256
