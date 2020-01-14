# 配网解绑
###从APP解绑
```java
//解绑成功后进入解绑回调
IPCServiceManager.getInstance().setResetHandler(isHardward -> {
            //处理解绑 isHardward参数代表是否为硬重置 默认为false
            }
        });
```
###从设备端解绑
```java
//主动触发重置，也会进入上面的回调
IPCServiceManager.getInstance().reset();
```