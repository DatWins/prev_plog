---
title: Polynomial Interpolation(보간 다항식)
date: 2023-09-12-23:39:00 +0900
categories: [AI Math, Numerical Analysis]
tags: [Interpolation, Lagrange Interpolation, Newton Polynomial interpolation]
img_path: /assets/post_imgs/
math: true
---
# Linear Interpolation

가장 간단한 보간법

두 점을 이은 직선의 방정식을 근사 함수로 사용한다.

데이터 점들 사이의 간격이 작을수록 더 좋은 근삿값을 얻는다.

$$
\mathrm{g}(x)=\frac{f\left(x_{i+1}\right)-f\left(x_i\right)}{x_{i+1}-x_i}\left(x-x_i\right)+f\left(x_i\right)
$$

# **Polynomial interpolation**

(n+1)개의 점이 주어진 경우 n차 이하의 **유일한** 다항식을 구할 수 있다.

- **Q. n+1개의 점으로 찾을 수 있는 n차 다항식은 왜 유일한가?**
    
    **방데르몽드 행렬**
    
    각 행의 초항이 1인 등비수열로 이루어진 행렬
    
    $$
    V=\left(\begin{array}{ccccc}1 & \alpha_1 & \alpha_1^2 & \cdots & \alpha_1^{n-1} \\1 & \alpha_2 & \alpha_2^2 & \cdots & \alpha_2^{n-1} \\1 & \alpha_3 & \alpha_3^2 & \cdots & \alpha_3^{n-1} \\\vdots & \vdots & \vdots & & \vdots \\1 & \alpha_m & \alpha_m^2 & \cdots & \alpha_m^{n-1}\end{array}\right)
    $$
    
    방데르몽드 행렬 $V$에 대해 다음과 같이 일반화할 수 있다.
    
    $$
    \operatorname{det} V=\prod_{i<j}\left(\alpha_i-\alpha_j\right)
    $$
    
    따라서, $a_0,a_1,...,a_n$이 서로 다른 값을 가진다면 $V$는 역행렬이 존재한다.
    
    가역 행렬의 기본 정리에 의해 $\tt Vx = b$의 해는 유일하다.
    

이제 다항식을 찾아내는 세 가지 방법을 알아보자.

### **미정 계수법**

다항식을 찾는 가장 보편적인 방법

보간 다항식 $p(x) = a_0 + a_1x + a_2x^2 + ... + a_nx^n$에 대해

1. **주어진 $n+1$개의 점을 $p(x)$에 대입하여 연립 방정식을 생성한다.**
    
    모두 다 대입하면 아래와 같이 방데르몽드 행렬식 형태를 얻을 수 있다.
    
    $$
    \begin{array}{cc}p\left(x_0\right)=f\left(x_0\right) & a_0+a_1 x_0+a_2 x_0^2+\cdots+a_n x_0^n=f\left(x_0\right) \\p\left(x_1\right)=f\left(x_1\right) & a_0+a_1 x_1+a_2 x_1^2+\cdots+a_n x_1^n=f\left(x_1\right) \\\vdots & \vdots \\p\left(x_n\right)=f\left(x_n\right) & a_0+a_1 x_n+a_2 x_n^2+\cdots+a_n x_n^n+\left(x_n\right)\end{array}
    $$
    
    $$
    \left[\begin{array}{ccccc}1 & x_0 & x_0^2 & \cdots & x_0^n \\1 & x 1 & x_1^2 & \cdots & x_1^n \\& & & \cdots & \\1 & x_n & x_n^2 & \cdots & x_n^n\end{array}\right]\left[\begin{array}{l}a 0 \\a 1 \\\cdots \\a n\end{array}\right]=\left[\begin{array}{c}f\left(x_0\right) \\f\left(x_1\right) \\\cdots \\f\left(x_n\right)\end{array}\right]
    $$
    
2. **가우스 소거법 등으로 연립 방정식의 해를 구한다.**

**단점**

- 느린 계산 시간
- 오차 발생

### **Lagrange Interpolation((라그랑주 보간법)**

연립 방정식을 풀지 않고 다항식을 결정하는 방법

특정 숫자를 대입하면 0이나 1이 되는 항을 만든다.

1. $(x-a)$를 곱해주면 $x$에 a값을 대입할 때 0이 된다.
2. $(x-a)$를 $(b-a)$로 나누면, $x$에 $b$를 대입했을 때 1이 된다.

**1차 함수**

두 점$(x_0, y_0), (x_1, y_1)$이 주어진 경우

$$
y=\left(\frac{x-x_1}{x_0-x_1}\right) y_0+\left(\frac{x-x_0}{x_1-x_0}\right) y_1
$$

위 식에 $x_0$을 대입하면 $y_0$이 나오고, $x_1$을 대입하면 $y_1$이 나온다.

해당 식은 직관적으로 $(x_0,0),(x_1,y_1)$을 지나는 직선의 기울기와 $(x_0,y_0),(x_1,0)$을 지나는 직선의 기울기의 합으로 이해할 수 있다.

![Alt text](polynomial_interpolation.png)

