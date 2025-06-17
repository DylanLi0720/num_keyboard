# 为瀚文键盘增加一块数字小键盘

## 声明

本项目是在瀚文的SDK上进行的二次开发，属于个人项目，未经允许，任何人不能用于任何公用或商业用途。

## 前言

由于全键盘的尺寸较大，PCB与外壳加工成本较高，而数字键盘的PCB和外壳尺寸可以控制在10cm×10cm以内，成本不高，所以非常适合客制化或者diy玩家。

## 结构简介
- 01 hardware_numKeyboard文件夹是键盘的硬件电路文档
- 02 software_numKeyboard文件夹是键盘的软件文档，使用CMake构建工程
- 03 2D_model文件夹是定位板与底座的加工文件
- 04 Docs 文件夹是相关芯片的数据手册

## 开发环境

使用CLion + STM32cubeMX，在windows上开发。开发工具包括minGW、CMake、OpenOCD等等。

## 硬件说明

- 这是一个嵌入式软件项目,PCB设计使用的是立创eda工具。
- 下载工具使用jlink，采用SWD协议下载。
- 该数字键盘为单模键盘，即只有USB连接方式，使用USB进行供电。

## 软件说明
- HID报文描述符的数组。它规定了上传时报文的格式，这里定义的是通用桌面的用法，更详细的用途是作为键盘来使用。如果想要自定义输入功能则需要修改这一部分，例如增加鼠标功能、多媒体功能或者摇杆功能等等。
- 修改键盘配列。也就是按键的映射顺序。比如第零个按键的功能是锁定功能、第一个按键功能是除法功能，更具体的映射关系在remap函数中实现。需要注意的一点是的IO_NUMBER是8的整数倍，那么这里每层数组都需要把剩下的内容填满，不能保留为0。
- RGB灯效。使用一个t变量作为形参，遍历RGB三维空间的像素点。
- 圆形屏幕。可以显示自己喜欢的图片，思路来源于[承载我所有幻想的键盘](https://oshwhub.com/ran-pang/multifunctional-keyboard)，可以升级为旋钮屏。

## 功能说明
- 全键无冲
- USB2.0扩展，可以接入各类USB设备，如2.4G接收器、U盘等等
- TFT屏幕，主控芯片的flash大小为128KB，大约能存储一张图片，资源较为紧张。若需要渲染LVGL的控件则需要升级成更高容量的主控芯片
- 集成了触摸芯片，可以触摸输入，功能自行修改

## 参考
- [HelloWord-Keyboard](https://github.com/peng-zhihui/HelloWord-Keyboard)
- [瀚文键盘的嘉立创工程](https://oshwhub.com/pengzhihui/b11afae464c54a3e8d0f77e1f92dc7b7)
- [基于HS8836A的USB扩展坞](https://oshwhub.com/xx1111/usb-hid-8836)
- [承载我所有幻想的键盘](https://oshwhub.com/ran-pang/multifunctional-keyboard)