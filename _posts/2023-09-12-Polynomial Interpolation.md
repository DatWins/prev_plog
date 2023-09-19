---
title: Polynomial Interpolation(보간 다항식)
date: 2023-09-12-23:39:00 +0900
categories: [AI Math, Numerical Analysis]
tags: [Interpolation, Lagrange Interpolation, Newton Polynomial interpolation]
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

## **미정 계수법**

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

## **Lagrange Interpolation((라그랑주 보간법)**

연립 방정식을 풀지 않고 다항식을 결정하는 방법

특정 숫자를 대입하면 0이나 1이 되는 항을 만든다.

1. $(x-a)$를 곱해주면 $x$에 a값을 대입할 때 0이 된다.
2. $(x-a)$를 $(b-a)$로 나누면, $x$에 $b$를 대입했을 때 1이 된다.

### **1차 함수**

$$
y=\left(\frac{x-x_1}{x_0-x_1}\right) y_0+\left(\frac{x-x_0}{x_1-x_0}\right) y_1
$$

### **2차 함수**

$$
y=\left(\frac{\left(x-x_1\right)\left(x-x_2\right)}{\left(x_0-x_1\right)\left(x_0-x_2\right)}\right) y_0+\left(\frac{\left(x-x_2\right)\left(x-x_0\right)}{\left(x_1-x_2\right)\left(x_1-x_0\right)}\right) y_1\\
+\left(\frac{\left(x-x_0\right)\left(x-x_1\right)}{\left(x_2-x_0\right)\left(x_2-x_1\right)}\right) y_2
$$

### **3차 함수**

$$
y=\left(\frac{\left(x-x_1\right)\left(x-x_2\right)\left(x-x_3\right)}{\left(x_0-x_1\right)\left(x_0-x_2\right)\left(x_0-x_3\right)}\right) y_0\\
+\left(\frac{\left(x-x_2\right)\left(x-x_3\right)\left(x-x_0\right)}{\left(x_1-x_2\right)\left(x_1-x_3\right)\left(x_1-x_0\right)}\right) y_1\\
+\left(\frac{\left(x-x_0\right)\left(x-x_1\right)\left(x-x_3\right)}{\left(x_2-x_0\right)\left(x_2-x_1\right)\left(x_2-x_3\right)}\right) y_2\\
+\left(\frac{\left(x-x_0\right)\left(x-x_1\right)\left(x-x_2\right)}{\left(x_3-x_0\right)\left(x_3-x_1\right)\left(x_3-x_2\right)}\right) y_3
$$

### **일반화**

$$
L_i(x)=\prod_{\substack{j=0 \\ j \neq i}}^n \frac{x-x_j}{x_i-x_j}
$$

$$
\begin{matrix}P_n(x)&=&L_0(x) f\left(x_0\right)+L_1(x) f\left(x_1\right)+\cdots L_n(x) f\left(x_n\right)\\\\
&=&\sum_{i=0}^n L_{i(x)} f\left(x_i\right)
\end{matrix}
$$

Q. 단일 함수를 구할 수 있는가?

$P_n\left(x_i\right)=y_i$를 만족하므로 $\mathrm{n}+1$개의 점 $\left(x_i, y_i\right)$을 지나는 유일한 $\mathrm{n}$차 다항식이다.

Q. 연산량이 기존 방법과 비교했을 때 늘어나는가, 줄어드는가?

### **단점**

- 차수가 커지면 참 값을 기대할 수 없을 정도의 오차가 발생한다.
- 데이터의 수가 증가할 때, 바로 직전의 결과를 사용하지 못한다.
    
    점이 추가되면 식을 처음부터 다시 계산해야 한다.
    
- 하나의 보간을 위해 필요한 계산량이 많다.

## **Newton’s divided difference interpolation**

라그랑주 보간법의 모든 단점을 해결하는 방법

연립 일차 방정식을 사용하지 않는다.

점 두 개로 일차 함수를 먼저 그린 후, 점을 추가해나가며 다항식의 차수를 점점 확장해나가는 방식

인수 분해를 활용한다.

### **e.g.  $(1.23,5), (3.23,4), (5.23,8)$ 세 점을 지나는 다항식 구하기**

![Interpolation](/assets/post_imgs/interpolation.png)

1. **두 점 $(1.23,5), (3.23,4)$을 지나는 일차 함수 $g(x)$ 그리기**
    
    $$
    g(x)\ =\ \frac{4-5}{\left(3.23-1.23\right)}\left(x\ -1.23\right) + 5 = -\frac{1}{2}x + 5.615
    $$
    
    ![Interpolation](/assets/post_imgs/interpolation1.png)
    
2. **위의 두 점 $(1.23,5), (3.23,4)$에서 $g(x)$와 만나는 이차 함수 $f(x)$ 그리기**
    
    $$
    f(x) - g(x) = a(x - 1.23)(x - 3.23)
    $$
    
    $$
    \begin{matrix}f(x) &=& g(x) + a(x - 1.23) (x-3.23)\\
    &=& -\frac{1}{2}x + 5.615 + a(x - 1.23) (x-3.23)
    \end{matrix}
    $$
    
3. **$f(5.23) = 8$이므로,**
    
    $$
    \begin{matrix}
    f(5.23) &=& -\frac{1}{2}5.23 + 5.615 + a(5.23 - 1.23) (5.23-3.23)\\
    &=& 3 + 8a = 8
    \end{matrix}
    $$
    
    $a = 0.625$임을 알 수 있다.
    
    $$
    f(x) = -\frac{1}{2}x + 5.615 + 0.625(x - 1.23) (x-3.23)\\
        = \frac{5 x^2}{8}-\frac{263 x}{80}+\frac{129569}{16000}
    $$
    
    ![Interpolation](/assets/post_imgs/interpolation2.png)
    
4. 만약 점이 추가되면 동일한 방식으로 반복하면 된다.

**장점**

새로운 데이터가 추가되어도 차수를 늘리기 쉽다.

즉, 이전 결과를 사용할 수 있다.
