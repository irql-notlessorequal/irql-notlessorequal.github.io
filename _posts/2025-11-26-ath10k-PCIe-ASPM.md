---
layout: post
title: Fixing AER errors with ath10k Wireless cards
---

Just a small PSA for those on older Intel chipsets that absolutely hate ASPM, disabling PCIe sub-states tends
to fix this problem.

You can fix this by creating a udev rule that disables them on boot.

Here's an example one for my QCA6174 wireless card.

```
SUBSYSTEM=="pci", ATTR{vendor}=="0x168c", ATTR{device}=="0x003e", ATTR{link/l0s_aspm}="0", ATTR{link/l1_aspm}="0"
```

Put this into `/etc/udev/rules.d/` under any `.rules` named file and reboot.

This of course will come with a idle power draw penalty.