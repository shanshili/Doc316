## RC有源滤波器

有源滤波器：

+ 优点：不使用电感，体积小；可放大信号且倍数易调节；可加入电压串联负反馈，是输入电阻高，输出电阻低，输入输出之间有良好的隔离。
+ 缺点：可靠性差；不宜用于高频；不宜在高电压、大电流下使用；需外接电源。

### 一阶低通有源滤波器 - VCVS压控电压源电路

一种同相输入，产生正向增益的低阶滤波器，通过负反馈网络形成一个增益可控的VCVS。从一阶VCVS说起：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200424100311852.png#pic_center)

+ 输入电压先经过低通滤波器滤波，后输入至同相比例放大电路的同相端；

+ 同相比例放大电路由R1、Rf、放大器组成。同相比例放大器输入阻抗高，输出阻抗低，性能稳定，增益容易调节。
  
  $$
\begin{aligned}
&\text{传递函数}\qquad &&A(s)=\frac{V_o(s)}{V_i(s)}=\dot{A}_u\cdot A_0=\frac{A_0}{1+j\omega/\omega_n}\\
&\text{RC滤波器幅频函数}\qquad &&\dot{A_u}=\frac{\dot{U_c}}{\dot{U_i}}=\frac{1}{1+j\omega RC}\\
&\text{放大器增益}\qquad &&A_0=\frac{R_1+R_f}{R_1}\\
&\text{特征角频率}\qquad &&\omega_0=\frac{1}{RC}\\
&\text{幅频响应}\qquad &&|A(j\omega)|=\frac{A_0}{\sqrt{1+(\omega/\omega_0)^2}}
\end{aligned}
  $$

+ 

### 一阶高通有源滤波器

将低通滤波器的前置低通RC电路替换为高通。

$$
\text{传递函数}\qquad A(s)=\frac{1}{1+\omega_n/s}
$$


### 二阶有源滤波器

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200424100245976.png#pic_center)


+ 对于低通，Y1、Y2为电阻R1、R2；Y3、Y4为电容C1、C2（公式推导以低通为例）。

+ 二阶有源滤波在转折频率处性能不佳，因此引入一定正反馈Y3可改善。

+ R3、R4、放大器组成同相比例放大器。
  
  $$
  \begin{aligned}
  \text{传递函数}\qquad A(s)=\frac{V_o(s)}{V_i(s)}&=\frac{U_2(s)}{U_1(s)}=\frac{U_b(s)}{U_1(s)}\cdot\frac{U_2(s)}{U_b(s)}\\&=\dot{A}_u\cdot A_0\\
  &=\frac{A_0Y_1Y_2}{Y_3Y_4+(1-A_0)Y_2Y_3+Y_2Y_4+Y_1Y_2+Y_1Y_4}\\
  &=\frac{A_0}{R_1R_2C_1C_2s^2+[R_2C_2+R_1C_2+R_1C_1(1-A)]s+1}\\
  &=\frac{A_{\omega_0}^2}{s^2+\omega_0/Q\cdot s+{\omega_0}^2}
  \end{aligned}
  $$
 
  $$
  \text{a,b处KCL方程} \qquad
  \begin{aligned}
  &\begin{cases}
      \frac{U_1-U_a}{Y_1}-\frac{U_a-U_b}{Y_2}=\frac{U_a-U_2}{Y_3} \\
      U_a(s)\cdot\frac{Y_4}{Y_2+Y_4}=U_b(s)
  \end{cases}
  \end{aligned}
  $$
  
  $$
  \begin{aligned}
  &\text{放大器增益}\qquad &&A_0=\frac{U_2(s)}{U_b(s)}=\frac{R_3+R_4}{R_3}\\
  &\text{特征角频率}\qquad &&{\omega_0}^2=\frac{1}{R_1R_2C_1C_2}\\
  &\text{品质因数}\qquad &&Q=\frac{1}{3-A_0}\\
  &\text{相频响应}\qquad &&\varphi(\omega)=-arctg\frac{\omega/(\omega_0Q)}{1-(\omega/\omega_0)^2}
  \end{aligned}
  $$

+ $A_0<3$ 时，滤波电路才能稳定工作，$A_0\geqq 3$时，滤波器自激

![img](https://imgconvert.csdnimg.cn/aHR0cDovL3AxLnBzdGF0cC5jb20vbGFyZ2UvcGdjLWltYWdlLzVlY2JkYzhkMWYxMzRlYThhMDQwOGE1MzA5YzYyMWRj?x-oss-process=image/format,png)

### 总结

![img](https://imgconvert.csdnimg.cn/aHR0cDovL3AxLnBzdGF0cC5jb20vbGFyZ2UvcGdjLWltYWdlL2VhODU5NzdlYTZlZTQwODU4MDQ5ZjFkNzU2NTE0ODlh?x-oss-process=image/format,png)

#### *参考文献：*

+ 牛燕炜. 有源低通滤波器的设计与仿真分析[J]. 现代电子技术, No.251(12):181-183.
+ 王龙, 贾瑞皋, 陈洪海. VCVS有源滤波器的设计及Matlab辅助仿真分析[J]. 测井技术, 2005(06):95-99.
+ 滤波器基本概念分类 - https://mbb.eet-china.com/forum/topic/75523_1_1.html
+ 低通、高通、带通、带阻、状态可调滤波器 - https://mbb.eet-china.com/forum/topic/76881_1_1.html
