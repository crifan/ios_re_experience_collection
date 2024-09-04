# dict字典

## lldb中获取ObjC中dict中key的值

此处lldb中，ObjC的（Subscript的）dict：

```bash
(lldb) po $x0
{
...
    "v_Data" = {length = 69, bytes = 0x0a2105d8 4217d833 e0d21288 0d7b833c ... a57f1bb8 1a416162 };
}
```

想要获取：`key=v_Data`的值

* 方式1：ObjC通用的`valueForKey`

```bash
(lldb) po [$x0 valueForKey: @"v_Data"]
<0a2105d8 4217d833 e0d21288 0d7b833c 34ae59c6 6dd91f37 c5e859dc 8338cb01 17067112 20d8eef6 4cc8de06 3a7cfb92 8f5af71d 8819ea0a cc4d00a4 04a57f1b b81a4161 62>
```

方式2：（subscript的）dict专门的：`objectForKeyedSubscript`

```bash
(lldb) po [$x0 objectForKeyedSubscript: @"v_Data"]
<0a2105d8 4217d833 e0d21288 0d7b833c 34ae59c6 6dd91f37 c5e859dc 8338cb01 17067112 20d8eef6 4cc8de06 3a7cfb92 8f5af71d 8819ea0a cc4d00a4 04a57f1b b81a4161 62>
```

详见：
[objectForKeyedSubscript: | Apple Developer Documentation](https://developer.apple.com/documentation/foundation/nsdictionary/1415430-objectforkeyedsubscript?language=objc)

方式3：dict通用的：`objectForKey`

```bash
(lldb) po [$x0 objectForKey: @"v_Data"]
<0a2105d8 4217d833 e0d21288 0d7b833c 34ae59c6 6dd91f37 c5e859dc 8338cb01 17067112 20d8eef6 4cc8de06 3a7cfb92 8f5af71d 8819ea0a cc4d00a4 04a57f1b b81a4161 62>
```
