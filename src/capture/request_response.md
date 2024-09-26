# request和response

概述：

* 调试网络信息：request和response
  * 如果Charles抓包抓不到详情，可以考虑写插件hook代码实现
    * 举例
      * Apple账号登录过程，抓包失败
        * 【未解决】iOS逆向Apple账号：用Charles抓包signin/v2/login的请求和响应的详情数据
        * 【未解决】Mac中Charles抓包：https请求始终只是显示CONNECT无法查看到详情数据
      * 后来转去用之前的插件hook代码
        * 主要hook的点是：
          * request
            * `NSMutableURLRequest`
              * `-[NSMutableURLRequest allHTTPHeaderFields]`
              * `-[NSMutableURLRequest addValue:forHTTPHeaderField:]`
              * `-[NSMutableURLRequest setValue:forHTTPHeaderField:]`
              * `-[NSMutableURLRequest setAllHTTPHeaderFields:]`
            * `NSURLRequest`
              * `-[NSURLRequest allHTTPHeaderFields]`
          * response
            * `NSHTTPURLResponse`
              * `-[NSHTTPURLResponse initWithURL：]`
              * `-[NSHTTPURLResponse allHeaderFields]`
              * `-[NSHTTPURLResponse initWithURL:statusCode:HTTPVersion:headerFields:]`
              * `-[NSHTTPURLResponse statusCode]`
  * 如果Charles抓包抓不到详情，可以考虑写用frida去hook打印
    * TODO：去试试效果，把结果整理过来

详解：

## 写插件hook代码

### 代码

```c

/*==============================================================================
 Request
==============================================================================*/

/*------------------------------------------------------------------------------
 NSMutableURLRequest
------------------------------------------------------------------------------*/

%hook NSMutableURLRequest

-(void)setHTTPBody:(NSData *)bodyData{
//    iosLogInfo("bodyData=%@", bodyData);
   NSURL *reqUrl = [self URL];
   iosLogInfo("reqUrl=%{public}@: bodyData=%{public}@", reqUrl, bodyData);
   return %orig;
}

//-(NSDictionary<NSString *,NSString *>)*allHTTPHeaderFields{
//-(NSDictionary<NSString *,NSString *>)allHTTPHeaderFields{
-(id)allHTTPHeaderFields{
//    NSDictionary<NSString *,NSString *> allHeaderDict = %orig;
   id allHeaderDict = %orig;
   NSURL *reqUrl = [self URL];
//    if ((allHeaderDict != nil) && ([[allHeaderDict allKeys] count])) {
   if (nonEmptyHeader(allHeaderDict)){
       if( [allHeaderDict count] > 3){
//            iosLogInfo("allHeaderDict=%{public}@ : reqUrl=%{public}@", allHeaderDict, reqUrl);
//            NSString* headerUrlNSStr = [NSString initWithFormat:@"reqUrl=%{public}@, allHeaderDict=%{public}@", reqUrl, allHeaderDict]
//            NSString* headerUrlNSStr = [NSString stringWithFormat:@"reqUrl=%{public}@, allHeaderDict=%{public}@", reqUrl, allHeaderDict];
//            NSString* headerUrlNSStr = [NSString stringWithFormat:@"reqUrl=%@, allHeaderDict=%@", reqUrl, allHeaderDict];
           NSString* headerUrlNSStr = [NSString stringWithFormat:@"NSMutableURLRequest:allHTTPHeaderFields reqUrl=%@, allHeaderDict=%@", reqUrl, allHeaderDict];
           logPossibleLargeStr(headerUrlNSStr);
           gNoUse = 1;
       }
   }
   return allHeaderDict;
}

- (void)addValue:(NSString *)value forHTTPHeaderField:(NSString *)field{
   NSURL *reqUrl = [self URL];
   iosLogInfo("field=%{public}@, value=%{public}@ : reqUrl=%{public}@", field, value, reqUrl);
   %orig;
}

- (void)setValue:(NSString *)value forHTTPHeaderField:(NSString *)field{
   NSURL *reqUrl = [self URL];
   iosLogInfo("field=%{public}@, value=%{public}@ : reqUrl=%{public}@", field, value, reqUrl);
   %orig;
}

- (void) setAllHTTPHeaderFields:(id)newAllHeaders{
   NSURL *reqUrl = [self URL];
   iosLogInfo("newAllHeaders=%{public}@ : reqUrl=%{public}@", newAllHeaders, reqUrl);
   %orig;
}

%end


/*------------------------------------------------------------------------------
NSURLRequest
------------------------------------------------------------------------------*/

%hook NSURLRequest

-(NSDictionary*)allHTTPHeaderFields{
   NSDictionary* allHeaderDict = %orig;
   NSURL *reqUrl = [self URL];
//    if ((allHeaderDict != nil) && ([[allHeaderDict allKeys] count])) {
   if (nonEmptyHeader(allHeaderDict)){
       if( [allHeaderDict count] > 3){
//            iosLogInfo("allHeaderDict=%{public}@ : reqUrl=%{public}@", allHeaderDict, reqUrl);
           NSString* reqHeaderUrlStr = [NSString stringWithFormat:@"NSURLRequest:allHTTPHeaderFields reqUrl=%@, allHeaderDict=%@", reqUrl, allHeaderDict];
           logPossibleLargeStr(reqHeaderUrlStr);
           gNoUse = 1;
       }
   }
   return allHeaderDict;
}

/*==============================================================================
Response
==============================================================================*/

/*------------------------------------------------------------------------------
NSHTTPURLResponse
------------------------------------------------------------------------------*/

%hook NSHTTPURLResponse

- (NSHTTPURLResponse*)initWithURL:(NSURL *)url statusCode:(NSInteger)statusCode HTTPVersion:(NSString *)HTTPVersion headerFields:(NSDictionary<NSString *,NSString *> *)headerFields{
   NSHTTPURLResponse* newUrlResp =  %orig;
   iosLogInfo("url=%{public}@,statusCode=%ld,HTTPVersion=%@,headerFields=%{public}@ -> newUrlResp=%{public}@", url, statusCode, HTTPVersion, headerFields, newUrlResp);
   return newUrlResp;
}

-(NSDictionary *)allHeaderFields{
   NSURL* curUrl = [self URL];
   NSDictionary* allHeader = %orig;

   //    iosLogInfo("curUrl=%{public}@ : allHeader=%{public}@", curUrl, allHeader);
   NSString* respUrlHeaderStr = [NSString stringWithFormat:@"NSHTTPURLResponse:allHeaderFields curUrl=%@ : allHeader=%@", curUrl, allHeader];
   logPossibleLargeStr(respUrlHeaderStr);

   return allHeader;
}

-(NSInteger)statusCode{
   NSURL* curUrl = [self URL];
   NSInteger respStatusCode = %orig;
   iosLogInfo("respStatusCode=%ld : curUrl=%{public}@", respStatusCode, curUrl);
   return respStatusCode;
}

%end

```

