**问题**：更换密码后打开360浏览器lsass进程在很长一段时间占用过高cpu

**解决**：`RD /s /q "%USERPROFILE%\AppData\Roaming\Microsoft\Protect"`
