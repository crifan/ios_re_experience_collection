# 属性值

## ObjC的类，没有函数，但对应父类有该函数

调试到：

```asm
0x107b8c808 <+24>:  bl   0x107c42940  ; objc_msgSend$executeDatabaseFetchRequest:context:
```

看到参数是：

```bash
(lldb) reg r x0 x1 x2 x3
      x0 = 0x000000010f541210
...
(lldb) po $x0
<WASignalKeyStore: 0x10f541210>
```

以为是：

* `-[WASignalKeyStore executeDatabaseFetchRequest:context:]`

但是后来发现：
* `-[WASignalKeyStore executeDatabaseFetchRequest:context:]`
  * 断点：加不上，加断点失败

转而发现：

`WASignalKeyStore`类，没有这个函数：`executeDatabaseFetchRequest:context:`

后来才发现：是继承的子类

继承关系是：

* WASignalKeyStore
  * WAAutoMigratingStorage
    * WACheckpointingStorage
      * WAStorage

而WAStorage：才有函数

* `- (id)executeDatabaseFetchRequest:(id)arg1 context:(id)arg2 error:(id *)arg3;`

所以是：

* `-[WAStorage executeDatabaseFetchRequest:context:]`
