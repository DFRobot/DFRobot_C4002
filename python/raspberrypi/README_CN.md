# DFRobot_C4002
- [English Version](./README.md)

这是⼀款侧装运动检测11m，静⽌检测11m的24Ghz毫⽶波测距雷达传感器（顶装运动检测范围直径11m，静⽌检测11m），同时具备靠近远离检测功能、区域分区检测功能、环境底噪采集功能，板载光线检测传感器。此传感器适⽤于智能家居应⽤场景。

![svg](../../resources/images/C4002.jpg)


## 产品链接（https://www.dfrobot.com/product-3081.html）

    SKU：SEN0691

## 目录

* [概述](#概述)
* [库安装](#库安装)
* [方法](#方法)
* [兼容性](#兼容性)
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
使用此库前，请首先下载库文件，将其粘贴到树莓派的自定义目录中，然后打开examples文件夹并在该文件夹中运行演示。

## 方法

```python
  def begin(self,outpin = 255):
    '''!
      @brief begin
      param outpin: out引脚，默认为255，即不输出检测结果，可根据自己的需求进行设定
      @return True or False
    '''

  def set_run_led_state(self, run_led):
    '''!
      @brief set run led state
      @param switching LED_OFF:关闭 LED_ON:开启 LED_KEEP:保持原样
      @return True or False
    '''

  def set_out_led_state(self, out_led):
    '''!
      @brief 设置out引脚输出状态
      @param outled LED_OFF:关闭 LED_ON:开启 LED_KEEP:保持原样
      @return True or False
    '''

  def set_out_pin_mode(self, out_mode):
    '''!
      @brief 设置out脚输出模式
      @param out_mode
      @n  OUT_PIN_MODE1:只有目标运动时输出高电平。
      @n  OUT_PIN_MODE2:只有目标存在时输出高电平。
      @n  OUT_PIN_MODE3:只有目标存在或运动时输出高电平。
      @return True or False
    '''

  def start_env_calibration(self,delay_time,cont_time):
    '''!
      @brief 开始底噪校准
      @param delay_time: 延时时间.range:0-65535s
      @param cont_time : 持续采样校准时间.range:15-65535s
    '''

  def set_detect_range(self, closet_distance, farthest_distance):
    '''!
      @brief 设置检测范围,单位:cm,范围:0-1100cm
      @param closet_distance   : 最近距离
      @param farthest_distance : 最远距离
      @return True or False
    '''


  def configure_gate(self, gate_type, gate_data):
    '''!
      @brief 配置距离门
      @param gate_type: 距离门类型
      @n              MOTION_DISTANCE_GATE:运动距离门
      @n              PRESENCE_DISTANCE_GATE:存在距离门
      @param gate_data：距离门状态数据，这是一个数组，数组的长度取决于分辨率模式
      @n              80cm模式下，可设置的门为15个，20cm模式下，可设置的门为25个，
      @n              每个门对应数组的下标，从0开始
      @return True or False
    '''

  def factory_reset(self):
    '''!
      @brief 恢复出厂设置
      @return True or False
    '''

  def set_resolution_mode(self, resolution_mode):
    '''!
      @brief 设置分辨率模式
      @param resolution_mode: 分辨率模式
      @n              RESOLUTION_80CM:80cm
      @n              RESOLUTION_20CM:20cm
      @return True or False
    '''

  def set_report_period(self, period):
    '''!
      @brief 设置上报周期
      @param period 上报周期，单位：0.1s
      @return True or False
    '''

  def set_light_thresh(self, threshold):
    '''!
      @brief 设置光照阈值
      @param threshold 光照阈值, 范围: 0-50, 单位: lux
      @n     注意：当阀组设置为0时，无论光照强度为多少，都会触发目标检测功能.
      @n     当阀值不为0时，只有当光照强度小于阀值时，才会触发目标检测功能；否则不会触发
      @return True or False
    '''

  def set_gate_thresh(self,gate_type , thresh):
    '''!
      @brief 设置门阈值
      @param gate_type: 门类型
      @n              MOTION_DISTANCE_GATE  :运动距离门
      @n              PRESENCE_DISTANCE_GATE:存在距离门
      @param thresh: 阈值，这是一个数组，数组的长度取决于分辨率模式
      @n                ，80cm模式下，可设置的门为15个，20cm模式下，
      @n                可设置的门为25个
      @return True or False
    '''

  def set_baudrate(self, baudrate):
    '''!
      @brief 设置波特率
      @param baudrate 波特率
      @n     注意: 波特率设置后，重启生效
      @n     波特率不应设置过高，否则会导致数据丢失
      @return True or False
    '''

  def get_note_info(self):
    '''!
      @brief 获取周期上报的目标信息
    '''

  def get_target_state(self):
    '''!
      @brief 得到目标状态
      @return 目标状态
      @n     NO_TARGET:没有目标
      @n     PRESENCE :静态存在
      @n     MOTION   :运动
    '''

  def get_presence_gate_index(self):
    '''!
      @brief 获取存在目标的距离索引
      @n     注意: 当分辨率模式为80cm时, 返回的数据0到15位可能被设置为1,1表示目标存在.
      @n     当分辨率模式为20cm时, 返回的数据0到25位可能被设置为1,1表示目标存在.
      @return 存在目标的距离索引, 范围: 0-0xFFFFFFFF.
    '''

  def get_presence_target_info(self):
    '''!
      @brief 得到存在目标信息
      @return 存在目标信息
      @n          distance:距离,单位:m
      @n          energy:能量,范围:0-100
    '''

  def get_motion_target_info(self):
    '''!
      @brief 得到运动目标信息
      @return 运动目标信息
      @n          distance    :运动距离,单位:m
      @n          speed       :运动速度,单位:m/s
      @n          energy      :运动能量,范围:0-100
      @n          direction   :方向信息
      @n              AWAY        :远离
      @n              NODIRECTION :无方向
      @n              APPROACHING :靠近
    '''

  def get_out_target_state(self):
    '''!
      @brief 得到out引脚输出状态
      @return 目标状态
      @n  NO_TARGET             :没有目标
      @n  MOTION                :目标运动
      @n  PRESENCE              :目标静态存在
      @n  MOTION_OR_NO_TARGET   :运动或没有目标
      @n  PRESENCE_OR_NO_TARGET :存在或没有目标
      @n  MOTION_OR_PRESENCE    :运动或存在目标
      @n  PIN_ERROR             :引脚错误
    '''

  def set_lock_time(self, lock_time):
    '''!
    @brief 封锁时间设置，由有人变为无人时，封锁检测功能1秒钟（默认值,可调），在封锁时
    @n   间内传感器不检测目标，封锁时间计时完成后才再次允许检测目标。
    @param lock_time : 封锁时间, 单位: s 范围:0.2-10s 精度:0.1s
    @return True or False
    '''

  def set_target_disappear_delay(self, disappear_time):
    '''!
    @brief 设置目标消失延时时间
    @param disappear_time : 延迟时间, 单位: s ，范围： (0-65535s)
    @return True or False
    '''

  def set_sensitivity(self, gate_type, sensitivity):
    '''!
    @brief 设置灵敏度
    @param gate_type : 门类型
    @n  MOTION_DISTANCE_GATE    :运动距离门
    @n  PRESENCE_DISTANCE_GATE  :存在距离门
    @param sensitivity
    @n  LOW_THRESH_GROUP     :低灵敏度组
    @n  MID_THRESH_GROUP  :中间灵敏度组
    @n  HIGH_THRESH_GROUP    :高灵敏度组
    @n  CUSTOM_THRESH_GROUP  :自定义灵敏度组
    @return True or False
    '''

  def get_sensitivity(self, gate_type):
    '''!
    @brief 获取灵敏度
    @param gate_type 门类型
    @n  MOTION_DISTANCE_GATE  :运动距离门
    @n  PRESENCE_DISTANCE_GATE:存在距离门
    @return 灵敏度
    '''

  def get_light_thresh(self):
    '''!
    @brief 获取环境光照阈值
    @return 环境光照阈值,单位:lux
    '''

  def get_detect_range(self):
    '''!
    @brief 获取检测范围
    @return DetectRange
    @n          closest :范围左值, 单位:0-1100,单位:cm
    @n          farthest:范围右值, 范围:0-1100,单位:cm
    '''

  def get_target_disappear_delay(self):
    '''!
    @brief 获取目标消失延时时间
    @return 目标消失延时时间,单位:s
    '''

  def get_all_config_params(self):
    '''!
    @brief get all config params
    @return ConfigParams object
    @n          cur_light_threshold           :当前环境光照阈值,单位:lux
    @n          cur_detect_range              :当前检测范围,单位:cm
    @n          cur_target_disappe_delay_time :当前目标消失延时时间,单位:s
    @n          cur_motion_sensitivity        :当前运动距离门灵敏度,范围:0-100
    @n          cur_presence_sensitivity      :当前存在距离门灵敏度,范围:0-100
    @n          cur_out_mode                  :当前out模式
    @n          cur_resolution_mode           :当前分辨率模式
    @n          cur_led_status                :当前LED状态
    '''

  def get_presence_count_down(self):
    '''!
    @brief 目标消失后，状态由存在变为无目标状态的剩余时间
    @return 剩余时间, 单位: s.
    '''

  def get_distance_gate_thresh(self,gate_type):
    '''!
    @brief 获取距离门阈值
    @return distance gate threshold
    '''
```

## 兼容性

* RaspberryPi Version

| Board        | 正常运行  | 运行失败   | 未测试    | 备注
| ------------ | :-------: | :--------: | :------: | :-----: |
| RaspberryPi2 |           |            |    √     |         |
| RaspberryPi3 |           |            |    √     |         |
| RaspberryPi4 |     √     |            |          |         |

* Python版本

| Python  | Work Well | Work Wrong | Untested | Remarks |
| ------- | :-------: | :--------: | :------: | ------- |
| Python2 |     √     |            |          |         |
| Python3 |           |            |    √     |         |


## 历史

- 2025/11/04 - V1.0.0 版本

## 创作者

Written by JiaLi(zhixin.liu@dfrobot.com), 2025. (Welcome to our [website](https://www.dfrobot.com/))
