# 打印类的描述详情信息

* Xcode调试期间：打印ObjC类的描述详情信息
  * 已知的传统手段：`Xcode`/`lldb`中，`po`加上对应命令`_ivarDescription`、`_propertyDescription`、`_methodDescription`、`shortMethodDescription`
    ```bash
    po [xxx _ivarDescription]
    ```
    ```bash
    po [xxx _propertyDescription]
    ```
    ```bash
    po [xxx _methodDescription]
    ```
    ```bash
    po [xxx _shortMethodDescription]
    ```
  * 新的手段：tweak插件的hook代码中，调用对应命令 `_ivarDescription`、`_propertyDescription`、`_methodDescription`、`shortMethodDescription`
    * 【已解决】iOS逆向Apple账号：通过插件hook去打印AADeviceInfo的类的相关信息
