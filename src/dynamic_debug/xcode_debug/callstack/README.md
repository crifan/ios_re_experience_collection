# 函数调用堆栈

* 查看函数调用堆栈
  * 已知的传统手段：Xcode/lldb中，用命令：bt
  * 新的手段：tweak插件的hook代码中，调用：[NSThread callStackSymbols]
    * 【已解决】iOS逆向：hook代码中通过函数打印处函数调用堆栈
