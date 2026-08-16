# Wild Kernels for GKI2 Devices 5.10+ Release #

**IMPORTANT DISCLAIMER**

> [!CAUTION]
> This software is provided for testing and educational purposes only. Use at your own risk. The developers are not responsible for any damage, data loss, or issues that may occur. Please ensure you have proper backups before installation.

Join the telegram here: https://t.me/WildKernelsTG

# Features
- [ReSukiSU](#resukisu)
- [Enhanced ZRAM](#enhanced-zram)
- [Re-Kernel](#re-kernel)
- [DroidSpaces-OSS](#droidspaces-oss)
- [Networking Improvements](#networking)
- [NTSync](#ntsync)
- [Misc](#misc)

<!-- NOTE: The anchor links above match GitHub's auto-generated heading IDs (derived from heading text). Do NOT add explicit {#id} heading attributes: GitHub's release-notes renderer does not support them and renders them as literal text. -->

## [ReSukiSU](https://github.com/hzzmonetvn/ReSukiSU/tree/main)

A kernel-based root solution for Android devices.

Manager: {{KSU_MANAGER}}

> [!IMPORTANT]
> For best compatiblity ensure your Manager Version and Kernel Version match eg. 30100 = 30100.

**Version**  
`{{KSU_VERSION}}`

**Tag**  
`{{KSU_GIT_TAG}}`

**Ref**
`{{RESUKISU_REF}}`

**Commit**  
`{{RESUKISU_COMMIT}}`

## Enhanced ZRAM

Includes the LZ4 NEON, LZ4K, LZ4KD and Oplus compression patch stack derived from [zzh20188/GKI_KernelSU_SUSFS](https://github.com/zzh20188/GKI_KernelSU_SUSFS). Kernel 6.12 is skipped until its upstream patch set becomes available.

## [Re-Kernel](https://github.com/Sakion-Team/Re-Kernel)

Re-Kernel is integrated as an in-tree driver with network activity support enabled.

## [DroidSpaces-OSS](https://github.com/ravindu644/Droidspaces-OSS)

A lightweight, LXC-inspired container runtime for Android and Linux. Run full Linux distributions natively with zero performance penalty.

## Networking

- BBRv1 - Improved TCP congestion control
- BBRv3 - Improved TCP congestion control — available for Android 12 (5.10) through Android 15 (6.6), Android 16 (6.12) coming soon
- Wireguard - Built-in VPN support
- IP Set & IPv6 NAT Support - Advanced firewall capabilities
- TTL Target Support - Network packet manipulation
- CAKE, fq, fq_codel - Traffic shaping and fair queuing for reduced lag and balanced bandwidth
- connmark - Connection marking for packet classification
- TCP congestion control - CUBIC, BIC, Westwood, and HTCP for optimized performance across different network conditions
- CIFS - Network filesystem support (SMB/CIFS sharing)

## Other Features

- TMPFS_XATTR - Extended attributes for tmpfs (Mountify support)
- TMPFS_POSIX_ACL - POSIX ACLs for tmpfs

## [NTSync](#ntsync)

Provide high-performance, low-latency synchronization primitives compatible with the Windows NT kernel API

## [Misc](#misc)

- Ptrace Leak Fix: For kernels < 5.16
- Unicode Fix: Prevent path traversal and other detections using non-printable Unicode codepoints [Experimental]
- BTF/eBPF Support: CONFIG_BTF, CONFIG_BPF_EVENTS, CONFIG_FUSE_BPF for debugging and eBPF tooling
- TMPFS_XATTR: Extended attributes for tmpfs (Mountify support)
- TMPFS_POSIX_ACL: POSIX ACLs for tmpfs

## Changelog

### This Release
- Added BBRv3 — available for Android 12 (5.10) through Android 15 (6.6)
- Added NTSync
- Ptrace Leak Fix - For kernels < 5.16
- Unicode Fix - Prevent path traversal and other detections using non-printable Unicode codepoints [Experimental]

## Recommended Tools

[Kernel Flasher](https://github.com/fatalcoder524/KernelFlasher)
- Recommended flashing utility

[PixelFlasher by badabing2005](https://github.com/badabing2005/PixelFlasher)
- Pixel phone flashing GUI utility with features.

## Installation Instructions

### Prerequisites
- Unlocked bootloader.
- Backup your current boot image.
- Have root access using Magisk / KernelSU / Apatch (Any forks).

### Via Kernel Flasher
Download the correct AnyKernel3 ZIP for your device.
If you previously used another root method, clean it up first:
a. Magisk: perform a complete uninstall after flashing the AnyKernel3 ZIP.
b. KSU LKM (boot/init_boot/vendor_boot‑patched): Flash back the stock boot/init_boot/vendor_boot depending on what you patched.
c. KSU GKI: if you are 100% sure you already flashed stock init_boot/boot/vendor_boot, no action is needed; otherwise, follow the same steps as KSU LKM.
d. APatch: remove /data/adb contents to avoid leftover root conflicts after flashing the AnyKernel3 ZIP.
Flash the ZIP to the active slot using Kernel Flasher.
Install the ReSukiSU Manager APK, same version as mentioned in the release notes.
Open the ReSukiSU app.
Reboot the device if you performed any cleanup in step 2

## Force Load Kernel Modules (Bypass) — flashing with `Bypass-Image`

> [!IMPORTANT]
> Most users do not need this. This option does not help bypass root-detection systems — it only replaces the kernel image used during flashing for compatibility workarounds.

**How to enable:**
- Set `do.flash_bypass=1`, in the anykernel.sh file within the AnyKernel3.zip. 

**Behavior:**
- If `do.flash_bypass=1` is set it will move `Bypass-Image` to replace the usual `Image` file prior to performing version checks and flashing.
- If `do.flash_bypass=1` is set and `Bypass-Image` is not found, the installer will abort with an error to avoid accidental forced flashing of an unintended image.

**Why / When to use:**
- Use this only when a `Normal` flash fails to boot due to kernel module incompatibilities.
