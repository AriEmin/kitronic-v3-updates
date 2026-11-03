# Kitronic V3 updates

Distribution repository for the independent Kitronic V3 native Android application and ESP32-S3 ONEBOARD firmware.

[Download releases](https://github.com/AriEmin/kitronic-v3-updates/releases)

**Initial builds are bench previews. Physical BLE, electrical, hydraulic and OTA acceptance has not been performed.** A basic electrical/pressure/leak test is included; full legacy piston/gear control and the nine-phase gearbox test suite are not included.

- Android 8+, phone/tablet, portrait/landscape.
- Turkish and English built in; additional supported languages use downloadable Google ML Kit translation models. Automatic translation is powered by [Google Translate](https://developers.google.com/ml-kit/language/translation) and can contain errors.
- Bonded, authenticated BLE; device name `KitronicV3-<MAC suffix>`.
- Device-local calibration and profiles; safe disarm on connection loss.
- Basic coil/pressure/leak tests and local CSV/PDF report sharing.
- Signed update catalog and firmware authorization; APK package/signing-certificate/hash validation.

## Installation

Install the APK from a release. First firmware installation requires USB on an **8 MB ESP32-S3-DevKitM-1 ONEBOARD**. The `factory.bin` file is a combined image for address 0x0; it initializes NVS, so back up existing calibration first. The `firmware.bin` file is the OTA application image.

At the USB console (115200), send `pin` to display the device-specific Bluetooth pairing PIN. Verify hardware mapping and pressure calibration before confirming the device profile and enabling outputs. VESC node 10, 500 kbit CAN, status-9 feedback and a <=1 s controller-command timeout are expected.

Subsequent firmware updates run through Android → Settings → Updates, with outputs disabled. Interrupted transfers leave the previous application active. Automatic rollback after a successfully installed but faulty build is not enabled; USB recovery is required in that case.

Android updates require the operating system's installation confirmation. This is not a silent device-management installer.

## Update feed and security

Feed: `https://github.com/AriEmin/kitronic-v3-updates/releases/latest/download/updates.json`

The catalog uses an ECDSA P-256/SHA-256 signed payload. Firmware separately verifies its signed model/version/size/hash descriptor. V1 uses a separate repository and trust key. This repository contains no private signing keys, device passkeys or GitHub access tokens.

A release being marked “latest” serves the update-feed URL; it does not certify physical validation. Read the release notes and verification artifacts for the exact build status.
