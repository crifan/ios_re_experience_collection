# 从崩溃信息找崩溃所在位置

从XCode崩溃的地址寻找所属二进制的代码段和函数位置

此处XCode调试抖音ipa崩溃时：

## 获取崩溃时的函数地址

### 方式1：通过XCode自动解析iPhone中的崩溃日志

细节：抖音ipa运行崩溃时，从iPhone中得到的ips崩溃日志 或 XCode-》Window-》Device and Simulator-》Device Log中，找到的崩溃时的函数调用堆栈

### 方式2：通过bt

```bash
(lldb) bt
* thread #9, queue = 'NSOperationQueue 0x119653070 (QOS: USER_INTERACTIVE)', stop reason = signal SIGABRT
...
    frame #11: 0x000000010b07a1dc AwemeCore`___lldb_unnamed_symbol2502$$AwemeCore + 60
```

-》得到的地址：

`0x000000010b07a1dc`

## 从地址中反推寻找对应所属二进制和代码的位置

### 方式1：借用image lookup自动计算

```bash
image lookup -a 地址
```

举例：

```bash
(lldb) image lookup -a 0x000000010b41a1dc

      Address: AwemeCore[0x00000000059961dc] (AwemeCore.__BD_TEXT.__text + 467420)
      Summary: AwemeCore`___lldb_unnamed_symbol2502$$AwemeCore + 60
```

-》所属代码是：

* 所属二级制文件：`AwemeCore`
* 区域：`Text段`
* 函数起始地址：`0x00000000059961dc`
  * ？ 函数内偏移地址：`467420` = `0x721DC`

详见：

* 【已解决】lldb命令使用心得：image lookup
* 官网资料：
  * [Symbolication — The LLDB Debugger (llvm.org)](https://lldb.llvm.org/use/symbolication.html)

### 方式2：自己手动计算

```bash
(lldb) bt
...
    frame #11: 0x000000010b07a1dc AwemeCore`___lldb_unnamed_symbol2502$$AwemeCore + 60
```

思路：

* 用`image list -o -f`得到二进制起始地址=`ALSR`
* 再去手动计算： `函数偏移地址 = 当前地址 - 二进制ALSR`

举例：

```bash
(lldb) image list -o -f
...
[  2] 0x00000001056e4000 /Users/crifan/Library/Developer/Xcode/DerivedData/Aweme-ejnpzdlejfueeaffwupnpxokcaoj/Build/Products/Debug-iphoneos/Aweme.app/Frameworks/AwemeCore.framework/AwemeCore
```

-》得知：

AwemeCore的ALSR=起始地址=`0x00000001056e4000`

->

`0x000000010b07a1dc - 0x00000001056e4000` = `0x59961DC`
