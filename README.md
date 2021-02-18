## Action OpenWrt IPKs

------

利用GitHub Actions实现全自动的 **OpenWrt x86-64** ipk软件包自动编译



## 特性

> * 自动触发，每天检查源码是否存在更新，若存在更新就自动编译和打包ipk包并发布到Release；
> * 包含Luci绝大多数常用插件；
> * 所有软件包均包含依赖ipk，不用再去为了一个依赖ipk东奔西找。

## 食用方法

 1. 去Release下载文件 `x86-64-IPK.tar.gz` ，并确认SHA256是否匹配；
 2. 确认文件完整后打开压缩包，进入目录 `openwrt\packages\x86_64\` ，里面有几个文件夹，然后将文件夹里面所有的ipk文件解压到桌面（桌面新建文件夹）；
 3. 寻找需要的软件包并复制软件包全名（例如passwall）；
 4. 使用WinScp登录OpenWrt，切换到tmp目录下，将需要的软件包拖入此目录；
 5. 登录OpenWrt SSH，输入 `cd /tmp` 切换到tmp目录；
 6. 输入`opkg install 刚刚你复制的软件包名.ipk` ，回车；
 7. 若提示缺少依赖，复制软件包名去解压的那个文件夹查找，把依赖软件包装上，具体过程同上，然后再装你需要的软件包；
 8. 安装完成登入后台进行使用。

### 提醒

* 建议先将OPKG源更换为一个速度相对比较快且稳定的源，再执行 `opkg update` 更新源列表，这样可以省掉很多找某些依赖的时间（这里提供一个中国科技大学Linux用户协会OpenWrt镜像源： `https://openwrt.proxy.ustclug.org/` ）。
* 如果是用来更新本地已安装但较旧版本的软件包，建议先备份本地软件包内的数据（例如节点信息），然后执行卸载，将依赖等一并卸载，再按照上面的教程进行安装，避免各种玄学原因装不上。
* 不建议安装后台主题软件包，可能会导致后台Web页面瘫痪，若非要使用请做好备份。
* **非X86-64架构请勿使用本软件包！**
* 折腾必有风险，所以建议在安装任何一个软件包折腾前务必做好备份工作，以免出现不必要的麻烦。出现任何后果概不负责。
 

## 致谢
本项目是站在巨人的肩膀上完成的，没有他们的贡献不可能有这个项目，在此表示感谢。他们分别是：

- [P3TERX](https://p3terx.com/archives/build-openwrt-with-github-actions.html) 可以自行根据他的文章学习然后编译适合自己的OpenWrt。
- [rabbitwit](https://github.com/rabbitwit/test-xiaoyu/blob/a5e8c6b96704d78ee042c761adc8c08acb464008/.github/workflows/build-Lienol-openwrt.yml#L164)
- [Microsoft](https://www.microsoft.com)
- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub](https://github.com)
- [GitHub Actions](https://github.com/features/actions)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cisco](https://www.cisco.com/)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [Lean's OpenWrt](https://github.com/coolsnowwolf/lede)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)

## 更新日志

2021.02.17

增加SHA256验证(基于 /rabbitwit/test-xiaoyu 的小娱路由项目进行修改)

2021.02.15

修改Release IPK打包逻辑，至此项目已完成。后续只是增加提示等非必要内容了

2021.02.14 17:42

~~目前主要功能已经正常，可正常编译，但存在的问题就是Actions在执行发布到Release这一动作的时候提示没有文件，但实际上存放IPK的压缩包已经在Actions的输出目录打包好了。估计是原脚本上传没考虑好对上传软件包目录的支持。总之大体上没问题了，就是下载要去Actions里面去下载。不过我已将压缩包从Actions里提取出来，再手动发布到了Release，需要的朋友可以直接下载。~~

2021.02.13 22:00

~~目前正在修改测试中，编译到第三个小时的时候会报错，暂时先别fork了，等我测试完通过没毛病了再fork。谢谢。（吐槽下这玩意儿太玄学了~~

2021.02.13 23:47

~~报错，貌似是Luci-olsr的问题，故取消勾选软件包之后再次尝试编译。~~
