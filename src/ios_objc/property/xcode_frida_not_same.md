# Xcode和Frida属性值不一致

* iOS逆向调试时，遇到的一些特殊情况
  * NSXPCConnection的属性
    * 部分属性值：Xcode中有，但Frida中没有
      * processName
      * processBundleIdentifier
    * 其他属性，倒是都正常：Xcode和Frida中都有
      * endpoint
      * processIdentifier
      * exportedInterface
      * exportedObject
      * remoteObjectInterface
      * remoteObjectProxy
      * userInfo
      * auditSessionIdentifier
      * effectiveUserIdentifier
      * effectiveGroupIdentifier

详见：

* 【已解决】iOS逆向Apple账号：用frida打印com.apple.ak.auth.xpc的NSXPCConnection的其他属性值
* 【未解决】iOS逆向：通过查看NSXPCConnection的属性值搞清楚目标处理的类是哪个
