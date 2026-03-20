# Lab 1：MATLAB Programming

## 小组信息

- **姓名①**: 谢宏波
- **学号①**: 12410724
- **姓名②**: 杨耀淇
- **学号②**: 12413303

## 实验目标概括：

### 1.4(a) 实验目标

本实验旨在通过构造特定输入信号，验证系统  
$$
y[n] = \sin\left(\frac{\pi}{2}x[n]\right)
$$
是否满足线性性质。通过选取两个输入信号 $x_1[n]$ 和 $x_2[n]$，并分别计算系统对单独输入及其叠加输入的响应，对比是否满足叠加性原则，从而判断该系统是否为线性系统。


### 1.4(b) 实验目标

本实验旨在分析系统  
$$
y[n] = x[n] + x[n+1]
$$
的因果性。通过选取单位阶跃信号作为输入，观察输出在某一时刻是否依赖未来输入值，从而判断该系统是否满足因果性条件，并加深对因果系统定义的理解。


### 1.4(c) 实验目标

本实验旨在研究系统  
$$
y[n] = \log(x[n])
$$
的稳定性。通过构造一个有界输入信号，并观察其对应输出是否仍然有界，从而验证该系统是否满足 BIBO 稳定性条件，并理解稳定系统的基本判定方法。


### 1.4(d) 实验目标

本实验旨在分析系统
$$
y[n] = \sin\left(\frac{\pi}{2}x[n]\right)
$$
的可逆性。通过寻找不同输入产生相同输出的情况，验证系统是否能够从输出唯一确定输入，从而判断该系统是否为可逆系统。


## 具体实验内容：

## 1.4(a)

### 题目

证明系统
$$
y[n] = \sin\left(\frac{\pi}{2}x[n]\right)
$$
不是线性的。已知输入信号：
$$
x_1[n] = \delta[n], \quad x_2[n] = 2\delta[n]
$$


### 程序

```matlab
clc; clear; close all;

n = -4:4;

x1 = [0 0 0 0 1 0 0 0 0];
x2 = [0 0 0 0 2 0 0 0 0];
x3 = x1 + x2;

y1 = sin((pi/2) .* x1);
y2 = sin((pi/2) .* x2);
y3 = sin((pi/2) .* x3);

figure;

subplot(2,1,1);
stem(n, y1 + y2, 'k', 'filled');
xlabel('n');
ylabel('Amplitude');
title('y1+y2');
grid on;

subplot(2,1,2);
stem(n, y3, 'r', 'filled');
xlabel('n');
ylabel('Amplitude');
title('y3');
grid on;
```

### 实验结果图

