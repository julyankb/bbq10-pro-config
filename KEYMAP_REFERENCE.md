# BBQ10 Pro — Visual Key Reference

**Purpose:** Map every physical button on the BBQ10 Pro to its **position in
the keymap bindings array** (row & column), so the owner can describe a key
by what's printed on it and you immediately know which binding to edit.

**What this doc is:**
- ✅ A canonical translation from "the red circle key" / "the M key" / etc.
  to a stable `Row N, col M` coordinate in `config/zitaotech_q10.keymap`.
- ✅ A reference for the **physical layout** and the **printed labels**.

**What this doc is NOT:**
- ❌ A spec for what each key *should* do. The owner is actively customizing
  this keymap and will remap things freely — possibly to match the printed
  labels (e.g., making the "alt" key actually do Alt), possibly not.
- ❌ A reliable source for **current bindings**. The "Layer 0/1/2/3" columns
  in the tables below are a **snapshot of the initial state** after forking
  upstream and will drift as edits land.

**When planning a change, always read the current `config/zitaotech_q10.keymap`
file directly to see what a binding is right now — don't rely on this doc's
behavior columns.** The physical-position columns (Row N, col M) and the
printed-label columns are stable; the binding columns are not.

When the owner says "the red circle key" → check the **Function row** table
to get its position → then read the keymap file to see (and modify) what's
bound there in the relevant layer.

---

## Physical layout (top-down view)

The device has 42 keys total, arranged in 6 rows. Two additional trigger
buttons sit on the top edge of the device (not visible from above).

```
   [L-shoulder]                                                       [R-shoulder]    ← top edge of device
   [Red ⭕]   [Green △]   [Trackpad]    [Magenta ✕]   [Yellow ⬜]                       ← function row (5 keys)
   [ Q# ][ W1 ][ E2 ][ R3 ][ T( ][ Y) ][ U_ ][ I- ][ O+ ][ P@ ]                        ← alpha row 1 (10 keys)
   [ A* ][ S4 ][ D5 ][ F6 ][ G/ ][ H: ][ J; ][ K' ][ L" ][ ⌫  ]                        ← alpha row 2 (10 keys)
   [alt ][ Z7 ][ X8 ][ C9 ][ V? ][ B! ][ N, ][ M. ][ $🔊][ ⏎  ]                         ← alpha row 3 (10 keys)
            [ ⇧ ][ 0🎤][          SPACE          ][sym ][ ⇧  ]                           ← thumb row (5 keys)
```

The small symbol next to each big letter in the alpha rows is the **SYM-layer**
output (the secondary character printed on the key cap). The big letter is the
**DEFAULT-layer** output.

---

## Keymap structure refresher

Each layer in `config/zitaotech_q10.keymap` has a `bindings = <…>;` block. The
bindings are in this order (matching the physical layout above):

1. **Row 1** — 2 bindings: `L-shoulder, R-shoulder`
2. **Row 2** — 5 bindings: function row left-to-right
3. **Row 3** — 10 bindings: top alpha row (`Q W E R T Y U I O P` positions)
4. **Row 4** — 10 bindings: middle alpha row (`A S D F G H J K L ⌫` positions)
5. **Row 5** — 10 bindings: bottom alpha row (`alt Z X C V B N M $ ⏎` positions)
6. **Row 6** — 5 bindings: thumb row left-to-right

**Important:** behaviors that take parameters (like `&mt LSHFT A` or
`&sk_kp LCTRL LCTRL`) count as **one binding**, even though they appear as
multiple whitespace-separated tokens.

---

## Reference tables

### Top-edge shoulder triggers (row 1)

| You can say                          | Position     | Layer 0 (DEFAULT) | Layer 1 (SYM)   | Layer 2 (UPPER) | Layer 3 (MEDIA) |
|--------------------------------------|--------------|-------------------|-----------------|-----------------|-----------------|
| "L-shoulder", "left trigger"         | Row 1, col 1 | Mouse L-click     | Volume Up       | Scroll Up       | none            |
| "R-shoulder", "right trigger"        | Row 1, col 2 | Mouse R-click     | Volume Down     | Scroll Down     | none            |

