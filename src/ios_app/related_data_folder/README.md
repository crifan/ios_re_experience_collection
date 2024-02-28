# app相关文件目录和数据

TODO:

* 【整理】iOS逆向心得：app完全卸载后仍有可能有app相关的数据
* 【整理】iOS逆向心得：Keychain数据库
* 【未解决】iOS逆向WhatsApp：调试IdentityKeypairData调用SecItemAdd写入Keychain数据库的具体逻辑
* 【整理】iOS逆向：Keychain数据库字段含义

---

iOS的app安装后，相关数据和内容：

* 文件目录
  * `Bundle`目录
    * 根目录：`/private/var/containers/Bundle/Application/`
  * `Data`目录
    * 根目录：`/private/var/mobile/Containers/Data/Application/`
  * `Shared AppGroup`目录
    * 根目录：`/private/var/mobile/Containers/Shared/AppGroup/`
* 数据
  * Keychain数据
    * `Keychain-2.db`
      * 位置：`/private/var/Keychains/keychain-2.db`
      * 相关函数
        * 写入数据：`SecItemAdd`
        * 更新数据：`SecItemUpdate`

## 举例

### WhatsApp

* WhatsApp
  * WhatsApp
    * `Bundle`目录
      * `/private/var/containers/Bundle/Application/B42F04DD-E264-401B-A72C-C00B240A1E81/`
    * `Data`目录
      * `/private/var/mobile/Containers/Data/Application/3856AB23-E286-4EE0-B06E-A0519A591AA8/`
    * AppGroup目录
      * `/private/var/mobile/Containers/Shared/AppGroup/D70C70AC-D347-4640-9667-1AA86D05CB65/`
  * 数据
    * Keychain数据
      * `Keychain-2.db`
        * 位置：`/private/var/Keychains/keychain-2.db`
