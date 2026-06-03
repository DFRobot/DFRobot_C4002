# DFRobot_C4002
- [中文版](./README_CN.md)

This is a 24Ghz millimeter-wave distance radar sensor with a side-mounted motion detection range of 11m and a static detection range of 11m (top-mounted motion detection range with a diameter of 11m and a static detection range of 11m). It also features proximity and distance detection functions, regional zoning detection functions, environmental noise collection functions, and an on-board light detection sensor. This sensor is suitable for smart home application scenarios.

![svg](./resources/images/C4002.jpg)


## Product Link(https://www.dfrobot.com/product-3081.html)

    SKU：SEN0691

## Table of Contents

* [Summary](#Summary)
* [Installation](#Installation)
* [Methods](#Methods)
* [Compatibility](#Compatibility)
* [History](#History)
* [Credits](#Credits)

## Summary

* Supports a detection range of 0-11m
* Supports 5V main controller
* Supports serial communication
* Supports OUT pin output for detection results
* Supports OUT pin output mode setting
* Supports environmental noise collection
* Supports light intensity detection
* Supports distance threshold enable and threshold value setting
* Supports reporting cycle setting
* Supports environmental light threshold setting
* Supports 80cm and 20cm resolution setting
* Supports obtaining target status and related data

## Installation
There are two methods for using this library：
1. Open Arduino IDE, search for "DFRobot_C4002" on the status bar in Tools ->Manager Libraries and install the library.
2. Download the library file before use, paste it into \Arduino\libraries directory, then open the examples folder and run the demo in the folder.

## Methods

```C++
  /**
  * @fn begin
  * @brief Initialize the serial port and set the output pin
  * @param outPin: The output pin, default is 255, which means no output pin is used.
  * @return true: Initialization succeeded, false: Initialization failed.
  */
  bool begin(uint8_t outPin = 255);

  /**
   * @fn setRunLedState
   * @brief Set the operation led of runing status
   * @param switching
   *      eLedOff: Turn off the operation LED.
   *      eLedOn : Turn on the operation LED.
   * @return true: Operation LED succeeded, false: Operation LED failed.
  */
  bool setRunLedState(eLedMode_t switching);

  /**
   * @fn setOutLedState
   * @brief Set the output led
   * @param switching
   * @n     eLedOff: Turn off the output LED.
   * @n     eLedOn : Turn on the output LED.
   * @return true: Output LED succeeded, false: Output LED failed.
  */
  bool setOutLedState(eLedMode_t switching);

  /**
   * @fn setOutPinMode
   * @brief Set the output pin mode
   * @param outMode
   * @n      eOutpinMode1: Only when motion is detected will a high level be output.
   * @n      eOutpinMode2: A high level is output only when its presence is detected.
   * @n      eOutpinMode3: A high level only appears when motion or presence is detected.
   * @return true: Set output pin mode succeeded, false: Set output pin mode failed.
  */
  bool setOutPinMode(eOutpinMode_t outMode);

  /**
   * @fn startEnvCalibration
   * @brief Start environment calibration
   * @param delayTime: Delay the time when the calibration starts to be executed, unit: s
   * @param contTime : The calibration time, unit: s
   * @return true: Start calibration succeeded, false: Start calibration failed.
  */
  void startEnvCalibration(uint16_t delayTime ,uint16_t contTime);

  /**
   * @fn setDetectRange
   * @brief Set the detection distance range,range: 0-1100cm
   * @param closest : The closest distance to detect,   unit: cm
   * @param farthest: The farthest distance to detect,  unit: cm
   * @return true: Set detection range succeeded, false: Set detection range failed.
  */
  bool setDetectRange(uint16_t closest,uint16_t farthest);

  /**
   * @fn configureGate
   * @brief Configure the distance gate function
   * @param gateType
   * @n      eMotionDistGate   : Use this parameter when the motion gate parameter is enabled
   * @n      ePresenceDistGate : Use this parameter when the presence gate parameter is enabled
   * @param gateData: An array of type uint8 t is needed, with parameters 0 and 1 representing disabling and enabling respectively
   * @return true: Configure gate succeeded, false: Configure gate failed.
  */
  bool configureGate(eDistanceGateType_t gateType, uint8_t *gateData);

  /**
   * @fn factoryReset
   * @brief Factory reset the device
   * @return true: Factory reset succeeded, false: Factory reset failed.
   */
  bool factoryReset(void);

  /**
   * @fn setResolutionMode
   * @brief Set the detection distance range,range: 0-1100cm
   * @param mode : The resolution mode,  eResolution80Cm: 80cm, eResolution20Cm: 20cm
   * @return true: Set resolution mode succeeded, false: Set resolution mode failed.
  */
  bool setResolutionMode(eResolutionMode_t mode);

  /**
   * @fn setReportPeriod
   * @brief Set the report period
   * @param period : The report period, range: 0-255, unit: 0.1s
   * @return true: Set report period succeeded, false: Set report period failed.
  */
  bool setReportPeriod(uint8_t period);

  /**
   * @fn setLightThresh
   * @brief Set the light threshold
   * @param threshold : The light threshold, range: 0-50, unit: lux
   * @n     Note: When the valve group is set to 0, the target detection function will be triggered regardless of the light intensity.
   * @n     When the threshold is not 0, the target inspection function will only be activated when the light intensity is lower than the threshold; otherwise, it will not be activated
   * @return true: Set light threshold succeeded, false: Set light threshold failed.
   */
  bool setLightThresh(float threshold);

  /**
   * @fn setGateThresh
   * @brief Set the gate threshold
   * @param gateType
   * @n      eMotionDistGate  : Use this parameter when the motion gate parameter is enabled
   * @n      ePresenceDistGate: Use this parameter when the presence gate parameter is enabled
   * @param thresh : An array of type uint8 t is needed, with parameters 0-99 representing the threshold value of the gate
   * @return true: Set gate threshold succeeded, false: Set gate threshold failed.
  */
  bool setGateThresh(eDistanceGateType_t gateType,uint8_t * thresh);

  /**
   * @fn setBaudrate
   * @brief Set the baudrate of the serial port
   * @param baud : The baud rate type, eBaudrate_t
   * @n      eBaud57600   : 57600 bps
   * @n      eBaud115200  : 115200 bps
   * @n      eBaud230400  : 230400 bps
   * @n      eBaud460800  : 460800 bps
   * @n      eBaud500000  : 500000 bps
   * @n      eBaud921600  : 921600 bps
   * @n      eBaud1000000 : 1000000 bps
   * @n     Note: The baud rate should not be too high; otherwise, it will lead to data loss
   * @n     It takes effect after a successful restart
   * @return true: Set baudrate succeeded, false: Set baudrate failed.
  */
  bool setBaudrate(eBaudrate_t baud);

  /**
   * @fn getNoteInfo
   * @brief Get the detection result and environment calibration information
   * @return  sRetResult_t
   * @n           noteType      : The type of the notification message.
   * @n             eResult: detection result notification message.
   * @n             eCalibration: environment calibration notification message.
   * @n           calibCountdown: The remaining time of the environment calibration, unit: s.
  */
  sRetResult_t getNoteInfo(void);

  /**
   * @fn getTargetState
   * @brief Get the current state of the target
   * @return eTargetState_t
   * @n          eNoTarget        : No target is detected.
   * @n          ePresence        : The target is detected.
   * @n          eMotion          : The target is motion.
  */
  eTargetState_t getTargetState(void);

  /**
   * @fn getLightIntensity
   * @brief Get the current light intensity
   * @return The current light intensity, unit: lux.
  */
  float getLightIntensity(void);

  /**
   * @fn getPresenceGateIndex
   * @brief Get the index of the detected target
   * @n     Note: When the resolution mode is 80cm, 0 to 15 bits may be set to 1 to represent the presence of the target.
   * @n     When the resolution mode is 20cm, 0 to 25 bits may be set to 1 to represent the presence of the target.
   * @return The index of the detected target, range: 0-0xFFFFFFFF.
  */
  uint32_t getPresenceGateIndex(void);

  /**
   * @fn getPresenceTargetInfo
   * @brief Get the information of the detected target
   * @return sPresenceTarget_t
   * @n        distance: The distance of the detected target, unit: m.
   * @n        energy  : The energy of the detected target, range:0-99.
  */
  sPresenceTarget_t getPresenceTargetInfo(void);

  /**
   * @fn getMotionTargetInfo
   * @brief Get the information of the detected target
   * @return sMotionTarget_t
   * @n        distance : The distance of the detected target, unit: m.
   * @n        speed    : The speed of the detected target, unit: m/s.
   * @n        energy   : The energy of the detected target, range:0-99.
   * @n        direction: The direction of the detected target, eMotionDirection_t.
   */
  sMotionTarget_t getMotionTargetInfo(void);

  /**
   * @fn getOutTargetState
   * @brief Get the current state of the output target
   * @return eTargetState_t
   * @n          eNoTarget            : No output target is detected.
   * @n          ePresence            : The output target is detected.
   * @n          eMotion              : The output target is motion.
   * @n          eMotionOrPresence    : The output target is motion or detected.
   * @n          eMotionOrNoTarget    : The output target is motion or no output target is detected.
   * @n          ePresenceOrNoTarget  : The output target is detected or no output target is detected.
   * @n          ePinError            : The pin error occurred.
  */
  eTargetState_t getOutTargetState(void);

   /**
   * @fn setLockTime
   * @brief Set the lock time. When changing from occupied to unoccupied, the detection function
   * @n   is locked for 1 second (default, adjustable). During the lock time, the sensor does not
   * @n   detect targets. Detection is allowed again after the lock time expires.
   * @param lockTime : The lock time, unit: s range:0.2-10s accuracy:0.1s
   * @return true: Set lock time succeeded, false: Set lock time failed.
  */
  bool setLockTime(float lockTime);

  /**
   * @fn setTargetDisappearDelay
   * @brief Set the delay time for the target to disappear after it is no longer detected
   * @param delayTime : The delay time, unit: s (0-65535s)
   * @return true: Set target disappear delay succeeded, false: Set target disappear delay failed.
  */
  bool setTargetDisappearDelay(uint16_t delayTime);

  /**
   * @fn setSensitivity
   * @brief Set the sensitivity of the detection
   * @param gateType
   * @n      eMotionDistGate  : Use this parameter when the motion gate parameter is enabled
   * @n      ePresenceDistGate: Use this parameter when the presence gate parameter is enabled
   * @param sensitivity : The sensitivity
   * @n      eLowThreshGroup   : Low sensitivity
   * @n      eMidThreshGroup   : Medium sensitivity
   * @n      eHighThreshGroup  : High sensitivity
   * @n      eCustomThreshGroup: Custom sensitivity
   * @return true: Set sensitivity succeeded, false: Set sensitivity failed.
  */
  bool setSensitivity(eDistanceGateType_t gateType,eThreshGroup_t sensitivity);

  /**
   * @fn getLightThresh
   * @brief Get the light threshold
   * @return The light threshold, unit: lux.
  */
  float getLightThresh(void);

  /**
   * @fn getDetectRange
   * @brief Get the distance gate threshold
   * @return sDetectRange_t
   * @n        closest : The closest distance to detect, unit: cm,range: 0-1100cm.
   * @n        farthest: The farthest distance to detect, unit: cm,range: 0-1100cm.
  */
  sDetectRange_t getDetectRange(void);

  /**
   * @fngetTargetDisappearDelay
   * @brief Get the delay time for the target to disappear after it is no longer detected
   * @return The delay time, unit: s.
  */
  uint16_t getTargetDisappearDelay(void);

  /**
   * @fn getOutPinMode
   * @brief Get the output pin mode
   * @return eOutpinMode_t
   * @n          eOutpinMode1: Only when motion is detected will a high level be output.
   * @n          eOutpinMode2: A high level is output only when its presence is detected.
   * @n          eOutpinMode3: A high level only appears when motion or presence is detected.
  */
  eOutpinMode_t getOutPinMode(void);

  /**
   * @fn getResolutionMode
   * @brief Get the resolution mode
   * @return eResolutionMode_t
   * @n          eResolution80Cm: 80cm
   * @n          eResolution20Cm: 20cm
  */
  eResolutionMode_t getResolutionMode(void);

  /**
   * @fn getSensitivity
   * @brief Get the sensitivity of the detection
   * @param gateType
   * @n      eMotionDistGate : Use this parameter when the motion gate parameter is enabled
   * @n      ePresenceDistGate: Use this parameter when the presence gate parameter is enabled
   * @return eThreshGroup_t
  */
  eThreshGroup_t getSensitivity(eDistanceGateType_t gateType);

  /**
   * @fn getAllConfigParams
   * @brief Get all the configuration parameters of the device
   * @return sConfigParams_t
   * @n        curLightThreshold        : The light threshold, unit: lux.
   * @n        curDetectRange           : The detection distance range, unit: cm, range: 0-1100cm.
   * @n        curOutMode               : The output mode, eOutpinMode_t.
   * @n        curResolutionMode        : The resolution mode, eResolutionMode_t.
   * @n        curMotionSensitivity     : The sensitivity of the motion detection, eThreshGroup_t.
   * @n        curPresenceSensitivity   : The sensitivity of the presence detection, eThreshGroup_t.
   * @n        curTargetDisappearDelay  : The delay time for the target to disappear after it is no longer detected, unit: s.
   * @n        curLedStatus             : The led status, eLedMode_t.
  */
  sConfigParams_t getAllConfigParams(void);

  /**
   * @fn getPresenceCountDown
   * @brief Get the remaining time after target disappears, state changes from presence to no target
   * @return The remaining time, unit: s.
  */
  uint16_t getPresenceCountDown(void);

  /**
   * @fn getDistanceGateThresh
   * @brief Get the distance gate threshold
   * @param gateType
   * @n      eMotionDistGate : Use this parameter when the motion gate parameter is enabled
   * @n      ePresenceDistGate: Use this parameter when the presence gate parameter is enabled
   * @param gateData: An array of type uint8 t is needed, with parameters 0-99 representing the threshold value of the distance gate
   * @return true: Get distance gate threshold succeeded, false: Get distance gate threshold failed.
  */
  bool getDistanceGateThresh(eDistanceGateType_t gateType,uint8_t *gateData);
```

## Compatibility

MCU                | Work Well    | Work Wrong   | Untested    | Remarks
------------------ | :----------: | :----------: | :---------: | :----:
Arduino Uno        |      √       |              |             |
Arduino MEGA2560   |      √       |              |             |
Arduino Leonardo   |      √       |              |             |
FireBeetle-ESP32   |      √       |              |             |
Micro:bit          |              |              |      √      |


## History

- 2025/11/04 - V1.0.0 version

## Credits

Written by JiaLi(zhixin.liu@dfrobot.com), 2025. (Welcome to our [website](https://www.dfrobot.com/))
