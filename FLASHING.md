# Flashing the BBQ10 Pro

## What the owner does
1. **Double-tap the reset button** in the hole on the bottom of the device
   within about 500 ms. A single press just reboots; the double-tap is what
   enters DFU/bootloader mode.
2. **Plug the keyboard into the Mac via USB.** (Order doesn't matter — you can
   plug in first, then double-tap.)
3. **Click "Allow"** if macOS shows a "Allow accessory to connect" prompt.

That's it. The agent handles the rest.

## What the agent does (automated flash)

When the owner says they're in bootloader mode and plugged in, the agent runs:

```bash
# 1. Verify the bootloader is mounted (drive is named "NICENANO" — same as
#    nice!nano's bootloader, since the BBQ10 Pro reuses it):
ls /Volumes/NICENANO/

# 2. (optional) Confirm it's the right device:
cat /Volumes/NICENANO/INFO_UF2.TXT
#   → should mention "nRF52840-nicenano" and a UF2 Bootloader version

# 3. Copy the .uf2 onto the drive (use -X on macOS to skip xattrs):
cp -X /Users/julyan/Workspace/zitaotech_q10/built-firmware/run-<RUN_ID>/firmware/zitaotech_q10-zmk.uf2 /Volumes/NICENANO/

# 4. The drive auto-ejects within ~1 second. Keyboard reboots into the new
#    firmware. Confirm by:
ls /Volumes/    # NICENANO is gone
ioreg -p IOUSB -l | grep -i ZitaoTech    # ZitaoTech_q10 shows up
```

## Gotchas

- **Without `cp -X`**, `cp` returns exit code 1 with the message
  "could not copy extended attributes ... Device not configured." This is
  **not a failure** — the file body was written, the device auto-ejected
  itself once the UF2 was fully received, and the post-copy xattr step then
  failed because the device was gone. The flash succeeded. Use `cp -X` to
  avoid the noise.

- **Single-tap reset ≠ bootloader.** A single press just reboots the device
  into the existing firmware. Must be a double-tap within ~500 ms.

- **Alternative bootloader entry** (works on whatever firmware is currently
  installed, no reset hole needed): from the current keymap, switch to the
  UPPER layer (rightmost ⇧-icon thumb key on the upstream config) and tap
  the `$` key — the upstream UPPER `$` is a tap-dance with `&bootloader` as
  the first action. This binding may move or change as the owner edits the
  keymap.

- **To flash the settings-reset companion** (`settings_reset-zitaotech_q10-zmk.uf2`),
  use the same flow. That firmware clears stored Bluetooth pairings and ZMK
  settings without changing the keymap; useful when BT gets stuck.

## When `/Volumes/NICENANO/` is not mounted

Run `ioreg -p IOUSB -l 2>&1 | grep -iE "USB Product Name" | grep -vi apple`
to see what's actually attached:
- If you see `"ZitaoTech_q10"` → the keyboard is plugged in but running the
  normal firmware, not bootloader. Ask the owner to double-tap reset.
- If you see nothing → keyboard isn't connected, or the cable is charge-only.
  Ask the owner to verify the cable and connection.
