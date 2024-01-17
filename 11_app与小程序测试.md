# app 测试

> 主要从功能和专项方面考虑
> 功能方面主要考虑 app 功能、业务逻辑、数据交互是否正常，是否满足需求文档要求
> 除此之外考虑 app 启动，热启动【锁屏，后台】、冷启动
> 考虑 app 首次打开的授权权限问题
> 考虑 app 内部层级关系是否过深
> 清除文件，清除缓存，杀死后台进程
> 广告，跳转，错误引导

> 专项测试
>
> > 安装卸载更新
> >
> > > 初次安装，卸载安装，覆盖安装，新版本覆盖旧版本，旧版本覆盖新版本
> > > 强制更新，非强制更新
> > >
> > > > 不更新能不能使用
> > > > 拒绝更新是否还有提示，能否正常操作
> > > > 更新下载一半下次能否继续更新
>
> 中断交叉事件
>
> > 关机，闹钟，来电，短信
>
> 兼容
>
> > 手机系统，系统版本【android 9-14，ios 12-17】，品牌，分辨率【10802400、10202340、14402560、14003200】，尺寸【6.4-6.8】，屏幕类型
>
> 网络
> 性能
> 稳定性

# qnet 怎么用

> 选择弱网环境模板，比如 2 g、3 g、地铁，也可以手动设置参数【带宽，延迟抖动，丢包】
> 选择 app 启动

## Adb

```powershell
查看现有设备
adb devices
启动adb服务
adb start -server
关闭adb服务
adb kill-server
安装apk
adb install apk地址
覆盖安装
adb install -r apk地址
将电脑文件拷贝到手机
adb push
将手机文件拷贝到电脑
adb pull



进入shell环境
adb shell -s 设备名
搜索设备当前运行的包名或页面名
adb shell dumpsys window w | findstr name=
查看指定app日志
adb shell  "logcat | grep 包名"
查看安装的包
adb shell pm list package -f
查看第三方包名
adb shell pm list package -3
查看包安装路径
adb shell pm path 包名
启动
adb shell am start 包名/页面名
停止
adb shell am force-stop 包名
查看网卡信息
adb shell ifconfig
查看网络连通性
adb shell ping ip地址

```

## monkey 怎么用

> 一般对 app 进行稳定性、压力测试时使用 monkey  
> 先下载配置 jdk 和 androidSDK 环境  
> 执行 adb shell monkey -p 包名 -s 种子数 --throttle 延迟  
> 还可以设定时间百分比选项 --pct-touch 点击事件，--pct-motion 移动事件，--pct-syskeys 系统按键事件  
> 还可以添加忽略错误 --ignore-crashes 忽略崩溃，--ignore-timeouts 忽略 anr 错误  
> -v 设置日志详细程度  
> 加随机事件次数，一般 5w-10w 条

## monkey 测试如何进行结果分析

> 通过 monkey 日志分析  
> 将 monkey 日志重定向到文件里  
> 在日志内搜索错误关键字，比如 error，anr，crash，exception  
> 如果发现错误，结合上下文分析如何产生  
> 可以通过种子数复现问题  
> 可以用 adb bugreport 生成测试报告查看相关信息

## 崩溃有可能的原因

> 内存泄露、内存溢出、程序代码逻辑错误、设备兼容性问题

## app 性能怎么测的

> 使用 solopi 和性能狗，主要使用 solopi  
> 先下载安装 solopi  
> 使用 adb tcpip 命令开放端口  
> 选择要测的软件  
> 勾选要测试的指标：cpu、内存、电量、网络、温度  
> 开启监控  
> 按常规操作使用软件  
> 检查 solopi 生成的指标数据
>
> > 应用程序 cpu 和内存占比在 20% 以下  
> > fps 30-60  
> > 流量与实际使用流量相近  
> > 电量使用稳定，没有过多耗电

## Ios 和 Android 区别

> 开发语言不一样  
> 机制不同，ios 是沙盒机制，Android 是虚拟机机制  
> Ios 使用伪后台，Android 使用真后台  
> 分辨率不同  
> 消息推送不同
>
> > Android 需要在 app 里实现推送，或接入第三方 sdk 实现推送【友盟】  
> > Ios 使用官方推送服务
>
> Android 默认有三个虚拟按键，ios 只有一个  
> Android 和 ios 程序上架方式不同
>
> > Android 需要在各大应用商店上架  
> > ios 在 AppStore 上架

## app 和 web 区别

> 架构不同，app 是 C/S 架构，web 是 B/S 架构  
> Web 的客户端性能只需要考虑响应时间，app 还有考虑电量内存 cpu 使用情况  
> Web 考虑不同浏览器内核和分辨率，app 考虑不同手机品牌、操作系统、版本、分辨率  
> app 还要考虑专项测试【中断事件、网络、安装卸载更新、前后台横竖屏切换、权限等】，web 考虑非功能

## 怎么测埋点

> 有两种方式  
> 查看客户端埋点日志，安卓可以使用 adb shell logcat，ios 使用 Xcode  
> 使用第三方平台进行埋点管理，神测平台
>
> > 输入要测试的埋点名称  
> > 点击刷新
>
> 主要测试有没有漏埋点，埋点事件名称和 id 是否准确，埋点数据是否准确，埋点记录的频率是否准确，数据分析统计结果是否准确

## 小程序怎么测的

> 使用真机或微信开发者工具  
> 考虑功能是否与需求一致、业务逻辑、数据交互  
> 对小程序入口检测：搜索、扫二维码、链接分享  
> 授权状态：已授权、未授权、授权后取消  
> 兼容性：不同系统、不同系统版本、不同微信版本、不同分辨率  
> 缓存：清除缓存  
> 网络：弱网、断网  
> 安全：敏感数据加密  
> 性能：cpu、内存、耗电量、帧率、网络【开发调试 -> 性能监控面板】

## app 内存泄漏怎么测的

> 使用 Android studio 中的 monitor 工具【profiler】  
> 下载安装 Android studio  
> 配置 androidSDK  
> 连接手机打开 usb 调试  
> 打开想测试的 app  
> 打开 profiler  
> 选择要测试的 app  
> 正常操作 app  
> 导出内存相关分析结果  
> 如果结果中包含 leaks 相关数据，则 app 存在内存泄漏  
> 可以通过 leaks 定位到代码块，提交给开发修复
