---
description: IPC SDK API
---
###设计概述
IPC SDK的主要能力，按功能划分为不同类型的服务，服务由接口来定义其拥有的能力。每个服务都存在一个默认实现，当用户需要对某个服务做定制化时，需要实现服务对应的接口，并将服务注册来覆盖默认实现。服务管理类为`IPCServiceManager`

###服务定义
|  功能   |  服务定义名 | 接口 |
|  ----  | ----  | ---- |
| MQTT消息  | IPCService.MQTT_SERVICE | IMqttProcessManager |
| 配网相关  | IPCService.NET_CONFIG_SERVICE | INetConfigManager |
| DP控制  | IPCService.CONTROLLER_SERVICE | IControllerManager |
| 设备控制  | IPCService.DEVICE_SERVICE | IDeviceManager |
| 云存储&移动侦测相关  | IPCService.FEATURE_SERVICE | IFeatureManager |
| 多媒体配置 | IPCService.MEDIA_PARAM_SERVICE | IParamConfigManager |
| 流服务  | IPCService.MEDIA_TRANS_SERVICE | IMediaTransManager |
| 持久化存储  | IPCService.STORE_SERVICE | IStoreManager |
| 升级服务  | IPCService.UPGRADE_SERVICE | IUpgradeManager |

###服务使用
通过`IPCServiceManager.getService(String serviceName)`获取。
> example:  
> IControllerManager controllerManager = IPCServiceManager.getInstance()
> .getService(IPCServiceManager.IPCService.CONTROLLER_SERVICE);

###<div id="服务替换">服务替换</div>
通过`IPCServiceManager.getService(String serviceName)`获取。
> example:  
> public class CustomeStoreManager implements IStoreManager {
> }
> 
> IPCServiceManager.getInstance().registService(IPCService.STORE_SERVICE, new CustomeStoreManager())