**2차 함수**

세 점$(x_0, y_0), (x_1, y_1), (x_2, y_2)$이 주어진 경우

$$
y=\left(\frac{\left(x-x_1\right)\left(x-x_2\right)}{\left(x_0-x_1\right)\left(x_0-x_2\right)}\right) y_0+\left(\frac{\left(x-x_2\right)\left(x-x_0\right)}{\left(x_1-x_2\right)\left(x_1-x_0\right)}\right) y_1\\
+\left(\frac{\left(x-x_0\right)\left(x-x_1\right)}{\left(x_2-x_0\right)\left(x_2-x_1\right)}\right) y_2
$$

![Alt text](polynomial_interpolation1.png)

마찬가지로, $(x_i,y_i)$를 지나면서 $(x_j,0)$을 지나는 이차 함수의 기울기의 합으로 이해할 수 있다.

**3차 함수**

네 점이 주어진 경우

$$
y=\left(\frac{\left(x-x_1\right)\left(x-x_2\right)\left(x-x_3\right)}{\left(x_0-x_1\right)\left(x_0-x_2\right)\left(x_0-x_3\right)}\right) y_0\\
+\left(\frac{\left(x-x_2\right)\left(x-x_3\right)\left(x-x_0\right)}{\left(x_1-x_2\right)\left(x_1-x_3\right)\left(x_1-x_0\right)}\right) y_1\\
+\left(\frac{\left(x-x_0\right)\left(x-x_1\right)\left(x-x_3\right)}{\left(x_2-x_0\right)\left(x_2-x_1\right)\left(x_2-x_3\right)}\right) y_2\\
+\left(\frac{\left(x-x_0\right)\left(x-x_1\right)\left(x-x_2\right)}{\left(x_3-x_0\right)\left(x_3-x_1\right)\left(x_3-x_2\right)}\right) y_3
$$

**일반화**

$$
L_i(x)=\prod_{\substack{j=0 \\ j \neq i}}^n \frac{x-x_j}{x_i-x_j}
$$

위의 식은 곧 $x_i$를 넣었을 때 $y_i$가 나온다는 것을 의미한다.

$$
\begin{matrix}P_n(x)&=&L_0(x) f\left(x_0\right)+L_1(x) f\left(x_1\right)+\cdots L_n(x) f\left(x_n\right)\\\\
&=&\sum_{i=0}^n L_{i(x)} f\left(x_i\right)
\end{matrix}
$$

Q. 단일 함수를 구할 수 있는가?

$P_n\left(x_i\right)=y_i$를 만족하므로 $\mathrm{n}+1$개의 점 $\left(x_i, y_i\right)$을 지나는 유일한 $\mathrm{n}$차 다항식이다.

Q. 연산량이 기존 방법과 비교했을 때 늘어나는가, 줄어드는가?

**단점**

- 차수가 커지면 참 값을 기대할 수 없을 정도의 오차가 발생한다.
- 데이터의 수가 증가할 때, 바로 직전의 결과를 사용하지 못한다.
    
    점이 추가되면 식을 처음부터 다시 계산해야 한다.
    
- 하나의 보간을 위해 필요한 계산량이 많다.

---

그렇다면, 식을 처음부터 다시 계산하지 않는 방법은 없을까?

결국 라그랑주 보간법은 각 점을 지나는 함수의 기울기를 합산하는 방식이기 때문에, 반복되는 기울기 연산을 제거한다면 연산을 줄일 수 있다. 이를 위해 Divided Difference이 쓰인다.

## **Newton’s divided differences interpolation**

라그랑주 보간법의 모든 단점을 해결하는 방법

- 점 두 개로 일차 함수를 먼저 그린 후, 점을 추가해나가며 다항식의 차수를 점점 확장해나가는 방식
- 연립 일차 방정식을 사용하지 않는다.
- 뉴턴 형을 활용한다.

### Divided Differences(분할 차분법)

> **간단 요약**
> 
> 
> 분할 구간에서 함수값들의 차이
> 
> 기울기에 대한 이산적인 추정치로 사용할 수 있다.
> 

뉴턴 형이 주어졌을 때, 상수 항들을 어떻게 계산해야 할까?

**뉴턴 형**

서로 다른 점 $x_0, ..., x_n$에 대해 x값에 따라 상수 항들을 순서대로 구할 수 있는 형태

$$
\begin{matrix}P_n(x)=a_0+a_1\left(x-x_0\right)
+a_2\left(x-x_0\right)\left(x-x_1\right)
+\\\ldots
+a_n\left(x-x_0\right)\left(x-x_1\right) \ldots\left(x-x_{n-1}\right)\end{matrix}
$$

식이 복잡하게 생겼다. $P_n(x) = f(x)$라 정의하고, 식을 상수 항 기준으로 정리해보자.

### $a_0, a_1$ 도출 과정

$$
a_0 = f\left(x_0\right)\\
f(x_1) = a_0 + a_1(x_1-x_0),
\\
\therefore a_1 =  {f\left(x_1\right) - f(x_0)\over x_1-x_0}
$$

