# Realme sm8450 kernel from LineageOS added KSUN + SuSFS 1.5.8

- Fork of kernel for sm8450 from LineageOS with added KSUN Nightly which is root solution and hiding by SuSFS 1.5.8.
- All features, except OverlaysFS Auto Kstat Support on SuSFS, proceed into an invisible root experience for all apps, including Revolut, bank, ChatGPT, goverment apps etc.
- Custom-modified boot, dtbo, AnyKernel package, kernel images, and source code on every release.
- Not working Pixelify files in KernelSU (use a LSPosed module for unlimited GPhotos backup).

## Warranty & Liability Disclaimer  

I am not responsible if you brick your device, erase data, kill your SD card, install malware, burn the battery, trigger thermonuclear war, or get fired because an alarm app failed.  
**You must be the rightful owner of the device you are modifying and have the legal right to alter its software.**  

All guides, binaries, and source code are provided **“AS IS,” without any express or implied warranty.** You apply them at your own risk. If you blame me for messing up your device, I will laugh at you.  
For the full terms, see our **[Legal Notice](https://frpunlocking.com/legal)**.

This software is distributed under the **GNU General Public License v2 (GPL-2.0)**, modifications licensed by [Pawel Potacki](potacki.com). See `LICENSE.md` for full terms.

## Supported devices with LineageOS 22.2

- Realme GT2 pro
  - SoC: sm8450, Qualcomm Snapdragon 8 Gen 1
  - codename: ferrari
  - IDs:
    - RMX3300,
    - RMX3301.
  - On v1 newest release based on KernelSU Next `Stable` branch.

### Possible supported devices 

**Note:** They can work with AnyFlasher3 (in v1)
 
- OnePlus 10 Pro
  - SoC: sm8450, Qualcomm Snapdragon 8 Gen 1
  - codename: wly
  - Needs testers, please also write [post in XDA](https://xdaforums.com/t/kernel-unofficial-ksun-next-susfs-realme-10-pro-lineageos-22-2-with-spoofing-realme-ui-6-0-stable-5-4-292-qgki-frpunlocking-15-0.4745580/) if it is working in any way.     

## Installation Steps for luigi/oscar

Tested on GT2 Pro (ferrari):

- [lineage-22.2-20250626-UNOFFICIAL-ferrari](https://github.com/pjgowtham/android_device_realme_ferrari/releases/tag/lineage-22.2-20250626-UNOFFICIAL-ferrari) - don't working fingerprint, and many things, you cannot downgrade /data
- [lineage-22.2-20250608-UNOFFICIAL-ferrari](https://github.com/pjgowtham/android_device_realme_ferrari/releases/tag/lineage-22.2-20250608-UNOFFICIAL-ferrari) - recommended

If you don't have LineageOS [recovery ferrari](https://github.com/pjgowtham/android_device_realme_ferrari/releases/download/lineage-22.0-20241107-UNOFFICIAL-ferrari/recovery.img) or you can flash everything by [TWRP with data decrypt](https://github.com/pjgowtham/recovery_device_oplus_ferrarri/releases/tag/twrp-3.7.1_12-0_OPLUS-20240214-03-ferrarri) if your USB port is broken.

After flashing LineageOS and/or MindTheGApps, boot into LOS recovery fastboot (preffered) or factory fastboot and flash [latest files](https://github.com/frpunlocking-com/android_kernel_oneplus_sm8450/releases), you have 2 methods to flash kernel by `adb sideload` or `fastboot flash`.

1. Method by AnyKernel package is recommended

  - In LineageOS recovery go to `adb sideload` on GT2 Pro (ferrari family):

```
adb sideload 1.0.0_KernelSUNext_SuSFS_AnyKernel_GT2_Pro_LineageOS_22.2.zip
```

2. Alternative method by fastboot:

```
fastboot flash boot_a boot.img
fastboot flash boot_b boot.img 
fastboot reboot
```

After device boots, install [Kernel SU Next Manager v1.0.8 (Latest Nightly)](https://nightly.link/KernelSU-Next/KernelSU-Next/workflows/build-manager-ci/next/Manager.zip). Confirmed safe for dirty flash on 2025-06-14 to 2025‑06‑28 build, no data loss observed. Works seamlessly with MindTheGapps.

## Kernel Highlights

- Built on Linux 5.10.228-gki from @pjgowtham - includes upstream Android GKI compliance patches and driver patches in `/drivers/power` and included `lineage-23.0` kernel modules.
- KernelSU Next - latest version providing root access.
- SuSFS v1.5.8 - Android dynamic rootfs support for root hiding.

## Enhancements & Fixes

- Seamless GKI‑based kernel integration for the real Realme GT2 Pro device built from scratch.
- No bootloops or data errors in testing on real device as of 2025‑07‑05.
- Generated fingerprint is without `-dirty` and it is clean in many detectors app.

## Known Issues

No issues have been reported so far, but if any problems arise, please report them in the official thread on XDA or create a GitHub issue with a detailed description of the situation and attach screenshots or videos from the detectors.

## Changelog

All notable changes to this project are documented in this file.

### v1.0.0

#### Added

- Support for Realme GT2 Pro and possible rest like OnePlus 10 Pro.
- Initial integration of KSUN `Stable` and SuSFS 1.5.8.
- Included the [Yuri Keybox](https://github.com/dpejoh/yurikey/releases/) suggestion to enable passing Google Play Strong Integrity checks (with latest Play Services and Vending).

## Data Insights for Tech Enthusiasts

The development of this kernel modification was primarily driven by Google's ongoing attempts to block rooted devices via Play Integrity API checks - an action that we, as developers and researchers, strongly oppose. Root access is essential for thorough security research, and its restriction undermines transparency and the right to repair. This custom kernel was carefully crafted to bypass these limitations, integrating KernelSU and SuSFS into an older 5.4 LineageOS kernel.

These kernel modifications are part of an academic project related to my master's thesis on the security analysis of consumer electronics at the military university. Modifying a legacy Chinese-modified Realme 10 Pro kernel was quite a challenge - imagine trying to assemble IKEA furniture without any instructions, missing half the screws, and using pieces meant for a completely different set. Yes, it was precisely that entertaining.

## Credits & Resources

- KernelSU & KernelSU Next.
- SuSFS, susfs4ksu, and Wild Kernels.
- Big thanks to the Realme GT2 Pro [device dev](https://github.com/pjgowtham/), testers, and the MindTheGapps maintainers and devs.

## How do I submit patches to Android Common Kernels

1. BEST: Make all of your changes to upstream Linux. If appropriate, backport to the stable releases.
   These patches will be merged automatically in the corresponding common kernels. If the patch is already
   in upstream Linux, post a backport of the patch that conforms to the patch requirements below.
   - Do not send patches upstream that contain only symbol exports. To be considered for upstream Linux,
additions of `EXPORT_SYMBOL_GPL()` require an in-tree modular driver that uses the symbol -- so include
the new driver or changes to an existing driver in the same patchset as the export.
   - When sending patches upstream, the commit message must contain a clear case for why the patch
is needed and beneficial to the community. Enabling out-of-tree drivers or functionality is not
not a persuasive case.

2. LESS GOOD: Develop your patches out-of-tree (from an upstream Linux point-of-view). Unless these are
   fixing an Android-specific bug, these are very unlikely to be accepted unless they have been
   coordinated with kernel-team@android.com. If you want to proceed, post a patch that conforms to the
   patch requirements below.

## Common Kernel patch requirements

- All patches must conform to the Linux kernel coding standards and pass `script/checkpatch.pl`
- Patches shall not break gki_defconfig or allmodconfig builds for arm, arm64, x86, x86_64 architectures
(see  https://source.android.com/setup/build/building-kernels)
- If the patch is not merged from an upstream branch, the subject must be tagged with the type of patch:
`UPSTREAM:`, `BACKPORT:`, `FROMGIT:`, `FROMLIST:`, or `ANDROID:`.
- All patches must have a `Change-Id:` tag (see https://gerrit-review.googlesource.com/Documentation/user-changeid.html)
- If an Android bug has been assigned, there must be a `Bug:` tag.
- All patches must have a `Signed-off-by:` tag by the author and the submitter

Additional requirements are listed below based on patch type

### Requirements for backports from mainline Linux: `UPSTREAM:`, `BACKPORT:`

- If the patch is a cherry-pick from Linux mainline with no changes at all
    - tag the patch subject with `UPSTREAM:`.
    - add upstream commit information with a `(cherry picked from commit ...)` line
    - Example:
        - if the upstream commit message is
```
        important patch from upstream

        This is the detailed description of the important patch

        Signed-off-by: Fred Jones <fred.jones@foo.org>
```
>- then Joe Smith would upload the patch for the common kernel as
```
        UPSTREAM: important patch from upstream

        This is the detailed description of the important patch

        Signed-off-by: Fred Jones <fred.jones@foo.org>

        Bug: 135791357
        Change-Id: I4caaaa566ea080fa148c5e768bb1a0b6f7201c01
        (cherry picked from commit c31e73121f4c1ec41143423ac6ce3ce6dafdcec1)
        Signed-off-by: Joe Smith <joe.smith@foo.org>
```

- If the patch requires any changes from the upstream version, tag the patch with `BACKPORT:`
instead of `UPSTREAM:`.
    - use the same tags as `UPSTREAM:`
    - add comments about the changes under the `(cherry picked from commit ...)` line
    - Example:
```
        BACKPORT: important patch from upstream

        This is the detailed description of the important patch

        Signed-off-by: Fred Jones <fred.jones@foo.org>

        Bug: 135791357
        Change-Id: I4caaaa566ea080fa148c5e768bb1a0b6f7201c01
        (cherry picked from commit c31e73121f4c1ec41143423ac6ce3ce6dafdcec1)
        [joe: Resolved minor conflict in drivers/foo/bar.c ]
        Signed-off-by: Joe Smith <joe.smith@foo.org>
```

### Requirements for other backports: `FROMGIT:`, `FROMLIST:`,

- If the patch has been merged into an upstream maintainer tree, but has not yet
been merged into Linux mainline
    - tag the patch subject with `FROMGIT:`
    - add info on where the patch came from as `(cherry picked from commit <sha1> <repo> <branch>)`. This
must be a stable maintainer branch (not rebased, so don't use `linux-next` for example).
    - if changes were required, use `BACKPORT: FROMGIT:`
    - Example:
        - if the commit message in the maintainer tree is
```
        important patch from upstream

        This is the detailed description of the important patch

        Signed-off-by: Fred Jones <fred.jones@foo.org>
```
>- then Joe Smith would upload the patch for the common kernel as
```
        FROMGIT: important patch from upstream

        This is the detailed description of the important patch

        Signed-off-by: Fred Jones <fred.jones@foo.org>

        Bug: 135791357
        (cherry picked from commit 878a2fd9de10b03d11d2f622250285c7e63deace
         https://git.kernel.org/pub/scm/linux/kernel/git/foo/bar.git test-branch)
        Change-Id: I4caaaa566ea080fa148c5e768bb1a0b6f7201c01
        Signed-off-by: Joe Smith <joe.smith@foo.org>
```


- If the patch has been submitted to LKML, but not accepted into any maintainer tree
    - tag the patch subject with `FROMLIST:`
    - add a `Link:` tag with a link to the submittal on lore.kernel.org
    - add a `Bug:` tag with the Android bug (required for patches not accepted into
a maintainer tree)
    - if changes were required, use `BACKPORT: FROMLIST:`
    - Example:
```
        FROMLIST: important patch from upstream

        This is the detailed description of the important patch

        Signed-off-by: Fred Jones <fred.jones@foo.org>

        Bug: 135791357
        Link: https://lore.kernel.org/lkml/20190619171517.GA17557@someone.com/
        Change-Id: I4caaaa566ea080fa148c5e768bb1a0b6f7201c01
        Signed-off-by: Joe Smith <joe.smith@foo.org>
```

### Requirements for Android-specific patches: `ANDROID:`

- If the patch is fixing a bug to Android-specific code
    - tag the patch subject with `ANDROID:`
    - add a `Fixes:` tag that cites the patch with the bug
    - Example:
```
        ANDROID: fix android-specific bug in foobar.c

        This is the detailed description of the important fix

        Fixes: 1234abcd2468 ("foobar: add cool feature")
        Change-Id: I4caaaa566ea080fa148c5e768bb1a0b6f7201c01
        Signed-off-by: Joe Smith <joe.smith@foo.org>
```

- If the patch is a new feature
    - tag the patch subject with `ANDROID:`
    - add a `Bug:` tag with the Android bug (required for android-specific features)

