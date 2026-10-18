# Kokuban CI: Pixel 4 / Pixel 4 XL

- CI repository: https://github.com/YuzakiKokuban/Kokuban_Kernel_CI_Center
- Project: `floral_sm8150`; source branch / variant: `bakasu`.
- CI kernel release: `4.14.357-Kokuban-Kaltsit-BakaSU-g<kernel-commit>` (CI uses its 12-character kernel commit ID).
- Configuration: `floral_defconfig`, no LTO/CFI, no SUSFS.
- BakaSU: fetched from `Baka-SU/BakaSU` `main` on every CI build. There is no
  BakaSU submodule or commit pin in this kernel. The build log records the version.
- Hybrid Mount: built-in VFS provider, `CONFIG_HYBRIDMOUNT=y`; provenance is in
  `fs/hybridmount/IMPORT` and `fs/hybridmount/PROVENANCE`.
- Output: AnyKernel3 ZIP containing `Image.lz4`, restricted to `flame` / `coral`.
  The installer preserves the existing boot ramdisk, DTB and DTBO.

Use CI Center's **Build Kernel** workflow with `floral_sm8150` and `bakasu`.
SUSFS is disabled by the project policy even if a global setting requests it.
Hybrid Mount's Android metamodule is still installed separately through BakaSU.
Boot, root authorization, Wi-Fi and VFS operation require device verification.

For a local build, populate the ignored `KernelSU/` checkout before running make:

```sh
curl -fsSL https://raw.githubusercontent.com/Baka-SU/BakaSU/main/kernel/setup.sh | bash -s main
```

CI Center uses LLVM 12.0.1 and GNU AArch64 binutils; refer to its project config
for the toolchain URL and checksum. Do not select tracepoint hooks on this 4.14 tree.
