*让我们先掌握（复习）最基本的电路概念，包括RLC的拉式（傅里叶）变换，系统函数$H(\omega)$等...大部分资源来源于网络，本篇文章作为一个整理，欢迎大家纠错和补充。接下来会更新有源滤波器和数字滤波器等。之所以发到CSDN主要是对于md和latex有相对比较好的支持。*

# RLC无源滤波器

由RLC网络构成。带负载能力差，无放大作用，特性不理想，边沿不陡。

$$
H(s)=\frac{Y(s)}{X(s)}=\dot{A_u}=\frac{\dot{U_o}}{\dot{U_i}}
$$

## MatLab相关函数

+ freqs(b,a,w) - 求得$H(s)=\frac{B(s)}{A(s)}$，但相位单位为°;
+ bode(tf) - 得出Bode图，需要tf(b,a)处理参数。

## RLC变换

+ $R \leftrightarrow R$
+ $C \leftrightarrow \frac{1}{j\omega C}$
+ $L \leftrightarrow j\omega L$
+ $s \leftrightarrow j\omega$

## 一阶RC低通滤波器

![](https://img-blog.csdnimg.cn/20200412110131638.png#pic_center)

$$
\dot{A_u}=\frac{\dot{U_c}}{\dot{U_i}}=\frac{1}{1+j\omega RC}\\
f_H=\frac{1}{2\pi RC}=\frac{1}{\sqrt2}\dot{A_u};f=\frac{\omega}{2\pi}\\
\dot{A_u}=\frac{1}{1+jf/f_H}
$$

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412110211367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1dhbmdsZV8w,size_16,color_FFFFFF,t_70#pic_center)

$f=f_H$时，相角滞后45°，放大倍数幅值约降到0.707倍

+ 一阶RC高通滤波器

  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412110225941.png#pic_center)

$$
\dot{A_u}=\frac{\dot{U_r}}{\dot{U_i}}=\frac{j\omega RC}{1+j\omega RC}\\
f_L=\frac{1}{2\pi RC}=\frac{1}{\sqrt2}\dot{A_u};f=\frac{\omega}{2\pi}\\
\dot{A_u}=\frac{jf/f_L}{1+jf/f_L}
$$

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412110237447.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1dhbmdsZV8w,size_16,color_FFFFFF,t_70#pic_center)

$f=f_L $时，相角超前45°，放大倍数幅值约降到0.707倍

## RC带通滤波器 - 看做低通与高通的串联

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412110251817.png#pic_center)

$$
H(j\omega)=\frac{\dot{U_o}}{\dot{U_i}}=\frac{1}{3-j(f_0/f-f/f_0)}
$$

##RC带阻滤波器

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412110302139.png#pic_center)

## 二阶RC低通滤波器

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412110333902.png#pic_center)

$$
H(j\omega)=\frac{\dot{U_o}}{\dot{U_i}}
=\frac{\frac{1}{j\omega C}//(R+\frac{1}{j\omega C})}{R+\frac{1}{j\omega C}//(R+\frac{1}{j\omega C})
}\cdot\frac{\frac{1}{j\omega C}}{\frac{1}{j\omega C}+R}\\
=\frac{1}{1+3j(f/f_0)-(f/f_0)^2}
$$

$f_0$为截止频率，通过所需的截止频率可推算出RC值。

## 二阶RC高通滤波器

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412110426567.png#pic_center)

$$
H(j\omega)=\frac{\dot{U_o}}{\dot{U_i}}
=\frac{\dot{U_i}\cdot\frac{R//(\frac{1}{J\omega c}+R)}{\frac{1}{j\omega C}+R//(\frac{1}{J\omega c}+R)
}\cdot\frac{R}{R+\frac{1}{j\omega C}}}{\dot{U_i}}\\
=\frac{R//(\frac{1}{J\omega c}+R)}{\frac{1}{j\omega C}+R//(\frac{1}{J\omega c}+R)}\cdot\frac{R}{R+\frac{1}{j\omega C}}\\
=\frac{1}{1-(f_0/f)^2-j3(f_0/f)}
$$

## 电感滤波电路

由于电感有自感效应，当通过电流时，电感两端会产生电动势来阻值电流的变化，因而能够起到起到滤波作用。随着电流的增加，一部分将储存在电感当中使电流缓慢增加；与此同时，当电流减小的时候，反向电动势又反过来阻碍它的减小，最终的结果是得到比较平滑的直流电，同时它的外特性也比较硬，因此适用于大电流的负载。

## π型RC滤波电路

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412110408586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1dhbmdsZV8w,size_16,color_FFFFFF,t_70#pic_center)

+ C1可将大部分交流成分滤除，增大C1可提高效果，但充电时间会增长，充电电流随之增大，可能会损坏整流二极管，所以一般用比较小的C1与后续RC配合即可；

+ 增大R1、C2都可以提高滤波效果，但注意R1会产生压降，使输出电压降低

## π型LC滤波电路

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200412110357561.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1dhbmdsZV8w,size_16,color_FFFFFF,t_70#pic_center)

+ 由前置滤波C1与倒L滤波电路（L1、C2）组成；

+ **L对对交流电感抗大**，但相较于R不会降低输出电压。
+ 对于倒L型电路，LC乘积越大滤波效果越好。

| 滤波类型  | 滤波电路特点             | 对整流二极管冲击 | 带负载能力 | 应用                     |
| --------- | ------------------------ | :--------------: | :--------: | :----------------------- |
| 电容滤波  | 电路简单，外特性比较软   |        大        |     差     | 小电流、负载电流变化不大 |
| 电感滤波  | 电感笨重成本高，外特性硬 |        小        |     强     | 大电流负载               |
| 倒L滤波   | 电感笨重成本高，外特性硬 |        小        |     强     | 大电流负载，效果强于上面 |
| LCπ型滤波 | 电感笨重成本高，外特性硬 |        大        |     差     | 大电流负载，效果强于上面 |
| RCπ型滤波 | 常用，外特性比较软       |        大        |    最差    | 小电流、负载电流变化不大 |

### 参考文献

+ 滤波器基本概念分类 - https://mbb.eet-china.com/forum/topic/75523_1_1.html
+ 各种形式滤波电路的分析 - https://mbb.eet-china.com/forum/topic/75740_1_1.html

