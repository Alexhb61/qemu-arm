# An Approximation Emulator for Raspberry Pi

| Docker Image   | Description                                                                  |
|----------------|------------------------------------------------------------------------------|
| [ljishen/qemu-cortex-a15](https://github.com/ljishen/qemu-arm/tree/master/qemu-cortex-a15) | Emulator for `Raspberry Pi 2` |
| [alexhb61/qemu-cortex-a53](https://github.com/alexhb61/qemu-arm/tree/master/qemu-cortex-a53) | Emulator for `Raspberry Pi 3` |

# Notes
The emulator for `Raspberry Pi 3` waits until you load a `Rasbian.img` into `/var/tmp/img/` then starts the emulator.
It stops and saves the emulator when you make any file named `stop` inside `/var/tmp/img/`.
