# 🌐 Clipboard Share (Android Client)

> **Status:** 🚧 In Closed Beta (Google Play Store) | **Version:** 2.0.0 (Release Candidate)

**Clipboard Share** is a privacy-first, cross-platform productivity tool. It utilizes a custom peer-to-peer (P2P) local mesh network to seamlessly synchronize clipboards and transfer massive files between devices without ever relying on third-party cloud servers.

### Dynamic Theming (Light & Dark Mode)

| Light Theme | Dark Theme |
| :---: | :---: |
| <img src="assets/send_light.jpg" width="250"/> | <img src="assets/send_dark.jpg" width="250"/> |
| <img src="assets/receive_light.jpg" width="250"/> | <img src="assets/receive_dark.jpg" width="250"/> |
| <img src="assets/status_light.jpg" width="250"/> | <img src="assets/status_dark.jpg" width="250"/> |

---

## 🚀 The Vision: Zero-Cloud, Zero-Trust
Modern file-sharing apps suffer from three fatal flaws: they require internet access, they limit file sizes, and they pose a massive privacy risk by routing personal clipboard data through company servers. 

Clipboard Share solves this by keeping 100% of network traffic restricted to your local network (LAN) using direct socket connections and military-grade cryptography.

## 🛠️ System Architecture & Protocols

While the source code is currently closed-source prior to the official Play Store launch, the underlying engine is built on the following architecture:

### 1. Custom Mesh Discovery (UDP)
Devices broadcast their presence via UDP packets on port `50001` every 2 seconds. The Android client manages a `ConcurrentHashMap` to track active nodes, automatically expiring devices that drop off the network to maintain a clean UI state.

### 2. Cryptographic Handshake (ECDH + AES-256)
Connections require explicit user consent via a full-screen Intent broadcast. Upon acceptance, the devices negotiate a secure session using **Elliptic-Curve Diffie-Hellman (secp256r1)**. The derived AES-256 keys are stored securely using Android's `EncryptedSharedPreferences`. All subsequent clipboard payloads are encrypted before transmission.

### 3. Asynchronous Payload Delivery (TCP)
*   **Clipboard Sync (Port `65432`):** Bypasses modern Android 10+ background clipboard restrictions using a dual Explicit-Push and Sync-On-Focus model.
*   **File Transfer (Port `65433`):** Uses a custom `BATCH|Manifest` protocol to send unlimited file sizes at raw Wi-Fi Direct/LAN speeds. Integrates deeply with Android's **Storage Access Framework (SAF)** to allow users to save files to custom directories outside the standard Downloads folder.

### 4. Modern Android Compliance
The application strictly adheres to Android 14 (API 34) standards, utilizing robust Foreground Services (`DATA_SYNC` types) and decoupled `BroadcastReceivers` to ensure stable background execution without triggering OS-level security reinforcement crashes.

---

## 🗺️ Roadmap

- [x] **V1.0:** Core UDP/TCP Engine and Cryptography 
- [x] **V2.0:** Single-Activity Architecture Refactor, SAF Integration, Dynamic Theming
- [ ] **Desktop Client:** Native Windows companion application
- [ ] **V3.0 (Off-Grid):** QR-Code & NFC Host-Card Emulation (HCE) handshakes to generate ad-hoc Wi-Fi Direct networks for transfers completely independent of a router.

---

## 👨‍💻 About the Developer
Built by **Joseph Ting**, a pre-university student and self-taught software engineer passionate about local-first networking, applied cryptography, and pushing the limits of Android hardware APIs.

*If you'd like to support the development of the Windows client and keep the app ad-free, consider buying me a coffee via the link in the app!*
