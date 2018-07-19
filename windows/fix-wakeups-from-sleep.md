# Fix Computer Waking up from Sleep

`phobos` (Windows 10) was waking up from sleep, which seemed to be caused by
Spotify running somewhere else (e.g. on the phone). Debugging this for quite
some time showed that it was the network controller that was causing the wakeup.

What fixed the problem was:

- start admin PowerShell
- `powercfg /devicequery wake_armed` → listed USB keyboard, mouse, and "Realtek
  PCIe GBE Family Controller"
- `powercfg /devicedisablewake "Realtek PCIe GBE Family Controller"`
- `powercfg /devicequery wake_armed` → only USB keyboard and mouse left

Interestingly, what *did not* help:

- Changing any BIOS settings (all wakeup entries are disabled there), Windows
  seems to be able to overrule or ignore those.
- Fiddling around in any of the power settings ("Settings" → "Power & Sleep" →
  "Additional…" → "Change plan…" → "… advanced…"); almost all settings in there
  control when the computer should go to some sleep state, and what gets
  disabled and whatnot. However, there is one promising entry "Allow wake
  times"; turning this off didn't fix the problem, though.
