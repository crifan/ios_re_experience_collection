# 正则搜索

## lldb用正则查找函数时记得要转义特殊字符

* 现象

此处lldb去搜，本身存在的函数名=符号名：

`+[FIRAnalytics sharedInstance]_51_block`

但是却搜不到：
```bash
(lldb) im loo -rn "+[FIRAnalytics sharedInstance]_51_block"
(lldb)
```

* 原因

此处用`r`=`regex`=`正则`的方式去搜索，所以字符串中：

* `加号`=`+`
* `中括号`= `[]`

都是：正则中特殊的字符

所以此处把正则字符串当做普通字符去搜索，导致含义不对，所以搜不到

* 解决办法

如果要使用普通字符，则应该加上反斜杠转义
```bash
im loo -rn "\+\[FIRAnalytics sharedInstance\]_51_block"
```

即可搜到：

```bash
(lldb) im loo -rn "\+\[FIRAnalytics sharedInstance\]_51_block"
1 match found in /private/var/containers/Bundle/Application/4BD12EFB-0A75-49DC-8059-EBCDCF21522D/WhatsApp.app/Frameworks/SharedModules.framework/SharedModules:
        Address: SharedModules[0x0000000000b8f7c8] (SharedModules.__TEXT.__text + 12096916)
        Summary: SharedModules`+[FIRAnalytics sharedInstance]_51_block
```
