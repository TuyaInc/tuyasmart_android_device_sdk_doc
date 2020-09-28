# 配网重试

配网失败会出现在两个阶段，分别是**配网准备阶段**和**配网尝试阶段**，前者多为设备自身问题（相机启动失败、网络连接故障等）导致，可以进行重试。后者可能由外部错误导致（账号权限问题、无线网络故障等），建议提示用户重新操作。  
重试准备阶段：在`INetConfigManager.NetConfigCallback`的`onNetPrepareFailed`回调中进行重试

```java
/**
             * 配网准备阶段失败，建议重试
             * @param type 配网类型 ConfigProvider.TYPE_XX
             * @param msg 错误信息
             */
            @Override
            public void onNetPrepareFailed(int type, String msg) {
                Log.w(TAG, "onNetPrepareFailed: " + type + " / " + msg);
                iNetConfigManager.retry(type);
            }
```