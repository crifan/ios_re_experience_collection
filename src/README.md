# iOS逆向：心得集锦

* 最新版本：`v1.1.0`
* 更新时间：`20241026`

## 简介

把iOS逆向中的，各种不适合、不方便、不应该放到某个其他独立子教程中的心得，都整理过来，放到此处iOS逆向心得集锦中，方便参考；包括心得概述；iPhone的初始化开发环境和常用目录；app的plist文件、相关文件目录和数据，包括Bundle、Data、Shared AppGroup；二进制文件路径，app的卸载的残留数据；Keychain数据库及字段含义；以及ObjC的运行时，包括objc_msgSend、objc_alloc；Class类的打印类的描述详情信息、成员属性包括公开和私有的和扩展属性；以及类和实例的对比；以及属性值，如何获取变量的值，包括dict字典；计算类的属性值；Xcode和Frida属性值不一样；以及动态调试的调试代码逻辑，寻找函数触发时机；alloc和init和new；重装和spawn方式；寻找变量改动时机；wivar；改变运行逻辑的修改寄存器值、hook函数返回值；Xcode调试包括Attach调试、函数调用堆栈，函数名不一致；查看当前所有变量值；Fetching Variables on iPhone；汇编代码窗口保持打开状态；2个调试目标arm64和arm64e；xm文件无法定位到源代码位置；实时调试hook代码；和LLDB的正则搜索；iOSOpenDev；Mach-O的image base基地址；log日志的超过1K的打印；头文件的试试新旧不同版本；抓包的request和response；tweak插件；crash崩溃的崩溃日志解析工具、从崩溃信息找崩溃所在位置；和通用的：从汇编反推代码逻辑、必要时hook多个目标、特殊的参数传递、hook代码没生效、hook导致很慢和卡死；最后有附录相关资料。

## 源码+浏览+下载

本书的各种源码、在线浏览地址、多种格式文件下载如下：

### HonKit源码

* [crifan/ios_re_experience_collection: iOS逆向：心得集锦](https://github.com/crifan/ios_re_experience_collection)

#### 如何使用此HonKit源码去生成发布为电子书

详见：[crifan/honkit_template: demo how to use crifan honkit template and demo](https://github.com/crifan/honkit_template)

### 在线浏览

* [iOS逆向：心得集锦 book.crifan.org](https://book.crifan.org/books/ios_re_experience_collection/website/)
* [iOS逆向：心得集锦 crifan.github.io](https://crifan.github.io/ios_re_experience_collection/website/)

### 离线下载阅读

* [iOS逆向：心得集锦 PDF](https://book.crifan.org/books/ios_re_experience_collection/pdf/ios_re_experience_collection.pdf)
* [iOS逆向：心得集锦 ePub](https://book.crifan.org/books/ios_re_experience_collection/epub/ios_re_experience_collection.epub)
* [iOS逆向：心得集锦 Mobi](https://book.crifan.org/books/ios_re_experience_collection/mobi/ios_re_experience_collection.mobi)

## 版权和用途说明

此电子书教程的全部内容，如无特别说明，均为本人原创。其中部分内容参考自网络，均已备注了出处。如发现有侵权，请通过邮箱联系我 `admin 艾特 crifan.com`，我会尽快删除。谢谢合作。

各种技术类教程，仅作为学习和研究使用。请勿用于任何非法用途。如有非法用途，均与本人无关。

## 鸣谢

感谢我的老婆**陈雪**的包容理解和悉心照料，才使得我`crifan`有更多精力去专注技术专研和整理归纳出这些电子书和技术教程，特此鸣谢。

## 其他

### 作者的其他电子书

本人`crifan`还写了其他`150+`本电子书教程，感兴趣可移步至：

[crifan/crifan_ebook_readme: Crifan的电子书的使用说明](https://github.com/crifan/crifan_ebook_readme)

### 关于作者

关于作者更多介绍，详见：

[关于CrifanLi李茂 – 在路上](https://www.crifan.org/about/)
