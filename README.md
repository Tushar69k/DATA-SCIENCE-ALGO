
# Conm Answers

### Q.1 a) False-position (Regula-Falsi) method — outline & derivation (short)

* Suppose (f(a)) and (f(b)) have opposite signs. The root lies in ([a,b]).
* Replace the interval end with the point where the **secant** through ((a,f(a))) and ((b,f(b))) crosses the x-axis:
  [
  c = b - f(b)\frac{b-a}{f(b)-f(a)} \quad(\text{or symmetrically } c=a - f(a)\frac{b-a}{f(b)-f(a)}).
  ]
* If (f(c)f(a)<0) keep ([a,c]) else keep ([c,b]). Repeat until desired tolerance.
* Converges linearly; faster than bisection often but can slow if one end becomes “stuck”.

### Q.1 b) Euler’s method — outline & derivation (short)

* From (y'=f(x,y),; y(x_0)=y_0). Use first-order Taylor:
  [
  y(x+h)=y(x)+h,y'(x)+O(h^2)=y(x)+h f(x,y)+O(h^2).
  ]
* Discrete iteration (explicit Euler):
  [
  y_{n+1}=y_n + h f(x_n,y_n).
  ]
* Local truncation error (O(h^2)), global error (O(h)). Simple but low accuracy / conditionally stable.

### Q.2 a) Gauss-elimination (outline)

* Transform the linear system (A\mathbf{x}=\mathbf{b}) by forward elimination to upper triangular form, then back substitution.
* Steps: for each pivot row (i):

  * For each row (j>i) compute multiplier (m_{ji}=a_{ji}/a_{ii}) and do (R_j\leftarrow R_j-m_{ji}R_i).
* After upper triangular, compute (x_n) from last equation and back substitute.
* Mention partial pivoting to avoid division by small pivots.

### Q.2 b) Define error & types (short)

* **True error**: (E_{\text{true}} = x_{\text{true}} - x_{\text{approx}}).
* **Relative error**: (|E_{\text{true}}/x_{\text{true}}|).
* **Truncation error**: from approximating infinite processes (Taylor truncation).
* **Rounding/error due to finite precision**: due to machine arithmetic.
* Give small numeric examples for each in exam.

### Q.3 a) Newton’s general divided difference formula

* Newton forward form (for nodes (x_0,\dots,x_n)):
  [
  P_n(x)=f[x_0]+f[x_0,x_1](x-x_0)+f[x_0,x_1,x_2](x-x_0)(x-x_1)+\cdots
  ]
* Divided differences defined recursively:
  [
  f[x_i]=f(x_i),\quad f[x_i,x_{i+1}]=\frac{f(x_{i+1})-f(x_i)}{x_{i+1}-x_i},
  ]
  [
  f[x_i,\dots,x_{i+k}] = \frac{f[x_{i+1},\dots,x_{i+k}]-f[x_i,\dots,x_{i+k-1}]}{x_{i+k}-x_i}.
  ]
* Use the divided-difference table to build polynomial incrementally.

### Q.3 b) Gauss backward central difference formula (outline)

* For equally spaced nodes and interpolation near the center, use central difference formulas (Gauss forward/backward) to get compact formulas for interpolation and differentiation; derive using Newton–Gregory central forms and differences (\Delta).
* (Exam-level writeup: show central difference operator relations and final Gauss backward formula.)

---

# Worked numerical problems (detailed, with final answers)

I solved these numerically and show the steps & final values.

---

## Q.4 a)

**Problem:** Using Taylor’s series method, solve ODE
[
\frac{dy}{dx} = 1 + x - y^2,\quad y(0)=0,\quad h=0.1.
]
Find (y(0.1)).

**Method (use Taylor up to 2nd derivative):**

Given (y' = 1 + x - y^2).

Compute second derivative:
[
y'' = \frac{d}{dx}(1+x-y^2)=1 - 2y,y'.
]

At (x=0,; y(0)=0): (y'(0)=1+0-0=1,; y''(0)=1-2\cdot0\cdot1=1.)

Taylor (to second order):
[
y(0.1) \approx y(0) + h y'(0) + \frac{h^2}{2} y''(0).
]
Plugging in (h=0.1):
[
y(0.1) \approx 0 + 0.1(1) + \frac{0.01}{2}(1) = 0.1 + 0.005 = \boxed{0.105}.
]

---

## Q.4 b)

**Problem:** From table
(x: 1.5,;2.0,;2.5,;3.0,;3.5,;4.0)
(f(x): 3.375,;7.000,;13.625,;24.000,;38.875,;59.000)
Find (f'(1.5)) and (f''(1.5)) using Newton’s forward difference derivative formula.

**Work:**

* Step (h=0.5). Build forward differences:

[
\begin{aligned}
\Delta f_0 &= 3.625,\quad \Delta^2 f_0 = 3.0,\quad \Delta^3 f_0 = 0.75,\quad \Delta^4 f_0 = 0.
\end{aligned}
]

* Newton forward derivative formula at (x_0):
  [
  f'(x_0)=\frac{1}{h}\Big(\Delta f_0 - \tfrac12\Delta^2 f_0 + \tfrac13\Delta^3 f_0 - \cdots\Big).
  ]

* Using terms up to (\Delta^3):
  [
  f'(1.5)=\frac{1}{0.5}\Big(3.625 - 0.5(3.0) + \tfrac13(0.75)\Big)
  =2\big(3.625 - 1.5 + 0.25\big)=2(2.375)=\boxed{4.75}.
  ]

* For second derivative (forward expansion):
  [
  f''(x_0)=\frac{1}{h^2}\Big(\Delta^2 f_0 - \Delta^3 f_0 + \cdots\Big)
  ]
  (using up to (\Delta^3)):
  [
  f''(1.5)=\frac{1}{(0.5)^2}\big(3.0 - 0.75\big)=\frac{2.25}{0.25}= \boxed{9.00}.
  ]

---

## Q.5 a)

**Problem:** Solve ODE by Picard successive approximations:
[
\frac{dy}{dx} = 1 + x y,\quad y(0)=1,\quad \text{in }[0,0.2],;h=0.1.
]
Find successive approximations up to third approximation.

**Picard iteration formula:**
[
y_{n+1}(x)=1+\int_0^x\big(1 + t,y_n(t)\big),dt.
]

Start (y_0(x)=1).

* (y_1(x)=1+\int_0^x(1+t\cdot1),dt = 1 + x + \tfrac{x^2}{2}.)

* (y_2(x)=1+\int_0^x\big(1 + t(1 + t + \tfrac{t^2}{2})\big)dt
  =1 + x + \tfrac{x^2}{2} + \tfrac{x^3}{3} + \tfrac{x^4}{8}.)

* (y_3(x)=1+\int_0^x\big(1+t,y_2(t)\big),dt
  =1 + x + \tfrac{x^2}{2} + \tfrac{x^3}{3} + \tfrac{x^4}{8} + \tfrac{x^5}{15} + \tfrac{x^6}{48}.)

**Numerical values** (useful at (x=0.1) and (x=0.2), step (h=0.1)):

* At (x=0.1):

  * (y_1(0.1)=1.105000),
  * (y_2(0.1)=1.1053458333333),
  * (y_3(0.1)=1.1053465208333).

* At (x=0.2):

  * (y_1(0.2)=1.220000),
  * (y_2(0.2)=1.2228666666667),
  * (y_3(0.2)=1.2228893333333).

So third approximation (y_3) at (x=0.1) is ≈ **1.10534652** and at (x=0.2) ≈ **1.22288933**.

---

## Q.5 b)

**Problem:** Find the root of (x^3 - 3x - 5 = 0) correct to three places using Newton-Raphson.

**Newton iteration:** (x_{n+1} = x_n - \dfrac{f(x_n)}{f'(x_n)}) with (f'(x)=3x^2 -3).

Using an initial guess (take (x_0=2.0)), iterating gives the root:
[
\boxed{x\approx 2.279\ (\text{to three decimals})}.
]
(Actual root ≈ 2.279018786…; rounded to 3 decimals 2.279.)

---

## Q.6 a)

**Problem:** Given data
[
x: 4.0,;4.2,;4.4,;4.6,;4.8,;5.0,;5.2,\
y:1.3863,;1.4351,;1.4816,;1.5261,;1.5686,;1.6094,;1.6487,
]
compute (\displaystyle\int_{4.0}^{5.2} y,dx) by (i) composite trapezoidal and (ii) Simpson’s 1/3 rule. (Here (h=0.2).)

**(i) Composite trapezoidal rule**
[
I_T = h\Big[\tfrac12 y_0 + y_1 + y_2 + \cdots + y_{n-1} + \tfrac12 y_n\Big].
]
With the data:
[
I_T \approx \boxed{1.8276600}.
]

**(ii) Composite Simpson’s 1/3 rule** (n must be even; here (n=6))
[
I_S = \frac{h}{3}\Big[y_0 + y_n + 4\sum_{odd} y_i + 2\sum_{even\ne0,n} y_i\Big].
]
Compute:
[
I_S \approx \boxed{1.8278533333}.
]

(Values are close; Simpson slightly different as expected.)

---

## Q.6 b)

**Problem:** Using Lagrange interpolation from the table
[
x: 0.0,0.1,0.2,0.3,0.4;\quad f(x):1.0000,1.1052,1.2214,1.3499,1.4918
]
find (f(0.35)).

**Solution (Lagrange polynomial of degree 4 evaluated at 0.35):**
[
f(0.35)\approx \boxed{1.4191140625}\approx 1.41911.
]

(Computed by direct Lagrange interpolation.)

---

## Q.7 a)

**Problem:** Given (\dfrac{dy}{dx}=\dfrac{3x+y}{2},; y(1)=1). Use Runge-Kutta 2nd order (midpoint) on interval ([1,1.2]) with (h=0.1).

**Method (RK2 midpoint):** for each step
[
k_1 = f(x_n,y_n),\quad k_2 = f\big(x_n+\tfrac{h}{2},,y_n+\tfrac{h}{2}k_1\big),
\quad y_{n+1}=y_n + h k_2.
]

**Two steps (from 1.0 → 1.1 → 1.2):**

* Step 1: (x_0=1.0,y_0=1.0).

  * (k_1=(3\cdot1+1)/2=2.0).
  * (k_2=f(1.05,,1+0.05\cdot2) = f(1.05,1.1)=(3\cdot1.05+1.1)/2=(3.15+1.1)/2=2.125).
  * (y_1 = 1.0 + 0.1\cdot2.125 = \boxed{1.2125}).

* Step 2: (x_1=1.1,y_1=1.2125).

  * (k_1=f(1.1,1.2125)=(3.3+1.2125)/2=2.25625).
  * (k_2=f(1.15,,1.2125+0.05\cdot2.25625)=f(1.15,1.3233125) = (3\cdot1.15 + 1.3233125)/2=(3.45+1.3233125)/2=2.38665625).
  * (y_2 = 1.2125 + 0.1\cdot2.38665625 = \boxed{1.451265625}.)

So:
[
y(1.1)\approx 1.2125,\quad y(1.2)\approx 1.451265625.
]

---

## Q.7 b)

**Problem:** Solve the linear system by Gauss–Seidel, correct to three decimals:

System (as in the paper)
[
\begin{cases}
-28 x_1 + 4 x_2 - x_3 = 32,[2pt]
x_1 + 3 x_2 + 10 x_3 = 24,[2pt]
2 x_1 + 17 x_2 + 4 x_3 = 35.
\end{cases}
]

**Remark:** Convergence of Gauss–Seidel is eased when the coefficient matrix is (strictly) diagonally dominant. The given system is not diagonally dominant in its original row order for all rows, so we can **permute the equations** to obtain a row order that is diagonally dominant and then apply Gauss–Seidel.

Permutation used: keep row1 as is, swap row2↔row3 (i.e. use order: eq1, eq3, eq2). After that Gauss–Seidel converges rapidly.

**Result (to three decimals):**
[
\boxed{x_1 \approx -0.970,\quad x_2 \approx 1.706,\quad x_3 \approx 1.985.}
]

(Exact solution computed numerically: (x_1\approx -0.97006924,; x_2\approx 1.70582980,; x_3\approx 1.98525799). Rounded to 3 decimals as above.)

---

# Summary of final numeric answers (quick list)

* Q4(a) (y(0.1)=\boxed{0.105}).
* Q4(b) (f'(1.5)=\boxed{4.75},; f''(1.5)=\boxed{9.00}.)
* Q5(a) Picard approximations:

  * (y_1(x)=1+x+\tfrac{x^2}{2}),
  * (y_2(x)=1+x+\tfrac{x^2}{2}+\tfrac{x^3}{3}+\tfrac{x^4}{8}),
  * (y_3(x)=1+x+\tfrac{x^2}{2}+\tfrac{x^3}{3}+\tfrac{x^4}{8}+\tfrac{x^5}{15}+\tfrac{x^6}{48}.)
  * Numerically: (y_3(0.1)\approx1.1053465,; y_3(0.2)\approx1.2228893.)
* Q5(b) Newton-Raphson root: (\boxed{2.279}) (3 decimals).
* Q6(a) Integral from 4.0 to 5.2:

  * Trapezoidal: (\boxed{1.8276600}).
  * Simpson 1/3: (\boxed{1.8278533333}).
* Q6(b) Lagrange (f(0.35)\approx\boxed{1.4191140625}).
* Q7(a) RK2:

  * (y(1.1)\approx\boxed{1.2125},; y(1.2)\approx\boxed{1.451265625}.)
* Q7(b) Gauss–Seidel (3 d.p.):

  * (\boxed{x_1=-0.970,;x_2=1.706,;x_3=1.985.})

---

