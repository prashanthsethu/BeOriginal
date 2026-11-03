Changelog

All notable changes to the Be Original Android project (https://github.com/prashanthsethu/BeOriginal) will be documented in this file.

The format is based on Keep a Changelog, and this project adheres to Semantic Versioning.
[1.0.0] - 2026-11-03
Added

    Core Verification Pipeline (MainActivity.kt): Implemented hybrid edge-to-cloud forensic engine combining on-device image inspection with gemini-2.5-flash multimodal reasoning.

    4-Pillar Forensic Scoring: Added structured evaluation and UI cards for:

        Modification & Tampering Risk (modifiedScore & modifiedDetails)

        AI Generation Probability (aiScore & aiDetails)

        Scripted vs. Spontaneous Analysis (scriptedScore & scriptedDetails)

        Factuality & Fabrication Status (factualityStatus & factualityDetails)

    Ground-Truth Recovery Engine: Added dedicated Recovered Original / Ground Truth anchor card displaying verbatim unedited quotes, baseline facts, and primary origin references (originalOutput & originalSourceUrl).

    On-Device Error Level Analysis (ELA): Built local computeErrorLevelAnalysis() processor performing 90% JPEG re-compression and 20x RGB channel delta amplification to generate an interactive tamper heatmap bitmap (ARGB_8888) and mean variance telemetry score.

    On-Device EXIF Metadata Scanner: Integrated androidx.exifinterface:exifinterface:1.3.7 (extractExifForensics()) to inspect camera make/model, original capture timestamps, and editing software tags (TAG_SOFTWARE).

    Android Share-Sheet Integration (AndroidManifest.xml): Registered Intent.ACTION_SEND intent filters for text/plain and image/* so users can forward content directly from external apps into Be Original.

    Memory-Safe Image Ingestion: Added loadScaledBitmap() utility to constrain input bitmaps to a maximum dimension of 960px prior to ELA pixel processing and network upload.

    Cloud CI/CD Workflow (.github/workflows/android-cloud-build.yml): Configured automated GitHub Actions pipeline using ubuntu-latest and Temurin JDK 17 to compile ./gradlew assembleDebug in the cloud and publish BeOriginal-debug-apk artifacts.

    Official Release Documentation (RELEASE_DOCUMENTATION.md): Added complete non-technical executive summary and technical architecture specifications.

Fixed

    Gradle Configuration Hierarchy: Separated root project plugin declarations (build.gradle.kts) from app module dependencies (app/build.gradle.kts) to resolve Unresolved reference 'implementation' sync errors.
    EOF
