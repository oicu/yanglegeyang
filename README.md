# 《羊了个羊》API 接口一键通关

:sheep: :ram: :goat: :sheep: :ram: :goat: :sheep: :ram: :goat:

Python 和 Java 版本又是依赖又是编译，麻烦得要死，不如用 Windows 自带的 PowerShell 脚本简单。

我使用 Windows 10 的 PowerShell 5.1 版本验证通过。

## 操作步骤

1. 在电脑或者手机里先打开抓包工具，玩《羊了个羊》第 1 关。
1. 查看抓包工具记录里域名 *cat-match.easygame2021.com* 请求体中的 `t` 值和 `User-Agent` 值（脚本里默认是 iPhone 15.7）。
1. 修改脚本里的 `$header_t` 和 `$header_user_agent` 参数。
1. 打开 _Windows PowerShell ISE_，输入 `Set-Executionpolicy RemoteSigned` 允许后再运行通关脚本。
 
## 推荐的抓包工具

| 平台 | 软件 | 备注 |
| --- | --- | -- |
|PC|Fiddler、HTTPDebugger、Charles| 最新版 PC 微信抓不到，换低版本微信 |
|Android|HttpCanary| |
|iOS|Stream|[Lcry 编写的保姆级 Stream 教程](https://github.com/Lcry/a-sheep-assistant/blob/main/docs/stream.md)|

## 参考链接

Java 版本
* https://github.com/Selina1981/yanglegeyang

Python 版本
* https://github.com/Lcry/a-sheep-assistant
* https://www.gaoyuanqi.cn/python-requests-ylgy
