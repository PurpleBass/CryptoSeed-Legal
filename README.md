CryptoSeed

CryptoSeed is an iOS app that provides local, offline, user-controlled encryption for text and files, with a clean native UI and optional Shortcuts automation.

It uses Apple CryptoKit only, runs entirely on-device, and does not use servers, user accounts, cloud storage, analytics, or external cryptography libraries.

All cryptographic operations happen locally, under the user’s control.

⸻

What CryptoSeed Is (and Is Not)

✅ CryptoSeed is
    •    A native iOS app for encrypting and decrypting text and files
    •    A local-first cryptography tool with no network dependency
    •    A way to manage symmetric keys and asymmetric identities
    •    A system for secure key sharing using public-key cryptography
    •    An automation-friendly cryptography engine exposed via Shortcuts / App Intents
    •    An educational and auditable reference for applied cryptography on iOS

❌ CryptoSeed is not
    •    A password manager
    •    A cloud service
    •    A messaging app
    •    A DRM system
    •    A replacement for end-to-end encrypted messengers

⸻

Threat Model

CryptoSeed is designed to protect against:
    •    Accidental exposure of sensitive text or files
    •    Curious apps or users without the correct keys
    •    File interception during sharing
    •    Device compromise without access to encryption keys

CryptoSeed does not protect against:
    •    Malware with full device access
    •    An attacker who already has your keys
    •    Losing all backups and keys

CryptoSeed gives you control, not guarantees against poor key management.

⸻

Core Design Principles
    •    🔐 Local-only cryptography (no servers, no sync)
    •    🧱 Apple CryptoKit only
    •    🔑 Keys stored securely in iOS Keychain
    •    📱 Fully usable via native iOS UI
    •    ⚡ Automation-ready via Shortcuts
    •    📂 Files decrypt back to usable formats
    •    📖 Explainable, auditable, and transparent

⸻

Cryptography Overview

Algorithms Used
    •    Symmetric encryption: ChaCha20-Poly1305
    •    Asymmetric key agreement: X25519
    •    Key derivation: HKDF-SHA256
    •    Authentication: AEAD (via ChaChaPoly)

All cryptography is provided by Apple CryptoKit.

⸻

Symmetric Encryption

Capabilities
    •    Encrypt / decrypt text
    •    Encrypt / decrypt files
    •    Uses named 256-bit symmetric keys stored in Keychain

File Behavior
    •    invoice.pdf → invoice.pdf.seed
    •    Decrypts back to invoice.pdf
    •    Files open normally in Files / Preview

Key Management
    •    Keys are generated securely (random, 256-bit)
    •    Stored in iOS Keychain
    •    Keys can be:
    •    Created
    •    Deleted
    •    Exported securely
    •    Imported from backups

⸻

Asymmetric Encryption (Public Key)

Identities
    •    Each identity is an X25519 keypair
    •    Private keys stored securely in Keychain
    •    Default identity: Personal Device Key

Capabilities
    •    Encrypt text to a recipient public key
    •    Encrypt files to a recipient public key
    •    Decrypt using your private identity
    •    Export / import identities securely

File Behavior
    •    photo.jpg → photo.jpg.seed
    •    Decrypts back to photo.jpg

⸻

Secure Key Sharing (Key Wrapping)

CryptoSeed supports secure transport of symmetric keys using asymmetric cryptography.

Why this matters
    •    Symmetric keys are fast and ideal for files
    •    Asymmetric keys are ideal for sharing
    •    CryptoSeed combines both correctly

How it works
    1.    A symmetric key is encrypted (wrapped) using a recipient’s X25519 public key
    2.    The wrapped blob can be shared openly
    3.    The recipient decrypts it using their private identity
    4.    The symmetric key is stored securely in Keychain

This enables:
    •    Secure backups
    •    Secure sharing
    •    Device migration
    •    Family or team workflows

⸻

Identity Backup & Restore
    •    Identity private keys can be:
    •    Encrypted with a symmetric key
    •    Exported as a Base64 blob
    •    Restored later under a new name

⚠️ Identity backups are extremely sensitive.
Treat them like master keys.

⸻

iOS Keychain Behavior
    •    Keys are stored per app
    •    Deleting the app deletes its Keychain items

Therefore:
    •    Deleting CryptoSeed without backups makes encrypted data inaccessible
    •    CryptoSeed provides export mechanisms to avoid lock-in

This behavior is intentional and transparent.

⸻

Shortcuts & Automation

CryptoSeed optionally exposes cryptography as building blocks for Apple Shortcuts:
    •    Encrypt files before uploading to cloud storage
    •    Securely share keys using public-key cryptography
    •    Build custom privacy-preserving workflows
    •    Combine with Files, Share Sheets, QR codes, AirDrop

The native app UI covers everyday usage.
Shortcuts enable advanced automation.

⸻

License

CryptoSeed is proprietary software.

Source code is provided for transparency and auditability only.
No reuse, redistribution, or derivative works are permitted.

⸻

Final Note

CryptoSeed does not try to hide cryptography.
It exposes it — clearly, honestly, and locally.

If you understand your keys, you control your data.
