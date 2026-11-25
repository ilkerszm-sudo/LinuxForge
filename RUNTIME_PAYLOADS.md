# Runtime payload inventory

| Payload | Provisioning reason | Expected location |
|---|---|---|
| PRoot | Android ABI-specific executable | `filesDir/runtime/<abi>/proot` |
| Debian/Ubuntu/Fedora rootfs | Large and frequently updated archives | `filesDir/containers/<name>/` |
| FreeBSD userland | Separate compatibility/emulation path | `filesDir/containers/<name>/` |
| Termux:X11 | Separate Android companion app | Installed Android package |
| XFCE/LXQt/KDE | Installed inside rootfs with distro package manager | Container filesystem |
| JDK/Android command-line tools/SDK/NDK | Large archives with individual licenses | `filesDir/toolchains/` |
| QEMU | ABI-specific native binaries | `filesDir/runtime/qemu/<abi>/` |
| VM disks and ISOs | User-selected, often multi-GB | `filesDir/vms/` |

Before release, maintain a signed payload manifest with version, URL, SHA-256, ABI, license and upstream project for every native executable/archive. Never download and execute an unverified binary.