### Function row (row 2)

| You can say                                          | Position     | Layer 0 (DEFAULT)     | Layer 1 (SYM)    | Layer 2 (UPPER)               | Layer 3 (MEDIA) |
|------------------------------------------------------|--------------|------------------------|------------------|--------------------------------|-----------------|
| "red key", "red circle", "⭕", "call key"            | Row 2, col 1 | CapsLock              | PrintScreen      | BT Select 0                    | none            |
| "green key", "green triangle", "△", "BB key"        | Row 2, col 2 | Cmd / GUI / Windows   | Search           | BT Select 1                    | none            |
| "trackpad", "center button", "trackpad-click"        | Row 2, col 3 | Mouse L-click         | Mouse L-click    | Tap-dance: L-click / clear-BT  | none            |
| "magenta key", "pink X", "✕", "back key"             | Row 2, col 4 | Tap=ESC, Hold=Back    | F5               | BT Select 2                    | none            |
| "yellow key", "yellow square", "⬜", "end-call key"  | Row 2, col 5 | Tab                   | F12              | BT Select 3                    | none            |

### Alpha row 1 (row 3) — the Q-row

Reference these keys by their big letter (e.g., "the Q key", "the T key") or
by their SYM symbol (e.g., "the # key", "the @ key"). Both refer to the same
physical key.

| Letter | SYM label | Position      | Layer 0 (DEFAULT) | Layer 1 (SYM)        | Layer 2 (UPPER) |
|--------|-----------|---------------|-------------------|----------------------|-----------------|
| Q      | #         | Row 3, col 1  | Q                 | #                    | none            |
| W      | 1         | Row 3, col 2  | W                 | 1                    | Up arrow        |
| E      | 2         | Row 3, col 3  | E                 | 2                    | none            |
| R      | 3         | Row 3, col 4  | R                 | 3                    | Sys-reset       |
| T      | (         | Row 3, col 5  | T                 | Tap=`[` Hold=`(`     | Ext-power tog   |
| Y      | )         | Row 3, col 6  | Y                 | Tap=`]` Hold=`)`     | none            |
| U      | _         | Row 3, col 7  | U                 | `_`                  | `<`             |
| I      | -         | Row 3, col 8  | I                 | `-`                  | `>`             |
| O      | +         | Row 3, col 9  | O                 | `+`                  | `\|`            |
| P      | @         | Row 3, col 10 | P                 | `@`                  | `=`             |

### Alpha row 2 (row 4) — the A-row

