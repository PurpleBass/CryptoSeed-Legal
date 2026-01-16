CryptoSeed

CryptoSeed is an iOS app that provides local, offline, user-controlled encryption for text, files, and cryptographic keys using Apple CryptoKit and Shortcuts / App Intents.

It does not use servers, user accounts, cloud storage, analytics, or external cryptography libraries.
All cryptographic operations happen entirely on-device, under the user’s control.

CryptoSeed acts as a cryptographic toolbox and transport layer for iOS automation.

⸻

What CryptoSeed Is (and Is Not)

✅ CryptoSeed is
    •    A local encryption engine for iOS
    •    A Shortcuts-first cryptography tool
    •    A way to encrypt and decrypt text and files
    •    A way to manage symmetric keys and asymmetric identities
    •    A way to securely share keys between devices or people
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
    •    Accidental exposure of sensitive files or text
    •    Curious apps or users without the correct keys
    •    File interception during sharing
    •    Device compromise without access to keys

CryptoSeed does not protect against:
    •    Malware with full device access
    •    An attacker who already has your keys
    •    You losing all backups and keys

CryptoSeed gives you control, not guarantees against poor key management.

⸻

Core Design Principles
    •    🔐 Local-only cryptography (no servers, no sync)
    •    🧱 Apple CryptoKit only
    •    🔑 Keys stored in iOS Keychain
    •    🧩 Composable via Shortcuts
    •    📂 Files decrypt back to usable formats
    •    📖 Explainable and auditable

⸻

Cryptography Overview

Algorithms Used
    •    Symmetric Encryption: ChaCha20-Poly1305
    •    Asymmetric Key Agreement: X25519
    •    Key Derivation: HKDF-SHA256
    •    Authentication: AEAD (built into ChaChaPoly)

All cryptography is provided by Apple CryptoKit.

⸻

Symmetric Encryption

Capabilities
    •    Encrypt / decrypt text
    •    Encrypt / decrypt files
    •    Uses named 256-bit symmetric keys stored in Keychain

File Behavior
    •    invoice.pdf → invoice.pdf.cseed
    •    Decrypts back to invoice.pdf
    •    Files open normally in Files / Preview

Key Management
    •    Keys are generated securely (random, 256-bit)
    •    Stored in iOS Keychain
    •    Can be:
    •    Created
    •    Deleted
    •    Exported securely
    •    Imported from backups

⸻

Asymmetric Encryption (Public Key)

Identities
    •    Each identity is an X25519 keypair
    •    Private keys stored securely in Keychain
    •    Default identity: “Personal Device Key”

Capabilities
    •    Encrypt text to a recipient public key
    •    Encrypt files to a recipient public key
    •    Decrypt using your private identity
    •    Export / import identities securely

File Behavior
    •    photo.jpg → photo.jpg.cseedasym
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
    •    Team or family workflows

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
    •    Therefore:
    •    Deleting CryptoSeed without backups makes encrypted data inaccessible
    •    CryptoSeed provides export mechanisms to avoid lock-in

This is intentional and transparent.

⸻

Shortcuts & App Intents

CryptoSeed exposes cryptography as building blocks for Shortcuts:
    •    Encrypt before uploading to cloud storage
    •    Securely share keys via public key
    •    Build custom secure workflows
    •    Combine with Files, Share Sheets, QR codes, AirDrop

CryptoSeed stays small. Shortcuts do the orchestration.

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
