# 🛡️ Be Original

**Forensic Authenticity & Ground-Truth Recovery Engine for Android**

[![Android](https://img.shields.io/badge/Platform-Android%208.0%2B%20(API%2026%2B)-3DDC84?logo=android)](https://developer.android.com)
[![Kotlin](https://img.shields.io/badge/Kotlin-JVM%2011-7F52FF?logo=kotlin)](https://kotlinlang.org)
[![Jetpack Compose](https://img.shields.io/badge/UI-Jetpack%20Compose%20(Material%203)-4285F4?logo=jetpackcompose)](https://developer.android.com/jetpack/compose)
[![CI Build](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF?logo=githubactions)](./.github/workflows/android-cloud-build.yml)

**Be Original** is a hybrid edge-to-cloud media forensics and fact-verification Android application. Rather than simply flagging digital text or imagery as "suspicious," **Be Original** evaluates content across four distinct forensic pillars and reconstructs the **Original Ground Truth**—returning the unedited verbatim quote, baseline historical context, or earliest known primary source.

📄 **For full Executive (Non-Technical) and Engineering (Technical) documentation, see [RELEASE_DOCUMENTATION.md](./RELEASE_DOCUMENTATION.md).**

---

## ✨ Key Features

* **Overall Authenticity Scorecard (0–100%):** Instant, color-coded trust rating (`Authentic / Unmodified`, `Manipulated or AI-Assisted`, or `Synthetic / Fabricated`).
* **4-Pillar Forensic Breakdown:**
  1. **Modified / Edited Check:** Detects image splicing, localized re-compression, stripped camera headers, or selectively truncated quotes.
  2. **AI Involvement Detector:** Evaluates perplexity, burstiness, and diffusion artifacts to estimate LLM or synthetic image generation probability.
  3. **Scripted vs. Spontaneous Meter:** Analyzes structural syntax, rhetorical staging, and cadence to distinguish organic statements from rehearsed/PR-scripted copy.
  4. **Factuality & Fabrication Engine:** Cross-references assertions against primary records (`VERIFIED`, `MISLEADING`, `FABRICATED`, `ALTERED`, or `UNVERIFIABLE`).
* **On-Device Error Level Analysis (ELA) Heatmap:** Toggleable pixel-level compression delta overlay computed locally on the device CPU to visually expose spliced or photoshopped regions.
* **On-Device EXIF Telemetry Inspector:** Extracts raw file metadata (`TAG_SOFTWARE`, `TAG_MAKE`, `TAG_MODEL`, `TAG_DATETIME_ORIGINAL`) to catch editing software signatures (e.g., Adobe Photoshop, GIMP) or stripped provenance headers.
* **Recovered Original / Ground-Truth Card:** Dedicated anchor card providing the unedited baseline text, original context, and primary origin reference.
* **Native Android Share-Sheet Target (`Intent.ACTION_SEND`):** Verify dubious viral claims or images directly from WhatsApp, Chrome, X, or the Android Gallery without opening the app first.

---

## 🏗️ System Architecture

```text
[User Input / Android Share Sheet (Text or Image)]
                       │
                       ▼
     ┌───────────────────────────────────┐
     │   ON-DEVICE EDGE PRE-PROCESSOR    │
     │  (Kotlin Coroutines Dispatchers.IO)│
     ├───────────────────────────────────┤
     │ 1. Bitmap Downscaling (Max 960px) │
     │ 2. AndroidX ExifInterface Scan    │
     │ 3. 90% JPEG Re-compression &      │
     │    20x Pixel Delta ELA Heatmap    │
     └─────────────────┬─────────────────┘
                       │ Bundles Image + EXIF String + ELA Variance Score
                       ▼
     ┌───────────────────────────────────┐
     │   CLOUD VERIFICATION & RECOVERY   │
     │     (Gemini 2.5 Flash Engine)     │
     ├───────────────────────────────────┤
     │ • Multimodal Vision + Text Check  │
     │ • 4-Pillar Risk Scoring           │
     │ • Ground-Truth Source Recovery    │
     └─────────────────┬─────────────────┘
                       │ Strict 11-Field JSON Schema
                       ▼
     ┌───────────────────────────────────┐
     │    JETPACK COMPOSE MATERIAL 3 UI  │
     │ • Interactive ELA Heatmap Switch  │
     │ • Color-Coded Diagnostic Badges   │
     │ • Monospace Ground-Truth Card     │
     └───────────────────────────────────┘
