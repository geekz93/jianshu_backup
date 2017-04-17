* **问题**
装了双系统后进入引导选择界面后，无法使用键盘，刚开机的时候键盘有用

* **分析**
刚开机能够使用键盘，说明驱动安装正常，键盘没问题

* **原因**
bios将键盘鼠标设备禁用了

* **BIOS设置**
启用bios的usb设备支持即可
bios -> Integrated peripherals -> onboard device -> usb keyboard support -> enable
