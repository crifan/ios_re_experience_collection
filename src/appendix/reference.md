# 参考资料

* 【未解决】iOS的app安装和使用后相关内容：数据、文件、目录
* 【未解决】iOS逆向WhatsApp：-[WASignalKeyStore storeSignedPreKeyRecord:prekeyId:creationDate:]_block
* 【未解决】iOS逆向WhatsApp：-[WASignalKeyStore executeDatabaseFetchRequest:context:]
* 【整理】iOS逆向：如何查看Mach-O的虚拟地址基地址vmaddr即镜像地址基地址image base
* 【整理】iOS逆向心得：寻找函数触发时机：hook类的alloc+init函数
* 【整理】iOS逆向心得：寻找函数触发时机：重新安装后以Spawn方式启动调试或交叉引用找上层调用
* 【整理】iOS逆向心得：app完全卸载后仍有可能有app相关的数据
* 【未解决】iOS逆向WhatsApp：-[WASignalKeyStore saveToKeychainIdentityKeypairData:registrationIdData:]
* 【未解决】iOS逆向WhatsApp：-[WASignalCoordinator createAndSaveIdentity]
* 【未解决】iOS逆向WhatsApp：signal_protocol_key_helper_generate_registration_id
* 【整理】iOS逆向调试：修改寄存器值使得程序走期望的分支
* 【已解决】iOS逆向WhatsApp：-[WASignalCoordinator localKeysAvailable]
* 【整理】iOS逆向心得：Keychain数据库
* 【未解决】iOS逆向WhatsApp：Keychain中genp中WhatsApp数据何时和如何被写入的
* 【未解决】iOS中的keychain保存位置路径
* 【记录】Mac中用DB Browser for SQLite查看keychain数据库文件：/var/Keychains/keychain-2.db
* 【已解决】Mac中如何打开iOS中的SQLite3格式的数据库.db文件
* 【记录】iOS逆向WhatsApp：查找keychain的数据库/var/Keychains/keychain-2.db中WhatsApp相关数据
* 【已解决】Mac中DB Browser for SQLite中删除genp数据表中WhatsApp的记录
* 【未解决】iOS逆向WhatsApp：寻找gena即kSecAttrGeneric的值0x45534916来源：从Axolotl引用入手
* 【未解决】iOS逆向WhatsApp：寻找gena即kSecAttrGeneric的值0x45534916来源：从SecItemAdd引用处入手
* 【未解决】iOS逆向WhatsApp：+[WASignalKeyStore baseKeychainQuery]
* 【整理】iOS逆向心得：用watchpoint或wivar监视寻找变量赋值的地方
* 【未解决】iOS逆向WhatsApp：用watchpoint监视寻找WASignalKeyStore的_registrationIdData值来源
* 【未解决】iOS逆向WhatsApp：WAFBUUID中的uuid如何初始化设置值的
* 【整理】iOS逆向调试：lldb用正则查找函数时记得要转义特殊字符
* 【已解决】iOS逆向：lldb中获取ObjC中dict中key的值
* 【未解决】iOS逆向WhatsApp：-[WARegistrationURLBuilder initWithPhoneNumber:language:locale:fbUUID:waUUID:chatPrivateKey:e2eKeyBundle:smbClientSignedVNameCertData:]
* 【未解决】iOS逆向WhatsApp：用watchpoint监视寻找WASignalKeyStore的_registrationIdData值来源
* 【整理】iOS逆向Xcode调试心得：查看当前所有变量值
* 【整理】Xcode调试心得：调试触发断点时Fetching Variables on iPhone
* 【已解决】从XCode崩溃的地址寻找所属二进制的代码段和函数位置
* 【整理】Xcode调试心得：给汇编代码窗口保持打开状态不关闭
* 【无需解决】Xcode的目标调试iOS设备出现2个：一个是arm64一个是arm64e
* 【整理】iOS逆向心得：iOS的ObjC的属性内部有可能是有额外生成属性值的处理逻辑的
* 【规避解决】Xcode调试iOSOpenDev的xm文件无法定位到源代码位置
* 【未解决】iOS逆向调试iOSOpenDev的Logos插件时%orig触发断点时无法正常打开并定位到xm源码位置
* 【未解决】iOS逆向WhatsApp：研究v2/reg_onboard_abprop的参数值cc、in、rc的来源和逻辑
* 【已解决】iOS逆向：获取iOS的app的主二进制文件路径
* 【整理】Xcode去Attach挂载调试app或二进制：通过PID或进程名
* 【整理】iOS调试心得：崩溃日志解析工具
* 【整理】lldb调试心得：用指针引用ObjC类的私有属性
* 【整理】iOS逆向：Xcode调试时访问类的实例的私有成员属性变量值
* 【整理】iOS逆向lldb调试心得：用点.去引用查看ObjC类的属性值
* 【整理】iOS逆向心得：找逆向关键函数时记得hook研究多个不同目标
* 【整理】iOS逆向：从ARM汇编代码反推理解出部分的原始代码逻辑
* 【已解决】iOS逆向时_os_log_impl的详细的参数和含义
* 【整理】iOS逆向心得：NSString、os_log等带格式化参数时的参数传递逻辑
* 【已解决】iOS逆向Apple账号：研究signin/v2/login请求的header头信息
* 【已解决】旧Mac中重新调试jailAppleAccount插件查看signin/v2/login等网络请求相关数据
* 【已解决】iOS逆向：hook代码中通过函数打印处函数调用堆栈
* 【整理】iOS逆向心得：对于iOS内置类比如NSMutableURLRequest的属性和函数的扩展
* 【已解决】iOS逆向：Xcode写hook插件看能否调试触发断点
* 【已解决】如何才能让Xcode中hook代码断点被触发实时调试插件hook代码
* 【记录】iOS逆向Apple账号：Xcode实时调试hook代码研究账号登录过程
* 【已解决】新建和初始化iOSOpenDev的Xcode项目：jailAppleAccount的hook插件
* 【已解决】换iPhone11去确保Xcode的iOSOpenDev的hook插件正常工作
* 【整理】Xcode去Attach挂载调试app或二进制：通过PID或进程名
* 【整理】iOS逆向心得：手动从汇编代码的adrp计算出字符串即objc_msgSend的参数的函数名
* 【整理】iOS逆向调试心得：从po打印值看出当前变量类型是实例对象还是类本身
* 【未解决】iOS逆向Apple账号：-[AAUISignInViewController _attemptAuthenticationWithContext:]
* 【整理】逆向调试心得：给被大量调用的底层函数加hook且加参数过滤会导致app运行很慢甚至卡死
* 【已解决】iOS逆向Apple账号：通过插件hook去打印AADeviceInfo的类的相关信息
* 