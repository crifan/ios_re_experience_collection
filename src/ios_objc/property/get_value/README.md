# 获取变量值

* 获取变量值
  * 通用的：`valueForKey`
    * `po [someObj valueForKey: @"keyName"]`
      * 举例
        ```bash
        po [$x0 valueForKey: @"v_Data"]
        ```
        ```bash
        (lldb) po [0x286d8a070 valueForKey: @"_phoneNumber"]
        <WAPhoneNumber: 0x28245e3c0> ({ 1 8784650468 })
        ```
        ```bash
        (lldb) po [0x112994040 valueForKey: @"_registrationIdData"]
        <45534916>
        ```
        ```bash
        (lldb) po [0x282170b80 valueForKey: @"_baseURLString"]
        https://v.whatsapp.net/v2/exist
        ```
  * 单个类自己的函数=`Selector`
    * `dict`
      * objectForKey
        ```bash
        po [$x0 objectForKey: @"v_Data"]
        ```
      * objectForKeyedSubscript
        ```bash
        po [$x0 objectForKeyedSubscript: @"v_Data"]
        ```
