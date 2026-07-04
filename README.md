# wwn-hyprland

Wawona's port of **Hyprland** — a dynamic-tiling wlroots Wayland compositor — to
run nested under Wawona on the Apple ecosystem and Android, App Store compliant.

> **Status: SKELETON.** flake + `registryFragment` skeleton + port plan only.
> Build stubs fail intentionally; full port is downstream.

## Delivery model

Hyprland (wlroots/aquamarine) runs **nested** as a Wawona client. Its
DRM/libinput backends are unused on Apple/Android; the nested Wayland backend is
used instead. Hyprland-specific protocols are mirrored where Wawona supports
them (see Wawona `docs/2026-wlroots-compat.md`).

## Port plan

1. Toolchain via `wwn-toolchain`.
2. Compliance: no JIT, no plugin `dlopen` of arbitrary code (Hyprland plugins
   must be disabled or statically vetted on Apple), sandbox-safe runtime dirs.
3. aquamarine/wlroots: nested Wayland backend only.
4. Replace `dependencies/hyprland/stub.nix` per platform; expose
   `hyprland-{ios,macos,android}`; register in Wawona.
5. `wwn-apt` lists `hyprland` `status: planned` → flip to `approved` post-review.

Convention: [wwn-* porting convention](https://github.com/Wawona/Wawona/blob/main/docs/2026-wwn-porting-convention.md).
