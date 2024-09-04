# 崩溃日志解析工具

* iOS（和Mac）崩溃日志解析工具
  * 通用？
    * `atos` = address to symbol
  * iOS 15之前：
    * `symbolicatecrash`
  * iOS 15之后：
    * `CrashSymbolicator.py`
      * 位置：（Xcode中？） `Contents/SharedFrameworks/CoreSymbolicationDT.framework/Resources/`
        * `/Applications/Xcode.app/Contents/SharedFrameworks/CoreSymbolicationDT.framework/Versions/A/Resources`
      * 用法：
        ```bash
        python3 CrashSymbolicator.py -d /dSYMs -o /xxxSymbo.crash -p /xxxCrash.ips
        ```
