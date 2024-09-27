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
    ```objc
      [classObj _ivarDescription]

      [classObj _propertyDescription]

      [classObj _methodDescription]

      [classObj _shortMethodDescription]
    ```

## 相关完整代码

`dynamicDebug/iOSOpenDev/jailAppleAccount/jailAppleAccount/libs/iOS/HookLogiOS.m`

```c
// write string to file
void writeStrToFile(char* filePath, char* outputStr){
  FILE *fp = fopen(filePath, "w");
  printf("fp=%p", fp);
  if(fp != NULL){
    fprintf(fp, "%s", outputStr);
    fclose(fp);
  } else {
    printf("Failed to open file %s", filePath);
  }
}

// write class description string into file
void dbgWriteClsDescToFile(char* className, id classObj){
  NSString* idNSStr = [classObj _ivarDescription];
  NSString* pdNSStr = [classObj _propertyDescription];
  NSString* mdNSStr = [classObj _methodDescription];
  NSString* smdNSStr = [classObj _shortMethodDescription];
  
  const char *idCStr = [idNSStr cStringUsingEncoding:NSUTF8StringEncoding];
  const char *pdCStr = [pdNSStr cStringUsingEncoding:NSUTF8StringEncoding];
  const char *mdCStr = [mdNSStr cStringUsingEncoding:NSUTF8StringEncoding];
  const char *smdCStr = [smdNSStr cStringUsingEncoding:NSUTF8StringEncoding];

    //    const char* smdOutputFile = "/var/root/dev/AADeviceInfo_shortMethodDescription.txt";
    //    const char* smdOutputFile = "/var/mobile/AADeviceInfo_shortMethodDescription.txt";
//    const char* outputFilePath = "/var/root/dev"; // failed for no write access
  const char* outputFilePath = "/var/mobile";
//    iosLogInfo("outputFilePath=%{public}s", outputFilePath);
//    const char* idOutputFile = "AADeviceInfo_ivarDescription.txt";
//    const char* pdOutputFile = "AADeviceInfo_propertyDescription.txt";
//    const char* mdOutputFile = "AADeviceInfo_methodDescription.txt";
//    const char* smdOutputFile = "AADeviceInfo_shortMethodDescription.txt";

  char idFullPath[200];
  char pdFullPath[200];
  char mdFullPath[200];
  char smdFullPath[200];

//    snprintf(idFullPath, sizeof(idFullPath), "%s/%s", outputFilePath, idOutputFile);
//    snprintf(pdFullPath, sizeof(pdFullPath), "%s/%s", outputFilePath, pdOutputFile);
//    snprintf(mdFullPath, sizeof(mdFullPath), "%s/%s", outputFilePath, mdOutputFile);
//    snprintf(smdFullPath, sizeof(smdFullPath), "%s/%s", outputFilePath, smdOutputFile);
  snprintf(idFullPath, sizeof(idFullPath), "%s/%s_ivarDescription.txt", outputFilePath, className);
  snprintf(pdFullPath, sizeof(pdFullPath), "%s/%s_propertyDescription.txt", outputFilePath, className);
  snprintf(mdFullPath, sizeof(mdFullPath), "%s/%s_methodDescription.txt", outputFilePath, className);
  snprintf(smdFullPath, sizeof(smdFullPath), "%s/%s_shortMethodDescription.txt", outputFilePath, className);

  writeStrToFile(idFullPath, (char*)idCStr);
  writeStrToFile(pdFullPath, (char*)pdCStr);
  writeStrToFile(mdFullPath, (char*)mdCStr);
  writeStrToFile(smdFullPath, (char*)smdCStr);

//    iosLogInfo("Written %s description into %s", className, outputFilePath);
}
```

调用：

`dynamicDebug/iOSOpenDev/jailAppleAccount/jailAppleAccount/jailAppleAccount.xm`

```c
%hook AADeviceInfo

- (id)udid{
  id objUdid = %orig;
  iosLogInfo("objUdid=%{public}@, self=%{public}@", objUdid, self);
  dbgWriteClsDescToFile("AADeviceInfo", self);
  return objUdid;
}

%end
```

注：最新代码详见：

* [HookLogiOS.m](https://github.com/crifan/crifanLib/blob/master/iOS/HookLogiOS.m)
* [crifanLib.c](https://github.com/crifan/crifanLib/blob/master/c/crifanLib.c)
