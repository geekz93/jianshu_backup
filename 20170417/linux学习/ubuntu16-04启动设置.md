## 双系统将windows启动放前面
- 在 /etc/grub.d/ 中将 30_os-prober 改名为 08_os-prober
- update-grub
原理：update-grub在 grub.d 中按照文件的序号来生成 grub.cfg 文件，os-prober文件的作用是寻找自身以外的启动引导，将它的序号改成比 10_linux 小就先找到了 windows 的启动引导

## ubuntu16.04启动进入命令行
- 注释掉 `GRUB_CMDLINE_LINUX_DEFAULT=”quiet” `
- 把GRUB_CMDLINE_LINUX=”" 改为 GRUB_CMDLINE_LINUX=”text”
- 去掉 #GRUB_TERMINAL=console 的注释，即 GRUB_TERMINAL=console
- `sudo update-grub`
- `sudo systemctl set-default multi-user.target`
- `sudo reboot`
