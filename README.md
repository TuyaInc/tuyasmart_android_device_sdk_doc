---
description: Android物联网应用接入涂鸦平台所使用的SDK
---

# 涂鸦智能 Android IPC SDK 文档

<!---SDK下载;--->

<!---* [minSdkVersion >= Anroid N](assets/24/ipc-sdk.zip)--->
<!---* [minSdkVersion >= 22](assets/22/ipc-sdk.zip)--->

Demo 地址 [https://github.com/TuyaInc/tuyasmart\_android\_device\_sdk\_demo](https://github.com/TuyaInc/tuyasmart_android_device_sdk_demo)

> 提示：接入和使用可能遇到的一些常见问题，在<a href="./faq.md">FAQ</a>都有记录，遇到困难可以先查看一下：）

* **IPC\_SDK for v1.1.1 \(2020-7-22\)**
	* 底层mqtt优化
* **IPC\_SDK for v1.1.0 \(2020-7-18\)**
	* 修复BUG
	* 移动侦测API升级
* **IPC\_SDK for v1.0.9 \(2020-7-18\)**
	* 兼容最低版本到Android 4.4
* **IPC\_SDK for v1.0.8 \(2020-7-7\)**
	* 开放视频流接收并发数参数设置
* **IPC\_SDK for v1.0.7 \(2020-7-4\)**
	* 修复DNS解析问题
* **IPC\_SDK for v1.0.6 \(2020-7-2\)**
	* 依赖优化
* **IPC\_SDK for v1.0.5 \(2020-6-30\)**
	* 修复测试文件写入失败导致的本地录像无效问题
* **IPC\_SDK for v1.0.4 \(2020-6-29\)**
	* 嵌入式SDK更新到最新版
	* 新增本地日志保存
	* 优化配网重试
	* 修复推流阻塞问题
	* 修复P2P导致的无响应
	* 优化解绑逻辑
* **IPC\_SDK for v0.1.6 \(2019-11-08\)**

  * 新增用户发送/订阅指定mqtt消息api
  * 新增mqtt配网
  * 默认支持mqtt配网，修复了打包依赖的问题 **\(2019-11-13\)**
  * 修复了配网连接失败多次回调的问题 **\(2019-11-14\)**
  * 修复夏令时时区错误 **\(2019-11-22\)**
  * 修复dp点重复上报错误 **\(2019-12-17\)**
  * API修改，将[MQTT](./sdk-api.md#mqtt)和[DP控制](./sdk-api.md#dp)相关方法归类 **\(2019-12-18\)**
  * 修复没有音频数据导致的视频回放跳帧问题 **\(2020-1-10\)**

  **IPC\_SDK for v0.1.5 \(2019-10-25\)**

  * 新增主动发送mqtt心跳接口
  * 修复录像初始化问题（2019-10-29）

  **IPC\_SDK for v0.1.4 \(2019-10-22\)**

  * 修复因为TransAPI优先初始化引起的Java层reset无法回调的问题

  **IPC\_SDK for v0.1.3 \(2019-10-15\)**

  * 修复stopAndRestartMultiMediaTrans等接口返回值错误

  **IPC\_SDK for v0.1.2 \(2019-10-8\)**

  * sdk 增加低功耗接口

  **IPC\_SDK for v0.1.1 \(2019-9-25\)**

  * sdk 再次改为初始化为耗时操作
  * 增加videotalk module，为可视对讲提供更方便的接入方式
  * 硬件重置时 删除录像文件

  **IPC\_SDK for v0.1.0 \(2019-09-20\)**

  * 修改没有相关配置会crash的bug
  * 新增低功耗模式

  **IPC\_SDK for v0.0.14 \(2019-09-17\)**

  * 修改时区非整数的问题

  **IPC\_SDK for v0.0.13 \(2019-09-07\)**

  * 修改多媒体通道初始化失败

  **IPC\_SDK for v0.0.12 \(2019-09-06\)**

  * 支持设备端主动挂断门铃呼叫流程
  * 更新门铃特性接口

  **IPC\_SDK for v0.0.11 \(2019-09-02\)**

  * 增加OTA进度报告接口

  **IPC\_SDK for v0.0.10 \(2019-08-10\)**

  * 增加接收音频推送消息、对讲开始和停止消息
  * 当传输通道关闭时，过滤所有的push 数据流

  **IPC\_SDK for v0.0.9 \(2019-07-18\)**

  * IPC SDK第九版本内容
    * 新增二维码配网预览输出

  **IPC\_SDK for v0.0.8 \(2019-06-05\)**

  * IPC SDK第八版本内容
    * 新增格式化录制目录删除接口
    * 修复获取时区错误问题

  **IPC\_SDK for v0.0.7 \(2019-05-09\)**

  * IPC SDK第七版本内容
    * 修改网络连接成功问题
    * 修改网络在低api下面的配置保存问题

  **IPC\_SDK for v0.0.6 \(2019-04-17\)**

  * IPC SDK第六版本内容
    * 增加视频录制接口
    * 修改配网bug

  **IPC\_SDK for v0.0.5 \(2019-04-09\)**

  * IPC SDK第五版本内容
    * 增加视频流停止开启回调接口

  **IPC\_SDK for v0.0.4 \(2019-04-03\)**

  * IPC SDK第四版本内容
    * 增加信号及视频清晰度切换的回调接口

  **IPC\_SDK for v0.0.3 \(2019-03-16\)**

  * IPC SDK第三版本内容
    * 修复5.0一下机型启动报错的问题（5.0以下无法使用蓝牙配网）
    * 修复云存储初始化失败问题

  **IPC\_SDK for v0.0.2 \(2019-03-08\)**

  * IPC SDK第二版本内容
    * 修复跨进程下获取权限的问题
    * 修改相机异常情况下闪退的问题
    * 修复蓝牙配网无法停止的bug
    * 升级嵌入式IPC-sdk
    * 修改不支持的对焦模式
    * 更新IPC SDK. 修复109 DP点内存错误问题

  **IPC\_SDK for v0.0.1 \(2019-02-25\)**

  * IPC SDK第一版本内容
    * 传输服务
    * 配网服务（蓝牙、二维码）

