# iPhone中常用目录

iOS逆向期间，常常会涉及到很多目录，且其中有些是有（软链接等）关系的。整理如下：

* `/etc/` == `/private/etc/`
* `/var/` == `/private/var/`
  * `/User/` == `/var/mobile/` == `/private/var/mobile/`
  * `/tmp/` == `/private/var/tmp/`

->

举例：

* Bundle目录 入口=根目录
  * `/private/var/containers/Bundle/Application/`
    * ==
      * `/var/containers/Bundle/Application/`

## 附录

根目录下文件目录和内容：

```bash
iPhone8-143:/ root# pwd
/
iPhone8-143:/ root# ls -lh
total 1.5K
drwxrwxr-x 107 root admin 3.4K Dec 25 11:14 Applications/
drwxr-xr-x   7 root wheel  306 Dec  4  2020 Developer/
drwxr-xr-x  25 root wheel  800 Dec 13 10:48 Library/
drwxr-xr-x   4 root wheel  128 Jan  8  2021 System/
lrwxr-xr-x   1 root wheel   11 Dec 13 11:07 User -> /var/mobile/
drwxr-xr-x  61 root wheel 2.0K Dec 13 10:48 bin/
drwxr-xr-x   2 root wheel   64 Oct 28  2006 boot/
drwxrwxr-t   2 root admin   64 Jun 28  2018 cores/
dr-xr-xr-x   4 root wheel 1.4K Dec 13 11:01 dev/
lrwxr-xr-x   1 root wheel   11 Jun 28  2018 etc -> private/etc/
drwxr-xr-x   2 root wheel   64 Oct 28  2006 lib/
drwxr-xr-x   2 root wheel   64 Oct 28  2006 mnt/
drwxr-xr-x   7 root wheel  224 Jan  8  2021 private/
drwxr-xr-x  40 root wheel 1.3K Dec 13 10:48 sbin/
lrwxr-xr-x   1 root wheel   15 Jun 28  2018 tmp -> private/var/tmp/
drwxr-xr-x  12 root wheel  384 Dec 13 10:48 usr/
lrwxr-xr-x   1 root admin   11 Jun 28  2018 var -> private/var/
iPhone8-143:/ root#
```
