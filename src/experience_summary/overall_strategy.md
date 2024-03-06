# iOS逆向的总体对策

TODO：

* 【整理】iOS逆向心得：不同app的逆向破解出的难度不同
* 【整理】iOS逆向破解越狱开发：相关工具

---

## iOS安全对应的逆向破解对策

针对[iOS安全](https://book.crifan.org/books/ios_security_protect/website/)的防护手段，目前能想到的，iOS逆向破解的办法：

* iOS的代码混淆
  * 被反编译后，也只能看到 乱码的函数
    * 部分防止被破解，被猜测到核心逻辑
* iOS的加壳？
  * 没法加壳
    * 但是也可以去研究看看，是否有机会
* iOS代码运行期间，动态下载要运行的核心代码（二进制格式？）
  * 增加核心逻辑的安全性
    * 好像涉及到虚拟机之类的
      * 注：对应的iOS逆向，则是：unicorn等 模拟器 虚拟机，模拟运行对应的指令
* iOS的抓包方面的：加https证书验证？ ssl pinning？
  * 甚至（参考抖音的做法）去本地ssl证书验证
    * 只有破解hook后，才能Charles抓包看到https明文
    * 后记：[[原创]绕过抖音SSL Pinning-iOS安全-看雪论坛-安全社区|安全招聘|bbs.pediy.com](https://bbs.pediy.com/thread-270700.htm)
      * > 1.加入自己的证书2.干掉所有的证书3.不让他验证证书。很显然，你用的是第二种

