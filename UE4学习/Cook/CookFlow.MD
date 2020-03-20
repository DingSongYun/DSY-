## Cook流程解析
### 涉及到的一些源码位置
* `CookOnTheFlyServer.h/.cpp`
* `PakFileUtilities.cpp`
* `SavePackage.cpp`
* `BulkData.h/cpp`

### 单次Cook的文件
* `Always Cook Maps`
    未设置 `ECookByTheBookOptions::NoAlwaysCookMaps` 这个标记，
    * `Editor.ini` 中`AlwaysCookMaps`配置的地图加入`CookFiles`
    * Cook时设定的`IniMapSections`会加入到`CookFiles`中
    * `PackageSettings`中配置的`MapsToCook` 会加入到`CookFiles`
    * 如果以上步骤没有找到任何`Map`, `Editor.ini` 中`AllMaps`配置的地图加入`CookFiles`

* `Always Cook Directories`
    未设置 `ECookByTheBookOptions::NoAlwaysCookMaps` 这个标记, 
    `PackageSettings`中配置的`DirectoriesToAlwaysCook` 会加入到`CookFiles`

* Cook时设定的`IniMapSections`会加入到`CookFiles`中

* `Always Cook Package`
    * 未设置 `ECookByTheBookOptions::NoGameAlwaysCookPackages` 这个标记

* 平台相关的`Default Maps`配置
    平台相关的 ini文件, 相关Section: `GameMapsSettings`
    * `GameDefaultMap`
    * `ServerDefaultMap`
    * `GlobalDefaultGameMode`
    * `GlobalDefaultServerGameMode`
    * `GameInstanceClass`

* `Touch Interface`
    `Input.ini`中`DefaultTouchInterface`配置

* `Slate Package`
    * `GConfig` -> `UI` -> `ContentDirectories`

* 注意
    1. `SolicitedPackage` 相关还没搞清什么概念
    2. `DLC` 流程会不太一样

### UCookOnTheFlyServer::StartCookByTheBook()
1. 收集需要Cook的文件
2. 生成`FFilePlatformRequest` 加入到 `PackageTracker->CookRequests`中，在之后的Tick里做Cook的处理

### UPackage::Save()
获取两个单例对象


### Cook出来的一些相关文件
1. *.uasset
* 文件保存
     相关代码见 `AsyncWriteFileWithSplitExports::DoWork`

2. *.umap

3. *.uexp
    exp -> export

* 文件创建跟保存在 *.uasset 之后  
    相关代码见 `AsyncWriteFileWithSplitExports::DoWork`

4. .ubulk