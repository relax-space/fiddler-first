# fiddler-first

## 开始

### 如何抓取手机app,包括安卓7.0以上?
1. 安装模拟器: 为了能抓安卓7以上的包
2. 安装fiddler: 为了在pc端 抓取 app的请求

### 详细说明
1. 安装fiddler Everywhere: 为了在pc端 抓取 app的请求
    1.点击右上角小图标 "Settings"，选择菜单项 "HTTPS"，勾选 "Capture HTTPS traffic"。
    2.选择菜单项 "Connections"，勾选 "Allow remote computers to connect"，其它项保留默认设置即可。

2. 安装模拟器: 为了能抓安卓7以上的包
    * 安装模拟器 [网易 MuMu 模拟器](https://mumu.163.com)
    * [安装adb](http://tools.android-studio.org/index.php/sdk) 因为我不知道怎么向模拟器的安全目录拷贝文件,所以用adb命令
    * 安装app 如果应用中心没有,则可以先下载应用宝
    * 安装fiddler证书: 不确定这一步是否是必须,因为后面会拷贝pem证书

3. 模拟器设置代理
    打开 MuMu 模拟器 → 系统设置 → 选择 WLAN →（长按出弹框）选择修改网络 → 填写代理服务器信息 → 保存
    
4. 证书:
    * 下载fidder的证书, 然后转换成pem格式 ,如果windows没有openssl,请看[此文](https://github.com/relax-space/sign-first/tree/main/openssl)

    `$ openssl x509 -in FiddlerRootCertificate.crt -inform DER -out FiddlerRootCertificate.pem -outform PEM`
    * 修改证书文件名为Android 系统证书格式：<hash>.0 

    `FiddlerRootCertificate.pem => 45accdf7.0`
    * 把本地证书上传到手机目录中：/system/etc/security/cacerts
    
    `adb_server.exe push C:\Users\Administrator\Desktop\2\45accdf7.0 /system/etc/security/cacerts`

### 引用

https://segmentfault.com/a/1190000038422757

https://mumu.163.com/help/20210531/35047_951108.html
