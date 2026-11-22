# j4primelte-postmarketos
THIS IS NOT BUILT VERSION OF POSTMARKETOS DO NOT DOWNLOAD ANYTHING FROM HERE 

## Rootfs build (GitHub Actions + pmbootstrap)

The postmarketOS rootfs for j4primelte is built by the
`Build j4primelte rootfs (pmbootstrap)` workflow
(`.github/workflows/build-rootfs.yml`). Dispatch it from the Actions tab with
`workflow_dispatch`.

- Output: `rootfs-j4primelte.img.xz` — a flat ext4 root filesystem (no
  partition table, not sparse), with the UUID recorded in `uuid.txt` and the
  workflow summary.
- The rootfs is for **your** separately-built boot image (e.g. the medusa64
  aarch64 boot image with the "Samsung J4PRIMELTE SEA OPEN PROJECT Rev06"
  DTB). The kernel in the rootfs (`linux-lts`) is only there so mkinitfs
  succeeds; do not flash it.
- Your boot image's `pmos_root_uuid=` cmdline must match the UUID in
  `uuid.txt` (workflow input `root_uuid`, default `3725f30e-2934-4a82-a4c2-f32211aeee4c`).
- The device/firmware pmaports live under `overlay/`. The device package is
  category `downstream` (ext4 `metadata_csum` is disabled for 3.18-kernel
  safety) and intentionally does not build the old 5.8 kernel.
- `artifacts/` (extracted boot image contents) is local-only and git-ignored.
