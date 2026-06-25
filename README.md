# 基于实际工程的无感 FOC 教学页

这是一个面向学习和调试的无感 FOC 教学网页，内容基于瑞萨 RA6T2 平台上的 FOC 无感控制工程整理而来。网页不是通用课件，而是把工程里的快环时序、相电流计算、坐标变换、滑模观测器、启动状态机、闭环切换和调参流程拆开讲清楚。

在线访问：

https://zzloop14.github.io/sensorless-foc-tutorial/

## 项目内容

网页采用左侧目录切换章节的方式组织内容，避免一路滚动到底。当前包含 9 个章节：

1. 总览  
   通过可交互总流程框图建立整体认知，点击流程图模块可以跳转到对应章节。

2. 20 kHz 执行链  
   说明 ADC 中断、相电流重构、Clarke/Park、SMO、FOC/PID、SVPWM 在 50 us 快环中的执行顺序。

3. 耗时实测  
   介绍 GPIO 示波器法、GPT 计数法、DWT 周期计数法，以及为什么不能在快环里直接串口打印。

4. 坐标变换  
   用交互滑块展示 `abc -> alpha/beta -> d/q` 的关系，并同步显示三相电流平衡和 `Id/Iq` 投影结果。

5. 滑模观测器  
   梳理电机模型离散化、SMO 变量来源、`K/Smax` 参数影响、`z` 输出、低通滤波、反电势估计和角度计算。

6. 启动与切环  
   展示预充电、两次预定位、开环强拖、切闭环判断、角度校正和速度环接管的状态机流程。

7. 工程文件  
   按学习顺序说明关键文件职责，包括 `m_coordinate.c`、`m_observer.c`、`m_rotor_angle.c`、`m_foc.c` 和 `m_svpwm.c`。

8. 调参与台架  
   给出台架搭建、观测器初调、切闭环调试和速度环调试的建议顺序。

9. 自测  
   提供约 20 道单选题，覆盖每个模块和综合故障判断。

## 主要特性

- 单文件静态网页，直接由 GitHub Pages 托管。
- 总流程图支持模块点击跳转。
- 坐标变换、SMO 参数、启动流程等内容包含交互图表。
- 图文结合讲解无感 FOC 的信号链路、控制链路和调参路径。
- 内容与实际工程变量、函数名和参数关联，便于从网页回到代码阅读。

## 仓库结构

```text
sensorless-foc-tutorial/
  index.html
  assets/
    foc-hero.png
    sensorless-foc-flowchart.png
  README.md
```

## 本地预览

这个项目是纯静态网页，不需要安装依赖。

直接双击 `index.html` 即可打开；也可以在仓库目录启动一个简单本地服务：

```powershell
cd F:\FOC_WorkSpace\sensorless-foc-tutorial
python -m http.server 8000
```

然后在浏览器访问：

```text
http://localhost:8000
```

## 更新网页

如果你在本地修改了 `index.html` 或 `assets/` 中的图片，可以按下面流程提交并推送：

```powershell
cd F:\FOC_WorkSpace\sensorless-foc-tutorial
git status
git add .
git commit -m "Update tutorial content"
git push
```

推送完成后，GitHub Pages 通常会在几十秒到几分钟内自动更新。

## 说明

本仓库只包含教学网页，不包含完整电机控制固件工程。网页中的函数名、参数名和调试流程来自原始无感 FOC 工程，用于学习算法流程和调试方法。
