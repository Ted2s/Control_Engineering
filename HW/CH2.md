# 제어공학1-2장 과제
------------
## P2.7
그림 P2.7과 같이 1차 저역통과 필터로 구현한 적분 증폭기 회로의 전달함수를 구하라.

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/b524d9ab-d903-4eef-ba1f-98aa91b76561"  width="600" height="400">

### 문제풀이
1차 저역 필터로 증폭된 출력 전압은

$$V_2(s) = -\frac{Z_2(s)}{Z_1(s)}V_1(s)$$

이고, 여기서 $Z_1=R, Z_2=\frac{1}{C_s}$ 이므로 

$$V_2(s) = -\frac{1}{RC_s)}V_1(s)$$

그러므로  전달함수는

$$G(s)=\frac{V_2(s)}{V_1(s)}=-\frac{1}{RC_s}$$

가 된다.


## P2.12
그림 P2.12에 주어진 블록선도로 표현된 개루프 제어 시스템에 대해, t $\to \infty$ 일때 단위계단 입력 r(t)에 대한 응답 y(t) $\to$ 1이 되도록 K값을 정하라. 초기조건은 영이라고 가정한다.

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/aa22e8f6-8d7e-484a-a52d-8c57fddcc2c2"  width="600" height="400">

### 문제풀이

블록선도를 등가선도로 표현해보면

$$R(s) \to \frac{k}{s+50} \to Y(s)$$

라고 할수 있다. 또한 단위 계단 입력이기 때문에 r(t)의 라플라스 변환은 $\frac {1}{s}$이다. 또한 부분분수분해를 통해 식을 전개한다.

$$R(s)=\frac{1}{s} \to \frac{Y(s)}{R(s)}=\frac{k}{s+50} \to Y(s)=\frac{k}{s(s+50)} \to Y(s)=\frac{k}{50}(\frac{1}{s}-\frac{1}{s+50})$$

이를 라플라스 변환을 통해 

$$y(t)=\frac{k}{50}(1-\e^{-50t})$$

$$t \to \infty, y(\infty)=\frac{k}{50}=1 \to k=50이다.$$



## P2.15 
스프링-질량 시스템이 그림 P2.15에 주어졌다. 질량 m의 운동을 기술하는 미분방정식을 구하라. 초기조건이 0인 임펄스 입력에 대한 시스템의 응답 x(t)를 구하라.

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/b9849aac-3658-4446-b4f7-2ddb7379acd4"  width="600" height="500">

### 문제풀이

매달려 있는 스프링-질량-감쇠기는 뉴턴의 운동법칙을 이용해 문제를 해결해야한다. 여기서 마찰력, 스프링의 장력, 그리고 추의 중력을 이용한 식을 풀면,

$$m\frac{d^2x(t)}{dt^2} + b\frac{dx(t)}{dt} + kx(t) = 0$$

여기서 라플라스 변환을 이용해서,

$$m(S^2X(S) - Sx(0) - \frac{dx(t)}{dt}) + b(SX(S) - x(0)) + kX(S) = 0$$

$$r(t)=0,x(0)=x_0,\frac{dx(t)}{dt})=0 \to mS^2 X(S) -mSx_0 + bSX(S) - bx_0 + kX(S) = 0$$

식을 좌변을 X(S), 우변을 $x_0$로 정리하면

$$mS^2X(S) + bSX(S) + kX(S) = mSx_0 + bx_0$$

$$X(S)(mS^2+bS+k) = x_0(mS+b)$$

$$X(S) = \frac{mS+b}{mS^2+bS+k}x_0$$

처럼 정리된다. 이를 역라플라스 변환을 해주면

```
syms S m b k z
XS = (m*S + b)*z / (m*S^2 + b*S + k);
xt = ilaplace(XS);
disp(xt);
dirac(t)/S - (k*exp(-(t*(k + S*b))/S^2))/S^3
```

이므로, 식으로 정리하면

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/5342e24f-b1e7-4a33-bc35-bd313383e581"  width="200" height="100">



## P2.26
로봇은 그리퍼로 무거운 부하를 들 수 있으며 팔각 부위의 유연성이 높다[6,20]. 이 로봇의 두 질량모델이 그림 P2.26에 주어져 있다. 전달함수 $Y(s)/F(s)$를 구하라.

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/9d8328ef-8b09-4fff-80c2-b3e23248a5b2"  width="600" height="400">

### 문제풀이


$$M\frac{\mathrm{d^2x(t)}}{\mathrm{d} x^2} +b( \frac{\mathrm{dx(t)} }{\mathrm{d} x} -\frac{\mathrm{dy(t)} }{\mathrm{d} x}) + K(x(t)-y(t)) = F(t)$$

$$M\frac{\mathrm{d^2y(t)}}{\mathrm{d} x^2} +b( \frac{\mathrm{dy(t)} }{\mathrm{d} x} -\frac{\mathrm{dx(t)} }{\mathrm{d} x}) + K(y(t)-x(t)) = 0$$





## P.37
입력 힘 u(t)를 가지는 두 개의 질량 시스템을 그림 P2.37에 나타났다. $m_1 = m_2 = 1$ 이고 $K_1 = K_2 = 2$일 때, 
(a) 이 시스템을 표현하는 미분방정식을 구하라. 
(b) U(S)에서 Y(S)까지의 전달함수를 계산하라.

<img src="https://github.com/Ted2s/Control_Engineering/assets/144117619/b17ae3fe-f618-4e99-bebc-7a9419acf6fa"  width="600" height="500">

### 문제풀이




