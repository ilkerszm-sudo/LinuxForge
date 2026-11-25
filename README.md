# LinuxForge — Android source project

LinuxForge is an Android/Jetpack Compose project for managing Linux root filesystems and development workspaces on Android.

## Included source
- Android Studio project (Kotlin + Jetpack Compose)
- Persistent container registry and rootfs download/extraction helper
- PRoot command adapter and runtime integration point
- Package/update command builders for Debian/Ubuntu, Fedora and FreeBSD
- XFCE, LXQt and KDE launch profiles for Termux:X11
- Android SDK/NDK/JDK/Kotlin workspace bootstrap scripts
- QEMU VM configuration helper, encrypted AI key vault, file and command helpers
- GitHub Actions Android build workflow

## Current implementation status
The current Compose screen is a navigation/UI prototype. The engine and helper modules provide starting integration code, but the tabs are not yet fully wired into complete end-to-end workflows. In particular, a production PTY terminal, foreground session service, robust archive traversal-safe extractor, real package-manager UI, AI network client/streaming, and full VM lifecycle controller still require implementation and device testing.

## Runtime payloads are provisioned separately
This ZIP does **not** embed complete Linux root filesystems, Android SDK/NDK archives, JDK distributions, QEMU/PRoot executable binaries, or Termux:X11. These are large, architecture-specific or separately licensed/distributed payloads. Integration points and provisioning scripts are included, but payloads must be obtained from trusted upstreams and checksum-verified. Termux:X11 is a companion Android app and must be installed separately.

FreeBSD is experimental: it is not a Linux PRoot rootfs and needs a compatible userland/emulation strategy. Package command helpers are present, but the standard Linux desktop flow is not guaranteed to work on FreeBSD.

## Build
Open in Android Studio with JDK 17, Android SDK platform 35 and matching build tools. Then run `gradle wrapper` once (wrapper is not included) and `./gradlew assembleDebug`. The GitHub Actions workflow builds a debug APK after you push the project to your own repository.

## Compatibility and production work
- minSdk 26; PRoot must match device ABI and kernel behavior.
- `chroot` requires root and is not enabled by default.
- Termux:X11 integration depends on companion app availability and its supported launch intents.
- QEMU software emulation can be slow; acceleration is device/kernel dependent.
- Production long-running sessions need a foreground service and lifecycle handling.
- Rootfs extraction must reject path traversal and escaping symlinks; verify downloaded archive checksums before extraction.
- Pass command arguments as arrays; never concatenate untrusted user input into shell commands.