### 输出

* https://setup.icloud.com/setup/signin/v2/login
  * request
    * headers
      *   Accept = "*/*";
      *   "Accept-Encoding" = "gzip, deflate, br";
      *   "Accept-Language" = "zh-CN,zh-Hans";
      *   Authorization = "Basic YWRtaW5AY3JpZm...3NjRlRrUzB0dW0wc0Nwang2RURMTjRpbz1QRVQ=";
      *   "Content-Length" = 694;
      *   "Content-Type" = "application/xml";
      *   "Device-UDID" = abdc0dd...8433a;
      *   "X-Apple-I-Device-Configuration-Mode" = 0;
      *   "X-MMe-Client-Info" = "<iPhone10,1> <iPhone OS;15.0;19A346> <com.apple.AppleAccount/1.0 (com.apple.Preferences/1109.1)>";
      *   "X-MMe-Country" = CN;
      *   "X-MMe-Language" = "zh-Hans-CN";
      *   "X-Mme-Device-Id" = abdc0dd...8433a;
  * response
    * headers
      *   "Apple-Originating-System" = UnknownOriginatingSystem;
      *   "Cache-Control" = "no-cache, no-store, private";
      *   Connection = "keep-alive";
      *   "Content-Encoding" = gzip;
      *   "Content-Length" = 4213;
      *   "Content-Type" = "application/xml; charset=UTF-8";
      *   Date = "Mon, 05 Jun 2023 09:44:17 GMT";
      *   Server = "AppleHttpServer/3faf4ee9434b";
      *   "Set-Cookie" = "show-china-terms=false;Expires=Thu, 01-Jan-1970 00:00:01 GMT;Path=/setup;HttpOnly";
      *   "Strict-Transport-Security" = "max-age=31536000; includeSubDomains";
      *   Via = "63119...319:8ef2...35a6b:hktko1";
      *   "X-Apple-Edge-Response-Time" = 3589;
      *   "X-Apple-Jingle-Correlation-Key" = 4QJS...P4;
      *   "X-Apple-Request-UUID" = "e4132a7d-b..0-4..e-8..f-6387...7f";
      *   "X-Responding-Instance" = "setupservice:45100103:pv43p51ic-zteg06100801:8003:2316B377:36c327430fe1";
      *   "access-control-expose-headers" = "X-Apple-Request-UUID,Via";
      *   "apple-seq" = 0;
      *   "apple-tk" = false;
      *   "x-apple-user-partition" = 51;