![Figure: Comparison between y1+y2 and y3](https://github.com/Kranceeee/CS307_Principles_of_Database_System_Project1/blob/main/1.4a.png?raw=true)

### 分析：由于 y1+y2≠y3，故不满足线性。

## 1.4(b)

### 题目

证明系统  
$$
y[n] = x[n] + x[n+1]
$$
不是因果系统。已知输入信号：
$$
x[n] = u[n]
$$

### 程序

```matlab
clc; clear; close all;

n = -5:9;

x = [0 0 0 0 0 1 1 1 1 1 1 1 1 1 1];
y = [0 0 0 0 0 1 2 2 2 2 2 2 2 2 2 2];

figure;

subplot(2,1,1);
stem(n, x, 'k', 'filled');
xlabel('n');
ylabel('Amplitude');
title('x[n]');
grid on;

subplot(2,1,2);
stem(n, y, 'r', 'filled');
xlabel('n');
ylabel('Amplitude');
title('y[n]');
grid on;
```

### 实验结果图

![Figure: ](https://github.com/Kranceeee/CS307_Principles_of_Database_System_Project1/blob/main/1.4b.png?raw=true)

### 分析：由于 y[0]的值与 x[1]的值有关，故不满足因果关系的要求。

## 1.4(c)

### 题目

证明系统  
$$
y[n] = \log(x[n])
$$
不是稳定系统。

### 程序

```matlab
clc,clear,close all

n=0:50;
x=0.1*n;
y=log(x);

figure;
stem(n,x,'r')
xlabel('n');ylabel('x[n]'),legend('x[n]=0.1n'); grid on

figure;
stem(x,y)
xlim([-5 5]);
grid on;xlabel('x[n]');ylabel('log(x[n])'),legend('y[n]=log(x[n])')
```

### 实验结果图

![Figure: ](https://github.com/Kranceeee/CS307_Principles_of_Database_System_Project1/blob/main/1.4c_1.png?raw=true)

![Figure: ](https://github.com/Kranceeee/CS307_Principles_of_Database_System_Project1/blob/main/1.4c_2.png?raw=true)

### 分析： x[n]从正方向接近 0 时，y[n]趋于负无穷，没有下界。故系统为不稳定系统。

## 1.4(d)

### 题目

证明系统  
$$
y[n] = \sin\left(\frac{\pi}{2}x[n]\right)
$$
不是可逆系统。


### 程序

```matlab
clc,clear,close all

n=-4:1:4;

x1 = 1 .* (n >= 0);
x2 = 5 .* (n >= 0);

y1=sin((pi/2).*x1);
y2=sin((pi/2).*x2);

figure;
subplot(2,1,1);
stem(n,y1,'k','filled');
xlabel('n');
ylabel('y[n]');
legend('y1');
title('figure1');

subplot(2,1,2);
stem(n,y2,'r','filled');
xlabel('n');
ylabel('y[n]');
legend('y2');
title('figure2');

```

### 实验结果图

![Figure: ](https://github.com/Kranceeee/CS307_Principles_of_Database_System_Project1/blob/main/1.4d.png?raw=true)

### 分析：由于 y1=y2，系统不是 1 对 1 的，由输出信号无法确认输入信号。故系统不可逆。

## 1.5(a)

### 题目

已知一阶自回归方程
$$
y[n] = ay[n-1] + x[n]
$$
编写函数
```matlab
function y = diffeqn(a,x,yn1)
```
用来计算该系统的输出，其中输入向量 `x` 表示 $x[n]$，`yn1` 表示 $y[-1]$。


### 程序

```matlab
function y=diffeqn(a,x,yn1)
y=a*yn1+x(1);
l=length(x);
for i=2:l
    y=[y,a*y(end)+x(i)];
end
end
```


## 1.5(b)

### 题目

取  
$$
a=1,\quad y[-1]=0
$$
在区间  
$$
0 \le n \le 30
$$
上，分别取输入
$$
x_1[n]=\delta[n],\quad x_2[n]=u[n]
$$
利用 1.5(a) 中编写的函数求出对应输出，并用 `stem` 作图。


### 程序

```matlab
clc,clear,close all

n=0:30;

x1=[1 zeros(1,30)];
x2=ones(1,31);

y1=diffeqn(1,x1,0);
y2=diffeqn(1,x2,0);

figure;
stem(n,y1,'k')
ylim([0,5]);grid on;xlabel('n');ylabel('y[n]');legend('y1[n]');

figure;
stem(n,y2, 'r')
grid on;xlabel('n');ylabel('y[n]');legend('y2[n]');

```

> function y=diffeqn(a,x,yn1)
y=a*yn1+x(1);
l=length(x);
for i=2:l
y=[y,a*y(end)+x(i)];
end
end

### 实验结果图

![Figure: ](https://github.com/Kranceeee/CS307_Principles_of_Database_System_Project1/blob/main/1.5b1.png?raw=true)

![Figure: ](https://github.com/Kranceeee/CS307_Principles_of_Database_System_Project1/blob/main/1.5b2.png?raw=true)

### 分析：左方为 x1[n] =δ[n]对应图像，右方为 x2[n] = u[n]对应图像

## 1.5(c)

### 题目

再取  
$$
a=1,\quad y[-1]=-1
$$
在区间  
$$
0 \le n \le 30
$$
上，分别取输入
$$
x_1[n]=u[n],\quad x_2[n]=2u[n]
$$
定义对应输出为 $y_1[n]$ 和 $y_2[n]$。  
利用 `stem` 作出 $y_1[n]$、$y_2[n]$ 以及
$$
2y_1[n]-y_2[n]
$$
的图像，并说明为什么该差值不恒为 0。


### 程序

```matlab
clc,clear,close all

n=0:30;
x1=(n>=0);
x2=2*(n>=0);

y1=diffeqn(1,x1,-1);
y2=diffeqn(1,x2,-1);
y3=2*y1-y2;

figure;
subplot(3,1,1);
stem(n,y1,'r')
grid on;xlabel('n');ylabel('y[n]');legend('y1[n]');

subplot(3,1,2);
stem(n,y2)
grid on;xlabel('n');ylabel('y[n]');legend('y2[n]');

subplot(3,1,3);
stem(n,y3,'g')
ylim([-5,0]);grid on;xlabel('n');ylabel('y[n]');legend('2y1[n]-y2[n]');
```

> function y=diffeqn(a,x,yn1)
y=a*yn1+x(1);
l=length(x);
for i=2:l
y=[y,a*y(end)+x(i)];
end
end

### 实验结果图

![Figure: ](https://github.com/Kranceeee/CS307_Principles_of_Database_System_Project1/blob/main/1.5c.png?raw=true)

### 分析：由于 2y1[n]-y2[n]=2*(-1+x1[0]+x1[1]+……+x1[n])-(-1+x2[0]+x2[1]+……+x2[n]) ，x2[n]=x1[n]。故 2y1[n] – y2[n]=-1。与图像吻合。

## 经验总结

 通过本次 MATLAB 实验，我对离散时间系统的基本性质（线性、因果性、稳定性和可逆性）有了更加直观的理解。以前在课上主要是通过公式和理论来判断，这次通过编程和画图，把这些性质具体表现出来，对理解帮助很大。

在 1.4 部分中，我学会了如何通过构造简单的输入信号（如冲激信号和阶跃信号）来验证系统的性质。例如，通过比较 $y_1 + y_2$ 和 $y_3$ 判断线性，通过观察是否使用未来输入判断因果性，这些方法都比较清晰直接。同时，在做稳定性分析时，通过观察对数函数在接近 0 时的发散情况，加深了对 BIBO 稳定性的理解。

在 1.5 部分中，我第一次自己实现了差分方程函数 `diffeqn`，体会到了递推计算的过程。通过改变初始条件和输入信号，观察输出的变化，也让我更好地理解了系统的动态特性。尤其是在 1.5(c) 中，发现 $2y_1[n] - y_2[n]$ 不为 0，并通过推导验证结果，与图像一致，这一过程让我对理论和实验之间的联系有了更深的认识。

在编程过程中，也遇到了一些问题，比如最开始使用 `Step` 和 `Impulse` 函数时报错，后来通过直接构造数组或使用逻辑表达式（如 $(n \ge 0)$）解决了问题。这也让我意识到，写代码时尽量减少对额外函数的依赖会更加稳妥。

总体来说，这次实验不仅提高了我使用 MATLAB 进行信号处理的能力，也加深了我对课程内容的理解，为后续学习打下了基础。

## 自我评分
##### 姓名①：
##### 姓名②：
