# 🎓 RHEL 10: RHCSA Lab

I am setting up a dedicated Red Hat Enterprise Linux 10 VM to study for my RHCSA (Red Hat Certified System Administrator) certification.

## ⚙️ Installation Challenges

- **CPU Architecture**: RHEL10 requires a minimum of x86-64-v3.
- **Display Issues**: The graphical installer failed to load, regardless of the display adapter used (VirtIO GPU or VGA).

## 🛠️ Text-Mode Workaround

To bypass the graphical installer failures, I had to force the installation to run in text-only mode.

**Boot Parameters:**

```bash
inst.text console=tty0
```

**Steps to Apply:**

1. Start the VM and wait for the GRUB menu.
2. Highlight **"Install Red Hat Enterprise Linux"**.
3. Press `e` to edit the boot parameters.
4. Find the line starting with `linux` or `linuxefi`.
5. Append the code above to the end of that line.
6. Press `Ctrl+X` or `F10` to boot.

## 📝 Post-Install Notes

- **Subscription**: The text-based installer does not allow for Red Hat subscription registration. This must be configured manually via the command line after the system is installed.