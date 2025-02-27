项目设计
**************

:link_to_translation:`en:[English]`

在设计能够处理音频信号或音频数据的项目时，我们通常会考虑使用以下组件：

**输入：**

* **模拟信号输入**：连接麦克风等设备
* **存储媒体**：如 microSD 卡，可读取其中的音频文件
* **Wi-Fi 接口**：从互联网获取音频数据流
* **蓝牙接口**：从蓝牙耳机等设备获取音频数据流
* **I2S 接口**：从编解码芯片获取音频数据流
* **以太网接口**：从互联网获取音频数据流
* **芯片内部 flash**：播放音频样本
* **用户交互**：按钮或其他提供用户输入的方式

**输出：**

* **模拟信号输出**：连接耳机、放大器或扬声器
* **存储媒体**：如 microSD 卡，可通过录音写入音频文件
* **Wi-Fi 接口**：将音频数据流发送到互联网
* **蓝牙接口**：将音频数据流传输到蓝牙耳机等设备
* **I2S 接口**：将数据流传输到编解码器芯片
* **以太网接口**：将音频数据流传输到互联网
* **芯片内部 flash**：存储录音
* **用户交互**：如显示器、LED 或 `振动反馈 <https://en.wikipedia.org/wiki/Haptic_technology>`_

**主处理器：**

微控制器或计算机，可从输入读取数据、处理数据（例如编码/编码）、输出数据。


选择项目类型
================

ESP 系列芯片（包括 ESP32、ESP32-S2、ESP32-S3 等） 具有上述所有功能，或者说能够支持这些功能（如驱动以太网 PHY）。鉴于 ESP 芯片的成本较低，以及可免费使用的 ESP-ADF 软件开发平台，我们能够以极低的价格开发具有最少附加组件的音频项目。

基于应用程序、所需的功能和性能，我们可以考虑以下两种项目类型。

* **基础项目**：具有最少的附加组件，前提是使用板载的 I2S 、PDM 接口或 DAC，且不需要输出特别高质量的音频。
* **典型项目**：带有外部编解码器芯片和功率放大器，可输出高质量音频，提供多个输入/输出选项。

通过添加或删除上述项目的功能/组件，可以开发出其他不同的项目，示例请见下文。


基础项目
================

ESP 芯片拥有多个外设，可借助 I2S、PDM 或 DAC 接口可开发出一个基础项目。我们可以通过数字麦克风输入语音信号，构建一个可以与云服务通信的语音命令控制的基础项目。

.. figure:: ../../_static/audio-project-minimum-voice-service.jpg
    :alt: 音频项目示例 - 向云服务发送语音命令
    :figclass: align-center

    音频项目示例 - 向云服务发送语音命令

如果可接受 8 位的数据输出，我们可使用两个板载 DAC 实现另一个基础项目，播放联网广播节目。

.. figure:: ../../_static/audio-project-minimum-internet-radio.jpg
    :alt: 音频项目示例 - 联网广播播放器
    :figclass: align-center

    音频项目示例 - 联网广播播放器


典型项目
================

如果需要更好的音频质量和更多的接口选项，可使用外部 I2S 编解码器来完成所有模拟输入和输出信号的处理。不同类型的编解码器芯片可提供不同的额外功能，如音频输入信号前置放大器、耳机输出放大器、多个模拟输入和输出、音效处理等。`I2S <http://iot-bits.com/wp-content /uploads/2017/06/I2SBUS.pdf>`_ 是音频编解码器芯片接口的行业标准，通常用于高速、连续传输音频数据。为了优化音频数据处理的性能，可能需要额外的内存。对于这种情况，请考虑使用集成 8 MB PSRAM 和 ESP32 芯片的 `ESP32-WROVER-E <https://www.espressif.com/sites/default/files/documentation/esp32-wrover-e_esp32-wrover-ie_datasheet_cn.pdf>`_ 模组。

.. figure:: ../../_static/audio-project-typical-example.jpg
    :alt: 典型音频项目示例
    :figclass: align-center

    典型音频项目示例

ESP-ADF 主要支持使用编解码器芯片的项目，如 :doc:`ESP32 LyraT <../get-started/get-started-esp32-lyrat>` 开发板与软件之间的交互由音频 HAL 和驱动程序完成，开发板使用的编解码芯片是 `ES8388 <http://www.everest-semi.com/pdf/ES8388%20DS.pdf>`_。可以通过提供不同的驱动程序来支持具有不同编解码器芯片的开发板。