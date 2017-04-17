## crontab实现定时任务
crontab -e 编辑文件，保存退出后系统就会执行定时任务
- 时程表格式
f1 f2 f3 f4 f5 program
其中 f1 是表示分钟，f2 表示小时，f3 表示一个月份中的第几日，f4 表示月份，f5 表示一个星期中的第几天。program 表示要执行的程式
- 符号
`*`: 每个时间单位： 每分，每小时
`a-b`: 从a-b时间段内每个单位
`*/n`: 每n个时间单位
`a,b,c`: 第a,b,c个时间单位

### 例子
- 每月每天每小时的第 0 分钟执行一次 /bin/ls :
`0 * * * * /bin/ls`
- 在 12 月内, 每天的早上 6 点到 12 点中，每隔 20 分钟执行一次 /usr/bin/backup :
`*/20 6-12 * 12 * /usr/bin/backup`
- 周一到周五每天下午 5:00 寄一封信给 alexmailname :
`0 17 * * 1-5 mail -s "hi" alex_mail_name < /tmp/maildata`
- 每月每天的午夜 0 点 20 分, 2 点 20 分, 4 点 20 分....执行 echo "haha"
`20 0-23/2 * * * echo "haha"`
- 晚上11点到早上8点之间每两个小时，早上8点
`0 23-7/2，8 * * * date`

## 查看crontab log
1. /etc/rsyslog.d/50-default.conf 中去除 cron.* 的注释
2. service rsyslog restart 
3. tail -f /var/log/cron.log 查看log 

脚本中如果权限不够，将不能执行任务：在zooo用户下执行`back.sh` 其中的shutdown命令由于权限不够不能执行。要保证他能够正常关机，使用`sudo crontab -e`在下面添加`back.sh`即可
