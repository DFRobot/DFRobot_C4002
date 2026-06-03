# DFRobot_C4002
- [English Version](./README.md)

这是⼀款侧装运动检测11m，静⽌检测11m的24Ghz毫⽶波测距雷达传感器（顶装运动检测范围直径11m，静⽌检测11m），同时具备靠近远离检测功能、区域分区检测功能、环境底噪采集功能，板载光线检测传感器。此传感器适⽤于智能家居应⽤场景。

![svg](./resources/images/C4002.jpg)


## 产品链接(https://www.dfrobot.com/product-3081.html)

    SKU：SEN0691

## 目录

* [概述](#概述)
* [库安装](#库安装)
* [方法](#方法)
* [兼容性](#兼容性y)
* [历史](#历史)
* [创作者](#创作者)

## 概述
- 支持量程为0-11m
- 支持5V主控器
- 支持串口通信
- 支持out引脚输出检测结果
- 支持out引脚输出模式设置
- 支持环境底噪采集
- 支持光照强度检测
- 支持距离门使能和阀值设置
- 支持汇报周期设置
- 支持环境光照阈值设置
- 支持80cm和20cm分辨率设置
- 支持获取目标状态以及相关数据

## 库安装
这里提供两种使用本库的方法：
1.打开Arduino IDE,在状态栏中的Tools--->Manager Libraries 搜索"DFRobot_C4002"并安装本库.
2.首先下载库文件,将其粘贴到\Arduino\libraries目录中,然后打开examples文件夹并在该文件夹中运行演示.

## 方法

```C++
  /**
   * @fn begin
   * @brief 初始化串口并设置输出引脚.
   * @param outPin: 输出引脚, 默认255, 即不使用输出引脚.
   * @return true: 初始化成功. false: 初始化失败.
  */
  bool begin(uint8_t outPin = 255);

  /**
   * @fn setRunLedState
   * @brief 设置run Led状态.
   * @param switching
   *      eLedOff: 关闭run LED.
   *      eLedOn : 打开run LED.
   * @return true: 操作LED成功. false: 操作LED失败.
  */
  bool setRunLedState(eLedMode_t switching);

  /**
   * @fn setOutLedState
   * @brief 设置输出Led状态.
   * @param switching
   * @n     eLedOff: 关闭输出LED.
   * @n     eLedOn : 打开输出LED.
   * @return true: 输出LED成功. false: 输出LED失败.
  */
  bool setOutLedState(eLedMode_t switching);

  /**
   * @fn setOutPinMode
   * @brief 设置out脚输出模式
   * @param outMode
   * @n      eOutpinMode1: 只有当检测到运动时，才会输出高电平。
   * @n      eOutpinMode2: 只有在检测到存在时，才会输出高电平。
   * @n      eOutpinMode3: 当检测到运动或存在时，都会输出高电平。
   * @return true: 设置输出引脚模式成功. false: 设置输出引脚模式失败.
  */
  bool setOutPinMode(eOutpinMode_t outMode);

  /**
   * @fn startEnvCalibration
   * @brief 开始底噪校准
   * @param delayTime: 延迟开始执行校准采样的时间, 单位: s
   * @param contTime : 校准持续时间, 单位: s
   * @return true: 开始校准成功. false: 开始校准失败.
  */
  void startEnvCalibration(uint16_t delayTime, uint16_t contTime);

  /**
   * @fn setDetectRange
   * @brief 设置检测距离范围,范围: 0-1100cm
   * @param closest : 最短距离, 单位: cm
   * @param farthest: 最长距离, 单位: cm
   * @return true: 设置检测范围成功. false: 设置检测范围失败.
  */
  bool setDetectRange(uint16_t closest, uint16_t farthest);

  /**
   * @fn configureGate
   * @brief 配置距离门
   * @param gateType
   * @n      eMotionDistGate  : 设置运动距离门参数时使用此参数
   * @n      ePresenceDistGate: 设置存在距离门参数时使用此参数
   * @param gateData: 需要一个uint8_t类型的数组，参数0和1分别表示禁用和启用距离门
   * @return true: 配置门成功. false: 配置门失败.
  */
  bool configureGate(eDistanceGateType_t gateType, uint8_t *gateData);

  /**
   * @fn factoryReset
   * @brief 恢复默认设置
   * @return true: 恢复默认设置成功. false: 恢复默认设置失败.
   */
  bool factoryReset(void);

  /**
   * @fn setResolutionMode
   * @brief 设置分辨率模式
   * @param mode : 分辨率模式, eResolution80Cm: 80cm, eResolution20Cm: 20cm
   * @return true: 设置分辨率模式成功. false: 设置分辨率模式失败.
  */
  bool setResolutionMode(eResolutionMode_t mode);

  /**
   * @fn setReportPeriod
   * @brief 设置数据汇报周期
   * @param period : 数据汇报周期, 范围: 0-255, 单位: 0.1s
   * @return true: 设置数据汇报周期成功, false: 设置数据汇报周期失败.
  */
  bool setReportPeriod(uint8_t period);

  /**
   * @fn setLightThresh
   * @brief 设置光照阈值
   * @param threshold : 光照阈值, 范围: 0-50, 单位: lux
   * @n     注意：当阀组设置为0时，无论光照强度为多少，都会触发目标检测功能.
   * @n     当阀值不为0时，只有当光照强度小于阀值时，才会触发目标检测功能；否则不会触发
   * @return true: 设置光照阈值成功. false: 设置光照阈值失败.
   */
  bool setLightThresh(float threshold);

  /**
   * @fn setGateThresh
   * @brief 设置门阈值
   * @param gateType
   * @n      eMotionDistGate  : 设置运动距离门参数时使用此参数
   * @n      ePresenceDistGate: 设置存在距离门参数时使用此参数
   * @param thresh : 需要一个uint8_t类型的数组，参数0-99表示门的阈值
   * @return true: 设置门阈值成功. false: 设置门阈值失败.
  */
  bool setGateThresh(eDistanceGateType_t gateType,uint8_t * thresh);

  /**
   * @fn setBaudrate
   * @brief 设置串口波特率
   * @param baud : 波特率类型, eBaudrate_t
   * @n      eBaud57600   : 57600 bps
   * @n      eBaud115200  : 115200 bps
   * @n      eBaud230400  : 230400 bps
   * @n      eBaud460800  : 460800 bps
   * @n      eBaud500000  : 500000 bps
   * @n      eBaud921600  : 921600 bps
   * @n      eBaud1000000 : 1000000 bps
   * @n     注意: 波特率不应设置过高，否则会导致数据丢失
   * @n     波特率设置后，重启生效
   * @return true: 设置波特率成功. false: 设置波特率失败.
  */
  bool setBaudrate(eBaudrate_t baud);

  /**
   * @fn getNoteInfo
   * @brief 得到通知信息
   * @return  sRetResult_t
   * @n           noteType            : 通知消息的类型.
   * @n           eResult     : 数据信息通知消息.
   * @n           eCalibration: 底噪校准通知消息.
   * @n           calibCountdown: 环境校准剩余时间, 单位: s.
  */
  sRetResult_t getNoteInfo(void);

  /**
   * @fn getTargetState
   * @brief 获取目标状态
   * @n          eNoTarget        : 无目标.
   * @n          ePresence        : 存在目标.
   * @n          eMotion          : 目标移动.
  */
  eTargetState_t getTargetState(void);

  /**
   * @fn getLightIntensity
   * @brief 获取当前光照强度
   * @return 当前光照强度, 单位: lux.
  */
  float getLightIntensity(void);

  /**
   * @fn getPresenceGateIndex
   * @brief 获取存在目标的距离索引
   * @n     注意: 当分辨率模式为80cm时, 返回的数据0到15位可能被设置为1表示目标存在.
   * @n     当分辨率模式为20cm时, 返回的数据0到25位可能被设置为1表示目标存在.
   * @return 存在目标的距离索引, 范围: 0-0xFFFFFFFF.
  */
  uint32_t getPresenceGateIndex(void);

  /**
   * @fn getPresenceTargetInfo
   * @brief 获取存在目标的信息
   * @return sPresenceTarget_t
   * @n        distance: 存在目标的距离, 单位: m.
   * @n        energy  : 存在目标的能量, 范围:0-99.
  */
  sPresenceTarget_t getPresenceTargetInfo(void);

  /**
   * @fn getMotionTargetInfo
   * @brief 获取移动目标的信息
   * @n        distance : 移动目标的距离, 单位: m.
   * @n        speed    : 移动目标的速度, 单位: m/s.
   * @n        energy   : 移动目标的能量, 范围:0-99.
   * @n        direction: 移动目标的方向, eMotionDirection_t.
   */
  sMotionTarget_t getMotionTargetInfo(void);

  /**
   * @fn getOutTargetState
   * @brief 获取输出目标状态
   * @return eTargetState_t
   * @n          eNoTarget           : 没有输出目标.
   * @n          ePresence           : 存在输出目标.
   * @n          eMotion             : 输出目标移动.
   * @n          eMotionOrPresence   : 输出目标移动或存在.
   * @n          eMotionOrNoTarget   : 输出目标移动或没有目标.
   * @n          ePresenceOrNoTarget : 输出目标存在或没有目标.
   * @n          ePinError           : 输出引脚错误.
  */
  eTargetState_t getOutTargetState(void);

   /**
   * @fn setLockTime
   * @brief 封锁时间设置，由有人变为无人时，封锁检测功能1秒钟（默认值,可调），在封锁时
   * @n   间内传感器不检测目标，封锁时间计时完成后才再次允许检测目标。
   * @param lockTime : 封锁时间, 单位: s 范围:0.2-10s 精度:0.1s
   * @return true: 设置封锁时间成功, false: 设置封锁时间失败.
  */
  bool setLockTime(float lockTime);

  /**
   * @fn setTargetDisappearDelay
   * @brief 设置目标消失延迟时间
   * @param delayTime : The delay time, unit: s (0-65535s)
   * @return true: 设置目标消失延迟时间成功, false: 设置目标消失延迟时间失败.
  */
  bool setTargetDisappearDelay(uint16_t delayTime);

  /**
   * @fn setSensitivity
   * @brief 设置检测灵敏度
   * @param gateType
   * @n      eMotionDistGate : 使用此参数启用运动距离门参数
   * @n      ePresenceDistGate: 使用此参数启用存在距离门参数
   * @param sensitivity : 灵敏度, eThreshGroup_t
   *       eLowThreshGroup   : 低灵敏度
   *       eMidThreshGroup   : 中灵敏度
   *       eHighThreshGroup  : 高灵敏度
   *       eCustomThreshGroup: 自定义灵敏度
   * @return true: 设置灵敏度成功, false: 设置灵敏度失败.
  */
  bool setSensitivity(eDistanceGateType_t gateType,eThreshGroup_t sensitivity);

  /**
   * @fn getLightThresh
   * @brief 获取光照阈值
   * @return 光照阈值, 单位: lux.
  */
  float getLightThresh(void);

  /**
   * @fn getDetectRange
   * @brief 获取距离门阈值
   * @return sDetectRange_t
   * @n        closest : 范围左值, 单位: cm,范围: 0-1100cm.
   * @n        farthest: 范围右值, 单位: cm,范围: 0-1100cm.
  */
  sDetectRange_t getDetectRange(void);

  /**
   * @fn getTargetDisappearDelay
   * @brief 获取目标消失延迟时间
   * @return 目标消失延迟时间, unit: s.
  */
  uint16_t getTargetDisappearDelay(void);

  /**
   * @fn getOutPinMode
   * @brief 获取out脚输出模式
   * @return eOutpinMode_t
   * @n          eOutpinMode1
   * @n          eOutpinMode2
   * @n          eOutpinMode3
  */
  eOutpinMode_t getOutPinMode(void);

  /**
   * @fn getResolutionMode
   * @brief 获取分辨率模式
   * @return eResolutionMode_t
   * @n          eResolution80Cm: 80cm
   * @n          eResolution20Cm: 20cm
  */
  eResolutionMode_t getResolutionMode(void);

  /**
   * @fn getSensitivity
   * @brief 获取检测灵敏度
   * @param gateType
   * @n      eMotionDistGate  : 使用此参数启用运动距离门参数
   * @n      ePresenceDistGate: 使用此参数启用存在距离门参数
   * @return eThreshGroup_t
  */
  eThreshGroup_t getSensitivity(eDistanceGateType_t gateType);

  /**
   * @fn getAllConfigParams
   * @brief 获取所有配置参数
   * @return sConfigParams_t
   * @n        curLightThreshold        : 当前光照强度阀值, 单位: lux.
   * @n        curDetectRange           : 当前探测范围, 单位: cm, 范围: 0-1100cm.
   * @n        curOutMode               : 当前输出模式, eOutpinMode_t.
   * @n        curResolutionMode        : 当前分辨率模式, eResolutionMode_t.
   * @n        curMotionSensitivity     : 当前运动灵敏度, eThreshGroup_t.
   * @n        curPresenceSensitivity   : 当前存在灵敏度, eThreshGroup_t.
   * @n        curTargetDisappearDelay  : 当前目标消失延迟时间, 单位: s.
   * @n        curLedStatus             : 当前run LED状态, eLedMode_t.
  */
  sConfigParams_t getAllConfigParams(void);

  /**
   * @fn getPresenceCountDown
   * @brief 目标消失后，状态由存在变为无目标状态的剩余时间
   * @return 剩余时间, 单位: s.
  */
  uint16_t getPresenceCountDown(void);

  /**
   * @fn getDistanceGateThresh
   * @brief 获取距离门阈值
   * @param gateType
   * @n      eMotionDistGate  : 使用这个参数启用运动距离门参数
   * @n      ePresenceDistGate: 使用这个参数启用存在距离门参数
   * @param gateData: 需要一个uint8_t类型的数组，参数0-99表示距离门的阈值
   * @return true: 获取距离门阈值成功, false: 获取距离门阈值失败.
  */
  bool getDistanceGateThresh(eDistanceGateType_t gateType,uint8_t *gateData);
```

## 兼容性

| 主板        | 通过 | 未通过 | 未测试 | 备注 |
| ----------- | :--: | :----: | :----: | ---- |
| Arduino uno |  √   |        |        |      |
| Mega2560    |  √   |        |        |      |
| Leonardo    |  √   |        |        |      |
| ESP32       |  √   |        |        |      |
| micro:bit   |      |        |   √    |      |


## 历史

- 2025/11/04 - V1.0.0 版本


## 创作者

Written by JiaLi(zhixin.liu@dfrobot.com), 2025. (Welcome to our [website](https://www.dfrobot.com/))
