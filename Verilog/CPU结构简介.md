### CPU结构简介

该CPU设计如下：

 1. 存在三条总线，#A、#B两条用来提供计算输入/寄存器输出，#C用来提供计算输出/寄存器输入；

 2. 共有16个寄存器，其中#0到#11作为通用寄存器。#12被称作IOAD，#13被称作IOC，#14被称作Timer，#15被称作PC。寄存器会从#C上获取数据，会将数据输出到#A或#B上。

    (1) IOC是输入输出控制模块，该模块被封装为寄存器，其行为对于CPU而言与普通寄存器相同，用来对不同IO进行管理。

    (2) IOAD用来区分当前选中的IO模块，具体而言，IOAD低四位用来指示可能存在的IO内部寄存器地址，其它高位用来指示当前选中的IO。

    (3) Timer是定时器寄存器，寄存器中的值会不断自增，从0开始自增256次后到下一次0所用时间需要0.99999289s，同1s比误差小于1e-5。是在不使用中断时感知时间的一种手段。

    (4) PC是程序计数器。

 3. RAM、ROM使用Tang上的BSRAM实现。指令存在ROM中，定长32bit；

 4. ALU以及COND负责计算以及条件判断，会从#A和#B获取数据，其中ALU把计算结果输出到#C。