# Backlight Error - KDE Plasma (Some Asus Laptops)

We recommend you to do it step by step. For example, don't try third way for solving this issue at the first time. It's not bad, but do it step by step :)

If you get an **Failed to start Load/Save Screen Backlight Brightness** error in GNU/Linux, type following command in `/etc/default/grub`:

<!-- Failed to start Load/Save Screen Backlight Brightness -- comment for you guys and girls -->
`GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi_backlight=vendor"`

After write and save this action, make sure you are updating your grub: `sudo update-grub`

If you still get an error (like asus backlight service and etc.), type this command: `sudo systemctl disable systemd-backlight@.service`

The last and best way for get rid of that problem is:

- `systemctl disable acpi_video0.service acpi_video1.service`
- `systemctl mask acpi_video0.service acpi_video1.service`

Finally, reboot your computer by `reboot` or `init 6` or `shutdown /r` command. Have a nice day :)
