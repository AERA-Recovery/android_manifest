# AERA Recovery Project manifest

This is the Android 16 source manifest for AERA Recovery Project. It combines
the normal Android, LineageOS, and TeamWin sources with the private AERA forks
required to reproduce the current Dodge recovery build.

All AERA-owned projects are hosted in the private
[`AERA-Recovery`](https://github.com/AERA-Recovery) GitHub organization. Access
to that organization and an SSH key registered with GitHub are required before
syncing.

## Sync

```bash
mkdir -p ~/android/AERA_16.0
cd ~/android/AERA_16.0
repo init -u git@github.com:AERA-Recovery/android_manifest.git -b aera-16.0
repo sync -c --force-sync --no-clone-bundle --no-tags -j$(nproc)
```

The manifest intentionally keeps unchanged platform dependencies on their
normal upstream remotes. AERA repositories are used for every recovery fork and
for every source tree carrying an AERA-specific change.

## Build for OnePlus 13 (`dodge`)

```bash
cd ~/android/AERA_16.0
source build/envsetup.sh
lunch twrp_dodge-bp2a-eng
mka adbd recoveryimage
```

The recovery image is written under `out/target/product/dodge/`.

## Manifest layout

- `default.xml` pins the Android platform source set.
- `twrp-default.xml` overlays the recovery build system and dependencies.
- `fox.xml` contains the AERA recovery stack and Dodge device tree.
- `remove-minimal.xml` removes projects that are unnecessary for recovery.

## Contribution policy

Preserve original authorship when importing or adapting changes. Keep device-
specific work in its device tree and reusable recovery behavior in the
appropriate shared AERA project.
