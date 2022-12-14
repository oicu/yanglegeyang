# 《羊了个羊》连续通关秘籍 3 种及原理（失效）

:sheep: :ram: :goat: :sheep: :ram: :goat: :sheep: :ram: :goat:

验证通过的版本：2022-09-18 羊了个羊小程序 v20，后来小程序升级过好多次，加强了几次验证，下文的方法早已失效。

主要是讲原理，玩游戏不是目的，重要是学习知识。

## 1. API 接口一键通关

Python 和 Java 版本又是依赖又是编译，麻烦得要死，不如用 Windows 自带的 PowerShell 脚本简单。

使用 Windows 10 的 PowerShell 5.1 版本验证通过。

### 1.1. 原理

带账号 token 访问通过游戏接口的 URL 网址即可。

### 1.2. 操作步骤

1. 在电脑或者手机里先打开抓包工具，玩《羊了个羊》第 1 关。
1. 查看抓包工具记录里域名 *cat-match.easygame2021.com* 请求体中的 `t` 值和 `User-Agent` 值（脚本里默认是 iPhone 15.7）。
1. 修改脚本里的 `$header_t` 和 `$header_user_agent` 参数。
1. 打开 _Windows PowerShell ISE_，输入 `Set-Executionpolicy RemoteSigned` 允许后再运行通关脚本。

### 1.3. 推荐的抓包工具

| 平台 | 软件 | 备注 |
| --- | --- | -- |
|PC|Fiddler、HTTPDebugger、Charles| 最新版 PC 微信抓不到，换低版本微信 |
|Android|HttpCanary| |
|iOS|Stream|[Lcry 编写的保姆级 Stream 教程](https://github.com/Lcry/a-sheep-assistant/blob/main/docs/stream.md)|

其实 PC 版微信 v3.2.1 连抓包都不需要，`Applet\wx141bfb9b73c970a9\.S0` 文件里就有明文的 token 值，已通关的日期和获得的皮肤也记录在这个文件里，但这个文件里的 prop_remove、prop_cancel、prop_random 的值是动态更新的，无法修改。

PC 版本微信 v3.7.6 使用 `usrkvstorage0.db` 键值文件保存配置，非明文。

### 1.4. 参考链接

Python 版本
- [a-sheep-assistant](https://github.com/Lcry/a-sheep-assistant) 
- [python-requests-ylgy](https://www.gaoyuanqi.cn/python-requests-ylgy)

Java 版本有 $ 嫌疑，去掉了。

## 2. 重复第一关

### 2.1. 原理

`80001` 就是第一关的代号，把游戏资源文件里每一关的代号都修改为第一关即可。

`10017` 也是类似的意思，也都修改。

### 2.2. PC 版微信

支持最新的 PC 版微信 v3.7.6

用 `Everything` 搜索《羊了个羊》小程序的 ID 号 `wx141bfb9b73c970a9`，会有 2 个文件夹，一个是存放小程序，一个是存放用户数据。

进入用户数据的文件夹，再继续用 `Everything` 的**指定目录搜索** `.json content:80001`

修改最新的一个 json 文件即可，原文件大小约 2KB，参考内容如下：

```
[1,0,0,[["cc.JsonAsset",["_name","json"],1]],[[0,0,1,3]],[[0,"levelConfigData",{"dailyLevel":[[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001],[80001,80001]],"topicLevel":[[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017],[10017,10017]]}]],0,0,[],[],[]]
```

### 2.3. Android 手机

安卓手机的修改方法类似，不重复造车轮，请看[点链接](https://new.qq.com/rain/a/20220917A048QV00)。

## 3. 连续通关及重玩

通关后会获得皮肤，等第二天才能继续玩，着急的话直接修改系统日期到下一天就可以继续玩。

得到的皮肤保存在本地配置文件里，所以 PC 版玩的状态不支持同步到手机。

要重玩也简单，删除本地配置文件 `.S0` 或者 `usrkvstorage0.db` 即可，但我建议直接删 `wx141bfb9b73c970a9` 用户配置文件夹。

## 4. 无限道具版本制作原理

只测试了 PC 版微信，Android 懒得试。我这里介绍的是制作方法，理论上支持最新版本的小程序。

PC 微信 v3.7.6 使用修改过的小程序会提示“加载小程序代码包失败”，我猜测打开小程序前加了哈希验证，所以建议安装 `PC 微信 v3.2.1` 版本。

### 4.1. 原理

使用道具时不减少数量，看 1 次广告或者分享获得道具后，可以无限使用。

### 4.2. 制作方法

#### 4.2.1. 解密 wxapkg 文件

用 `Everything` 搜索《羊了个羊》小程序的 ID 号 `wx141bfb9b73c970a9`，会有 2 个文件夹，一个是存放小程序，一个是存放用户数据。

进入小程序 wxapkg 文件所在的文件夹，里面会有数字命名的子文件夹，进入最大的那个数字文件夹，比如 `20`，会看到 `__APP__.wxapkg` 文件。

因为 PC 版微信的小程序文件 wxapkg 是加密的，先解密才能修改，任选一种工具：

- [x] go 版解密 [pc_wxapkg_decrypt](https://github.com/BlackTrace/pc_wxapkg_decrypt)

  `pc_wxapkg_decrypt.exe -wxid wx141bfb9b73c970a9 -in __APP__.wxapkg -out dec.wxapkg`

- [ ] python 版解密 [pc_wxapkg_decrypt_python](https://github.com/superdashu/pc_wxapkg_decrypt_python) 或者 [wxapkg_v1mmwx_decrypt](https://github.com/xiongnemo/wxapkg_v1mmwx_decrypt)

  `py -3 pc_wxapkg_decrypt.py --wxid wx141bfb9b73c970a9 -f __APP__.wxapkg -o dec.wxapkg`

#### 4.2.2. 编辑 wxapkg 文件

得到解密的文件 `dec.wxapkg`，无需反编译，用 EverEdit 等支持 HEX 模式的编辑器打开，直接二进制修改（也可以用 python 或者 sed 修改文件，我懒得写代码）。

要无限洗牌道具就把 `prop_random--` 里的 `--` 替换为 2 个空格，撤销、移出的道具修改方法类似。

#### 4.2.3. 加密 wxapkg 文件

重新加密 wxapkg 文件（我写的脚本，还没开源，懂看解密的自然懂写加密）

`py -3 pc_wxapkg_encrypt.py --wxid wx141bfb9b73c970a9 -f dec.wxapkg -o __APP__.wxapkg`

#### 4.2.4. 验证

然后重新进入小程序，获取一次洗牌道具后就可以无限洗牌了。