해당 식의 형태를 $f[x_0,x_1]$로 치환하자.

이는 first order Divided Difference라고 부른다.

### **first order Divided Difference**

$$
f\left[x_0, x_1\right]=\frac{f\left(x_1\right)-f\left(x_0\right)}{x_1-x_0}
$$

한글로 번역하면 1차 분할 차분인데, 이는 위의 수식이 1차 미분에 대한 이산적인 추정치로 쓰일 수 있기 때문이다.

만약 $f(x)$가 구간 $[x_0,x_1]$에서 미분 가능하다면, 평균값 정리에 의해$f\left[x_0, x_1\right]=f^{\prime}(c)$임을 보장한다.

### $a_2$ 도출 과정

$$
\begin{matrix}
f(x_2) &=& a_0 + a_1(x_2 - x_0) + a_2(x_2-x_0)(x_2-x_1)\\
&=& f(x_0) + (x_2 - x_0)(a_1 + a_2(x_2 - x_1)),\\
f(x_2) - f(x_0) &=& (x_2-x_0)(a_1 + a_2(x_2 - x_1))
\end{matrix}
$$

이고, 이를 좀 더 정리하면

$$
\frac{f(x_2)-f(x_0)}{x_2-x_0} = a_1 + a_2(x_2 - x_1)
$$

이 된다.

여기서, $a_1$과 $a_2$에서 반복되는 형태를 $f[x_a,x_b]$로 치환하자.

$$
f[x_0,x_2] = f[x_0,x_1] + a_2(x_2 - x_1)\\
\frac{f[x_0,x_2] - f[x_0,x_1]}{x_2 - x_1} = a_2\\
$$

위 식은 $f[x_0,x_1,x_2]$로 치환하며, **Second order Divided Difference**라고 부른다.

### **High order Divided Difference**

$$
f\left[x_0, x_1, x_2\right]=\frac{f\left[x_1, x_2\right]-f\left[x_0, x_1\right]}{x_2-x_0}
$$

$$
f\left[x_0, x_1, x_2, x_3\right]=\frac{f\left[x_1, x_2, x_3\right]-f\left[x_0, x_1, x_2\right]}{x_3-x_0}
$$

$$
f\left[x_0, \ldots, x_n\right]=\frac{f\left[x_1, \ldots, x_n\right]-f\left[x_0, \ldots, x_{n-1}\right]}{x_n-x_0}
$$

이와 같은 형태로 나머지 $a_n$에 대해서도 정리할 수 있고, 최종적으로 기존의 뉴턴 형은 다음과 같은 형태가 된다.

$$
\begin{aligned}& P_1(x)=f\left(x_0\right)+\left(x-x_0\right) f\left[x_0, x_1\right] \\& \begin{aligned}P_2(x)=f\left(x_0\right) & +\left(x-x_0\right) f\left[x_0, x_1\right] \\& +\left(x-x_0\right)\left(x-x_1\right) f\left[x_0, x_1, x_2\right]\end{aligned}\\
&\ \ \ \ \ \ \ \ \ \ \ \ \vdots\\&
\begin{aligned}P_n(x)=f\left(x_0\right) & +\left(x-x_0\right) f\left[x_0, x_1\right]+\cdots \\& +\left(x-x_0\right)\left(x-x_1\right) \cdots\left(x-x_{n-1}\right) f\left[x_0, x_1, \ldots, x_n\right]\end{aligned}\end{aligned}
$$

여기에서 중요한 점은, 기호화를 함으로써 값을 재활용할 수 있게 되었다.

또한, 기존의 값을 활용하여 다음 값을 구할 수 있게 되었다.

---

### Error in polynomial interpolation

$$
e_n(x)=f(x)-p_n(x)
$$

- $f(x):$  구간 $[a,b]$에서 정의된 함수
- $p_n(x): n+1$ $n+1$$f(x)$의 보간 다항식
    
    따라서 다음이 성립한다.
    
    $$
    \begin{aligned}
    & p_{n+1}\left(x_i\right)=f\left(x_1\right), \quad i=0,1,2, \cdots, n \\
    & p_{n+1}(\bar{x})=f(\bar{x})
    \end{aligned}
    $$
    
    뉴턴 공식으로 다시 표현하면
    
    $$
    p_{n+1}(x)=p_n(x)+f\left[x_0, x_1, \cdots, x_n, \bar{x}\right] \prod_{j=0}^n(x-x j)
    $$
    
    과 같고, 이 때의 $f(x)$는 다음과 같다.
    
    $$
    f(\bar{x})=p_{n+1}+f\left[x_0, x_1, \cdots, x_n, \bar{x}\right) \prod_{j=0}^n\left(\bar{x}-x_j\right)
    $$
    
    아래에서 표현된 식들로 오차에 대한 식을 다시 정리해보면
    
    $$
    e_n(\bar{x})=f\left[x_0, x_1, \cdots, x_n, \bar{x}\right] \prod_{j=0}^n\left(\bar{x}-x_j\right)
    $$
    
    위처럼 나타낼 수 있다.

