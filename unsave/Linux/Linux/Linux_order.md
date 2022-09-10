# Linux 命令

> **目录**

## 关机/重启/注销

> ```bash
> shutdown(选项)(参数)
> ```

| 命令                    | 作用                   |
| :---------------------- | :--------------------- |
| shutdown -h now         | 即刻关机               |
| shutdown -h 10          | 10分钟后自动关机       |
| shutdown -h 11:00       | 11:00自动关机          |
| shutdown -c             | 取消指定时间关机       |
| shutdown -r now         | 即刻重启               |
| shutdown -r 10          | 10分钟后重启           |
| shutdown -r 11:00       | 11:00 自动重启         |
| shutdown +10 "SHUTDOWN" | 10分钟后关机并发出警告 |
| reboot                  | 重启                   |
| teinit 0                | 关机                   |
| poweroff                | 断电且关机             |
| halt                    | 停机不断电             |
| sync                    | 数据同步到磁盘         |
| logout                  | 退出登陆shell          |



> ```
> halt[选项]
> ```
>
> ```shell
> -d：不要在wtmp中记录；
> -f：不论目前的runlevel为何，不调用shutdown即强制关闭系统；
> -i：在halt之前，关闭全部的网络界面；
> -n：halt前，不用先执行sync；
> -p：halt之后，执行poweroff；
> -w：仅在wtmp中记录，而不实际结束系统。
> ```

> ```
> reboot[选项]
> ```
>
> ```shell
> -d：重新开机时不把数据写入记录文件/var/tmp/wtmp。本参数具有“-n”参数效果；
> -f：强制重新开机，不调用shutdown指令的功能；
> -i：在重开机之前，先关闭所有网络界面；
> -n：重开机之前不检查是否有未结束的程序；
> -w：仅做测试，并不真正将系统重新开机，只会把重开机的数据写入/var/log目录下的wtmp记录文件。
> ```

> ```
> poweroff[选项]
> ```
>
> ```shell
> -n 关闭之前不同步
> -p 当被称为halt时关闭电源
> -v 增加输出，包括消息
> -q 降低输出错误唯一的消息
> -w 并不实际关闭系统，只是写入/var/log/wtmp文件中
> -f 强制关机，不调用shutdown
> ```



## 系统信息