| Letter | SYM label | Position      | Layer 0 (DEFAULT) | Layer 1 (SYM) | Layer 2 (UPPER) |
|--------|-----------|---------------|-------------------|---------------|-----------------|
| A      | *         | Row 4, col 1  | A                 | `*`           | Left arrow      |
| S      | 4         | Row 4, col 2  | S                 | 4             | Down arrow      |
| D      | 5         | Row 4, col 3  | D                 | 5             | Right arrow     |
| F      | 6         | Row 4, col 4  | F                 | 6             | none            |
| G      | /         | Row 4, col 5  | G                 | `/`           | `\`             |
| H      | :         | Row 4, col 6  | H                 | `:`           | `&`             |
| J      | ;         | Row 4, col 7  | J                 | `;`           | `{`             |
| K      | '         | Row 4, col 8  | K                 | `'`           | `}`             |
| L      | "         | Row 4, col 9  | L                 | `"`           | `^`             |
| ⌫ Bksp | DEL       | Row 4, col 10 | Backspace         | Delete        | Backspace       |

### Alpha row 3 (row 5) — the Z-row (includes alt, $, Enter)

| Letter / label | SYM label  | Position      | Layer 0 (DEFAULT)       | Layer 1 (SYM)              | Layer 2 (UPPER)        |
|----------------|------------|---------------|--------------------------|----------------------------|------------------------|
| **"alt"** (no SYM) | —      | Row 5, col 1  | **Sticky Shift** ⚠       | Shift (regular)            | Shift                  |
| Z              | 7          | Row 5, col 2  | Z                        | 7                          | none                   |
| X              | 8          | Row 5, col 3  | X                        | 8                          | none                   |
| C              | 9          | Row 5, col 4  | C                        | 9                          | RGB brightness down    |
| V              | ?          | Row 5, col 5  | V                        | `?`                        | Backlight down         |
| B              | !          | Row 5, col 6  | B                        | `!`                        | RGB toggle             |
| N              | ,          | Row 5, col 7  | N                        | `,`                        | Backlight up           |
| M              | .          | Row 5, col 8  | M                        | `.`                        | RGB brightness up      |
| **"$"** key    | 🔊 (mute)  | Row 5, col 9  | Tap=`$` Hold=`;`          | Tap=mute, Double-tap→MEDIA | Tap=bootloader, DT=output toggle |
| ⏎ Enter        | (no SYM)   | Row 5, col 10 | Enter                    | Enter                      | Enter                  |

### Thumb row (row 6)

| You can say                                    | Position     | Layer 0 (DEFAULT)         | Layer 1 (SYM) | Layer 2 (UPPER) |
|------------------------------------------------|--------------|----------------------------|---------------|-----------------|
| "left shift thumb", "⇧-shift icon thumb"       | Row 6, col 1 | **Ctrl** (sticky/held) ⚠   | Ctrl          | Ctrl            |
| "0 thumb", "0/mic", "🎤 thumb"                 | Row 6, col 2 | **Alt** ⚠                  | 0             | Alt             |
| "spacebar", "space"                            | Row 6, col 3 | Space                      | Space         | Space           |
| "sym key"                                      | Row 6, col 4 | → SYM layer                | → DEFAULT     | → SYM           |
| "right ↑ thumb", "up-arrow thumb", "right ⇧"   | Row 6, col 5 | → UPPER layer              | → UPPER       | → DEFAULT       |

---

## Positions where the printed label and the current binding diverge

The labels on the keycaps are inherited from the original BlackBerry Q10
hardware. In the **initial upstream keymap** that the owner forked, several
positions are bound to something other than what the label suggests. The
owner may keep these remaps, undo them, or change them further — these notes
exist only to flag positions where label-based descriptions are ambiguous.

Positions where label ≠ initial binding (as of the fork):

1. **"alt" key** (Row 5 col 1) — initially bound to sticky Shift, not Alt.
2. **Left ⇧-icon thumb key** (Row 6 col 1) — initially bound to Ctrl.
3. **"0/🎤" thumb key** (Row 6 col 2) — initially bound to Alt.
4. **Right ⇧-icon thumb key** (Row 6 col 5) — initially bound to UPPER-layer toggle.
5. **"$" key** (Row 5 col 9) — initially mod-tap (tap=$, hold=;).

**How to handle ambiguous references:** When the owner says "the alt key," it
could mean the *physical key labeled "alt"* OR *whichever key currently
produces Alt*. Default to the **physical-label interpretation** (since this
doc is built around physical identification) but confirm explicitly if the
binding for that position has been changed and the literal interpretation
would be surprising.

---

## How to use this when editing

When the owner says "change the [X] key to do Y":

1. **Find the physical key** in the tables above → get its `Row N, col M`
   position. This step uses the *physical-position* columns, which are stable.
2. **Read the current binding** for that position in
   `config/zitaotech_q10.keymap` — don't trust this doc's behavior columns
   (they may have drifted as the owner edited).
3. **Identify the layer** the change applies to (DEFAULT, SYM, UPPER, MEDIA,
   or all layers if it's a global remap). Ask the owner if unclear.
4. **Find that layer's `bindings = <…>;` block** in the keymap file and count
   to the right row and column. Remember multi-parameter behaviors like
   `&mt LSHFT A` or `&sk_kp LCTRL LCTRL` count as **one binding**.
5. **Replace just that binding** with the new behavior. Define any new
   custom behaviors in the `behaviors { … }` blocks at the top of the file.

If the description is ambiguous (e.g., "the alt key" could mean the
physically-labeled "alt" key or whichever key currently produces Alt),
default to the physical-label interpretation and confirm.

**Never assume the existing keymap is what the owner wants to preserve.**
The owner is iterating — every binding is fair game to change.
