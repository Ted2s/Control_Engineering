# 제어공학1-3장 과제
------------
## P3.1

### 문제
<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/d7893625-d197-49d7-abb3-43c42bb6b58d"  width="500" height="400">

### 문제 풀이

(a) 상태 변수로 표현된 1차 미분 방정식을 구하기 위해서, 적당한 상태변수는 $x_1(t)=$변위 와 $x_2(t)=$속도로 설정한다. 

(b) 상태 변수로 1차 미분 방정식을 구현하면, 

$$x_1(t)=y(t) $$

$$x_2(t)=\frac{y(t)}{dt}$$

이 되고, 질량, 마찰력, 스프링의 탄성에 대한 운동 방정식을 작성하게 되면 

$$M\frac{\mathrm{d^2}y(t) }{\mathrm{d} t^2}+b\frac{\mathrm{d}y(t) }{\mathrm{d} t}+ky(x)=r(t)$$

이 된다.

(c) 상태 미분 방정식은 변위를 미분하면 속도가 되기 때문에, 이를 식으로 나타내면


$$x_2(t)=\frac{y(t)}{dt}=\frac{dx_1(t)}{dt}$$ 이고, 

$$\frac{dx_2(t)}{dt}=-\frac{b}{m}x_2(t)+\frac{k}{m}x_1(t)+\frac{1}{M}r(t)$$ 이 된다.



## P3.3
### 문제
<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/2ffb10e4-a4e2-4c72-b09c-98dc62a1da28" height="400">

### 문제 풀이

우선 상태변수는

$$x_1(t)=i_L(t), x_2(t)=V_c(t) $$

이고,

KCL과 KVL을 이용해서 RLC회로를 해석하게 되면, 


$$C\frac{dV_c}{dt}=i_R-i_L$$

$$R*i_R=V_2-V_c$$

가 된다. 이를 식을 정리하면, 

$$\frac{dx_2(t)}{dt}=\frac{V_2}{RC}-\frac{x_2(t)}{RC}-\frac{x_1(t)}{R}$$

$$\frac{dx_1(t)}{dt}=\frac{V_1}{L}-\frac{V_2}{L}+\frac{x_2(t)}{L}$$

이고, 이를 행렬로 정리하면, 

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/4d8c8b6f-23c4-44b7-b35e-d3e0b41902b1"  width="400" height="180">

이 된다.




## P3.5
### 문제 

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/86fec3b2-836d-4d8e-bd3b-a38921e8e74a"  width="500" height="300">

### 문제 풀이

(a) 폐루프의 전달 함수는 구하게 되면, 한번 반환 되는 부분을 잘 생각해야한다. 이를 통해 식을 세우면, 

$$T(s)=\frac{Y(s)}{R(s)}=\frac{G(s)}{1+G(s)}=\frac{\frac{s+2}{s^3+5s^2-24s}}{1+\frac{s+2}{s^3+5s^2-24s}}=\frac{s+2}{s^3+5s^2-23s+2}$$

가 된다.

(b) 이를 통해 상태모델과 phase variable form으로 작성하면, 

$$A=
\begin{bmatrix}
0&1&0 \\\\
0&0&1 \\\\
-2&23&-5
\end{bmatrix}$$

$$B=
\begin{bmatrix}
0\\\
0\\\
1
\end{bmatrix}$$

$$C=
\begin{bmatrix}
2&1&0
\end{bmatrix}$$

이므로, 


<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/cb0a930e-a39b-4883-bb53-6ed1d3079ec8"  width="500" height="300">

가 된다.


## P3.12
<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/6ac88ad8-6114-4ff4-a3b2-e0a96971d5e3"  width="500" height="250">

(a) 상태 공간 모델을 구하게 되면, 

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/43e21e1b-64b9-4ee5-a103-43cb810784c5"  width="500" height="300">

가 된다.

(b) 상태 천이 행렬을 구하는 식은

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/2e6ffa63-0b6a-433f-ae1f-01cfe774ff71"  width="500" height="300">

이다. 여기서 매트랩을 사용하여, 

```
syms s t
SI=[s -1 0; 0 s -1; 48 44 s+12]
PS=SI^-1
PT = ilaplace(PS);
PT
```
결과값을 출력하게 되면, 

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/5aaafe03-3ab4-49c3-af0a-2e5456191047"  width="500" height="700">

가 된다.


## P3.17
<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/2f8f62d6-1e0e-45ea-b332-1eeb22bcfa22"  width="500" height="250">

우선 이 상태 변수 방정식을 전달 함수로 변환하기 위한 식을 구하면, 

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/c9ccd5ac-e9a4-4725-9e15-dbf7187f4000"  width="500" height="700">

같은 형식이 된다. 하지만 매트랩으로 구하면 더 쉽게 구할수가 있는데, ss2tf 식을 사용해서 상태 방정식을 전달 함수로 변한해 줄 수 있다.

```
A=[1 1 -1; 4 3 0; -2 1 10]
B=[0;0;4]
C=[1 0 0]
[n,d]=ss2tf(A,B,C,D)
mySys_tf=tf(n,d)
```

이를 통한 출력값은 

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/65b106e3-576e-4a6f-b4f1-d1c725db8e12"  width="500" height="700">

다음과 같다. 
