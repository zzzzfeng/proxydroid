# proxydroid
编译版https://github.com/madeye/proxydroid

# remark
- Android代理软件大多不支持认证，而从google play上下载的proxydroid apk有广告，所以去掉广告编译了下

# 步骤
###########2020/02/13版代码支持gradle编译，使用Android studio即可###########
源码使用maven编译

- 首先要编译android-sdk-deployer工具下载android相关依赖
```
git clone https://github.com/mosabua/maven-android-sdk-deployer.git 
pushd maven-android-sdk-deployer
export ANDROID_HOME=【/path/to/android/sdk】
mvn install -P 【4.1】
popd
```
需要修改pom.xml中的android.sdk.platform为本地sdk版本，并查看profile是否存在对应版本。然后mvn install -P version

- 然后编译proxydroid
  - 修改proxydroid pom.xml的`<sdk><platform>`
  - 注释掉com.google.android.gms和com.flurry.android依赖
  - 搜索源码（包括androidmanifest.xml）中的flurry、android.gms、AdView，去掉相关代码
  - 最后mvn clean install编译

如果编译脚本出现命令执行错误，可直接执行命令获得错误详细信息
