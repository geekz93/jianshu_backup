1. 切换到root用户，为 /etc/sudoers增加w权限： chmod u+w /etc/sudoers
2. 修改文件 vi /etc/sudoers 找到 root  ALL=(ALL)   ALL 换行添加 zooo  ALL=(ALL)   ALL
3. 如果不需要密码则添加 zooo  ALL=(ALL)   NOPASSWD: ALL
4. 修改完成后需要恢复原来的权限才能生效
