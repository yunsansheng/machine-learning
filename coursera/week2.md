# multivariate linear regression


## multiple features 

### equations:

$h_\theta(x) = \theta_0+\theta_{1}x_1+\theta_{2}x_2+\theta_{3}x_3+...+\theta_{n}x_n$

$\begin{align*}x^{(i)} &= \text{input of the }i^{th}\text{ training example} \newline x_j^{(i)} &= \text{value of feature } j \text{ in the }i^{th}\text{ training example}  \newline m &= \text{the number of training examples} \newline n &= \text{the number of features} \end{align*}$

- $x^{(i)}$ 代表单个样本的集合,vector **注意上面的括号**
- $x_j^{(i)}$ 代表的是具体的值。vecotr中的一个值

上面的方程式可以简写为：
$\begin{align*}h_\theta(x) =\begin{bmatrix}\theta_0 \hspace{2em} \theta_1 \hspace{2em} ... \hspace{2em} \theta_n\end{bmatrix}\begin{bmatrix}x_0 \newline x_1 \newline \vdots \newline x_n\end{bmatrix}= \theta^T x\end{align*}$

- 为什么要用$\theta^T$:因为行*列得到一个合计值。
- $x^{i}_{0}$ 不管i是几，都是1.

### Gradient Descent For Multiple Variables

$\begin{align*} & \text{repeat until convergence:} \; \lbrace \newline \; & \theta_0 := \theta_0 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)}) \cdot x_0^{(i)}\newline \; & \theta_1 := \theta_1 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)}) \cdot x_1^{(i)} \newline \; & \theta_2 := \theta_2 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m} (h_\theta(x^{(i)}) - y^{(i)}) \cdot x_2^{(i)} \newline & \cdots \newline \rbrace \end{align*}$


### Feature Scaling

**goal**: speed up the learning

**method**: make features on a similar scale

特征缩放有很多种方法，只要能够把这些特征缩放到一定的比例就可以
推荐范围为： 最大在-3~+3之间，最小不能小于-1/3~+1/3之间

- feature scaling(rescaling)
	
	- $x_i= \frac{x_i-min(x)}{max(x)-min(x)}$
	- $-1 \leq x_i\leq 1$ or  $0\leq x_i\leq 1$
	
- mean normalizaiton
	- $x_i := \frac{x_i -u_i}{s_i}$ 
	- $u_i$ :average ,$s_i$: max - min
	- $-0.5 \leq x_i\leq 0.5$ or  $0\leq x_i\leq 0.5$
	

### learning reate

Debugging gradient descent. Make a plot with number of iterations on the x-axis. Now plot the cost function, J(θ) over the number of iterations of gradient descent. If J(θ) ever increases, then you probably need to decrease α.

Automatic convergence test. Declare convergence if J(θ) decreases by less than E in one iteration, where E is some small value such as $10^{−3}$. However in practice it's difficult to choose this threshold value.

- If α is too small: slow convergence. 
- If α is too large: ￼may not decrease on every iteration and thus may not converge.

### Features and Polynomial Regression 特征和多项式回归

we can combine multiple features into one.

We can change the behavior or curve of our hypothesis function by making it a quadratic, cubic or square root function (or any other form).

# computing parameters analytically

## Normal Equation

$\theta = (X^T X)^{-1} X^T y$

- X is the matrix of x,includ $x_0$(=1).
- **no need** to do feature scaling with the normal equation.

|gradient descent|normal equation|
|---|---|
|need chose alpha|no need|
|need iterations|no need|
|O($kn^2$)|O($n^3$),need to calculate inverse of $(X^T X)$ |
|work well in large|slow if n is very large|

if we have a very **large number of features**, the normal equation will be slow. In practice, when n exceeds **10,000** it might be a good time to go from a normal solution to an iterative process.

## Normal Equation Noninvertibility（正方程不可逆）

if noninvertible，the commen causes might be having:

- **Redundant features**, where two features are very closely **related** (i.e. they are linearly dependent)
- **Too many features** (e.g. m ≤ n). In this case, delete some features or use **"regularization"**(正则化)

# octave tutorial

see [octave语法介绍](https://www.coursera.org/learn/machine-learning/resources/QQx8l)

function in octave

1. 必须在脚本目录下创建一个 .m文件
2. 文件名，必须和函数名一致
3. 单返回值函数

```
function y = test(x)
y = x ^ 2
```

4. 多返回值函数

```
function [y1, y2 ] = test(x)
y1 = x ^ 2
y2 = x^3
```
