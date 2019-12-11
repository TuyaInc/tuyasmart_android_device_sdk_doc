## *低功耗模式（标准版暂未包含）

```java
class TransJNIInterface {
    
    /**
     * 进入低功耗
     *
     * @param interval 心跳间隔30-120s，默认60s,如果小于0则不发送
     * @param callback app唤醒的回调
     * @return
     */
    public boolean enableLowPower(int interval, WakeUpCallback callback);


    /**
     * 退出低功耗
     *
     * @return
     */
    public boolean disableLowPower();
    
}
```
