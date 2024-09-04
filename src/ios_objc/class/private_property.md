# 私有成员属性

## Xcode调试时访问类的实例的私有成员属性变量值

对于类`WAPreparedRegistrationURL`：

`WhatsApp/headers/WhatsApp_v23.20.79_headers_WhatsApp/WAPreparedRegistrationURL.h`

```c
#import <objc/NSObject.h>

@class NSArray, NSString, NSURL;

@interface WAPreparedRegistrationURL : NSObject
{
    NSString *_baseURLString;
    NSArray *_params;
    NSURL *_proxyURL;
}

- (void).cxx_destruct;
- (id)urlWithTokenArray:(id)arg1;
- (id)urlWithRegistrationToken:(id)arg1 backupToken:(id)arg2;
- (id)initWithBaseURLString:(id)arg1 params:(id)arg2 encryptWithProxyURL:(id)arg3;

@end
```

-》

* 类`WAPreparedRegistrationURL`的私有属性
  * `_baseURLString`
  * `_params`
  * `_proxyURL`

Xcode调试时，有对应的类的实例：

```bash
(lldb) po 0x0000000282170b80
<WAPreparedRegistrationURL: 0x282170b80>
```

想要查看：

* 类的`WAPreparedRegistrationURL`的**私有**属性=成员=变量的值
  * `_baseURLString`

具体方式：

（1）valueForKey

* 语法：`po [objcObj valueForKey: @"_xxx"]`
  * 属性名不带下划线也可以：`po [objcObj valueForKey: @"xxx"]`

```bash
(lldb) po [0x282170b80 valueForKey: @"_baseURLString"]
https://v.whatsapp.net/v2/exist

(lldb) po [0x282170b80 valueForKey: @"baseURLString"]
https://v.whatsapp.net/v2/exist
```

（2）指针
```bash
(lldb) po ((WAPreparedRegistrationURL*)0x282170b80)->_baseURLString
https://v.whatsapp.net/v2/exist
```

（3）偏移量+内存值 == 自己计算指针和内存中的值

```bash
(lldb) p/x 0x282170b80 + 0x08
(long) $18 = 0x0000000282170b88
(lldb) x/2gx 0x0000000282170b88
0x282170b88: 0x00000002833bbf80 0x000000028680ed90
(lldb) po 0x00000002833bbf80
https://v.whatsapp.net/v2/exist
```

其中：

* `0x282170b80 + 0x08` == `((*WAPreparedRegistrationURL)0x282170b80)->_baseURLString`
* 而内存地址是：`0x00000002833bbf80`
    * 其中保存的内容，就是：`NSString*`类型的URL值了

### 常见错误

* 用点.去访问：不带下划线，是无法访问的

```bash
(lldb) po ((WAPreparedRegistrationURL*)0x282170b80).baseURLString
error: expression failed to parse:
error: <user expression 23>:1:43: property 'baseURLString' not found on object of type 'WAPreparedRegistrationURL *'
((WAPreparedRegistrationURL*)0x282170b80).baseURLString
                                          ^
```

* 用点.去访问：带下划线，虽然也可以打印出值的
  * 但其实语法是错误的，但会自动会告诉你正确的语法：用指针->访问

```bash
(lldb) po ((WAPreparedRegistrationURL*)0x282170b80)._baseURLString
https://v.whatsapp.net/v2/exist

  Fix-it applied, fixed expression was: 
    ((WAPreparedRegistrationURL*)0x282170b80)->_baseURLString
```

* po无法，以ObjC的语法，去直接查看属性名（不论是带下划线还是不带下划线）-》 都会报错

```bash
(lldb) po [0x282170b80 baseURLString]
error: Execution was interrupted, reason: Attempted to dereference an invalid ObjC Object or send it an unrecognized selector.
The process has been returned to the state before expression evaluation.

(lldb) po [0x282170b80 _baseURLString]
error: Execution was interrupted, reason: Attempted to dereference an invalid ObjC Object or send it an unrecognized selector.
The process has been returned to the state before expression evaluation.
```

* 用指针访问时，不带下划线的话，会报报语法错误：找不到属性名=成员名=member

```bash
(lldb) po ((WAPreparedRegistrationURL*)0x282170b80)->baseURLString
error: expression failed to parse:
error: <user expression 17>:1:44: 'WAPreparedRegistrationURL' does not have a member named 'baseURLString'
((WAPreparedRegistrationURL*)0x282170b80)->baseURLString
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~  ^
```

即可。