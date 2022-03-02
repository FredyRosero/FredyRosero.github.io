
## Prerequisitos Windows

npcap

    libpcap
    libusb-1.0-0 (required by the HID module)
    libnetfilter-queue (on Linux only, required by the packet.proxy module)

Bettercap
```bash
net-show
bettercap -eval "caplets.update; ui.update; q"
bettercap -caplet http-ui
```

Las contraseñas las encontramos en `C:\ProgramData\bettercap\caplets\http-ui.cap` por defecto es `user` y `pass`