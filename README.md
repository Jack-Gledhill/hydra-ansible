# Hydra Ansible

## Reinstalling the Nodes

When reinstalling Raspberry Pi OS onto the nodes, it's important to note that additional setup is needed.
After flashing the OS onto the SSD drives, you should modify the `config.txt` file in the `bootfs` partition and add the following line:
```
usb_max_current_enable=1
```

When powered by a 3A supply (e.g. over PoE), the Raspberry Pi 5 limits the current in USB ports to 600mA (aggregate).
This is not sufficient to power the SSD drives that each Pi boots from, so the OS refuses to boot.
However, by adding the above line to the boot config, the Pi will allow the USB ports to draw the full 1.6A that would be provided on a 5A supply.

This is a little risky, as it could starve the SoC of current if the USB ports draw too much.
To mitigate this, no other USB or unpowered devices should be connected to the Pi, and the CPU should not be overclocked. 