# proxydroid
修改自https://github.com/madeye/proxydroid

# 用途
- 通过配置Android iptables代理，捕获所有APP数据包（包括Proxy.NO_proxy设置）
- 增加自动导入证书到system功能，使得代理可以解码https协议
- 下载[Proxydroid.apk](https://github.com/zzzzfeng/proxydroid/releases)

# 注意
- 将代理证书（一般pem格式）转成`<hash>.0`格式，然后adb push到手机/data/local/tmp/目录
  ```
  (openssl x509 -inform DER -in your_cacert.der -out cacert.pem)
  openssl x509 -inform PEM -subject_hash_old -in cacert.pem |head -1
  mv cacert.pem <hash>.0
  ```
- app会导入/data/local/tmp/目录下所有符合格式的证书
- 代理推荐使用mitmproxy，若使用fiddler，需要执行`prefs set fiddler.network.https.SetCNFromSNI true`开启SNI才行
- 另外一种可以抓到全局包的方案是使用[VPN模式](https://github.com/raise-isayan/TunProxy)，使用[appstarter](https://github.com/zzzzfeng/appstarter)工具辅助导入证书