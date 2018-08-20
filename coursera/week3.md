# classification and representation

## binary classification problem

Our new form uses the "Sigmoid Function,"(s型生长曲线) also called the "Logistic Function":

$\begin{align*}& h_\theta (x) = g ( \theta^T x ) \newline \newline& z = \theta^T x \newline& g(z) = \dfrac{1}{1 + e^{-z}}=\dfrac{1}{1 + \frac {1}{e^z} }\end{align*}$

- **注意**

$$e^{-z} = \frac{1}{e^z}$$

$\begin{align*}& h_\theta(x) = P(y=1 | x ; \theta) = 1 - P(y=0 | x ; \theta) \newline& P(y = 0 | x;\theta) + P(y = 1 | x ; \theta) = 1\end{align*}$

**In order to get our discrete 0 or 1 classification**, we can translate the output of the hypothesis function as follows:

$\begin{align*}& h_\theta(x) \geq 0.5 \rightarrow y = 1 \newline& h_\theta(x) < 0.5 \rightarrow y = 0 \newline\end{align*}$

## Decision Boundary

根据s型函数的特性，可做如下推导：

$\begin{align*}& g(z) \geq 0.5 \newline& when \; z \geq 0\end{align*}$

z代表的是之前的$\theta^T x$(线性函数)因此

$\theta^T x \geq 0 \rightarrow y=1$

$\theta^T x < 0 \rightarrow y=0$

Again, the input to the sigmoid function,**g(z) doesn't need to be linear**, and could be a function that describes a circle or any shape to fit our data.



# logistic regression model

## cost function

We cannot use the same cost function that we use for linear regression because the Logistic Function will cause the output to be **wavy**, causing many local optima. In other words, it will not be a convex function.

Instead, our cost function for logistic regression looks like:

$\begin{align*}& J(\theta) = \dfrac{1}{m} \sum_{i=1}^m \mathrm{Cost}(h_\theta(x^{(i)}),y^{(i)}) \newline & \mathrm{Cost}(h_\theta(x),y) = -\log(h_\theta(x)) \; & \text{if y = 1} \newline & \mathrm{Cost}(h_\theta(x),y) = -\log(1-h_\theta(x)) \; & \text{if y = 0}\end{align*}$


- 线性函数的代价函数

$J(\theta_0,\theta_{1}) = \frac{1}{2m}\sum\limits_{i=1}^m(h_{\theta}(x^{(i)}-y^{(i)})^2$ 

- 区别，没有$\frac1 2$,用cost函数（-log函数）代替平方函数
- 函数是一个从0到1的曲线。

$\begin{align*}& \mathrm{Cost}(h_\theta(x),y) = 0 \text{ if } h_\theta(x) = y \newline & \mathrm{Cost}(h_\theta(x),y) \rightarrow \infty \text{ if } y = 0 \; \mathrm{and} \; h_\theta(x) \rightarrow 1 \newline & \mathrm{Cost}(h_\theta(x),y) \rightarrow \infty \text{ if } y = 1 \; \mathrm{and} \; h_\theta(x) \rightarrow 0 \newline \end{align*}$

## simplified cost function

单个的代价函数

$\begin{align*}&  \mathrm{Cost}(h_\theta(x),y) = -\log(h_\theta(x)) \; & \text{if y = 1} \newline & \mathrm{Cost}(h_\theta(x),y) = -\log(1-h_\theta(x)) \; & \text{if y = 0}\end{align*}$

**note: y= 0 or 1 always**

$Cost(h_θ​(x),y)=−ylog(h_θ​(x))−(1−y)log(1−h_θ​(x))$

$J(\theta) = -\frac{1}{m}\sum\limits_{i=1}^m[y^{(i)}log(h_θ​(x^{(i)})+(1−y^{(i)})log(1−h_θ​(x^{(i)}))]$ 

- 这里的$h_\theta x^{(i)}$ 和线性函数中的**不是同一个东西**
- 一个是$\theta^Tx$， 而这里是$\dfrac{1}{1 + e^{-\theta^T x}}$

## Advanced Optimization(高级优化)

- Conjugate gradient 共轭梯度法
- BFGS
- L-BFGS

### advantage
- no need to pick  $\alpha$
- faster than gradient descent 


We first need to provide a function that evaluates the following two functions for a given input value θ:

$j(\theta)$

$\frac{\partial}{\partial\theta_j}j(\theta)$

记住公式，暂不推导：

$\frac{\partial}{\partial\theta_j}J(\theta))$ 
 =>$\frac{1}{m}\sum\limits_{i=1}^m(h_{\theta}(x^{(i)}-y^{(i)}) x_j^{(i)}$

```
function [jVal, gradient] = costFunction(theta)
  jVal = [...code to compute J(theta)...]; #计算J(θ)
  gradient = [...code to compute derivative of J(theta)...]; #计算J(θ)偏导
end
```

例子：

costfunction.m

```
function [jval,gradient] =costfunction(theta)

jval = (theta(1)-5)^2+(theta(2)-5)^2

gradient =zeros(2,1);
gradient(1) = 2*(theta(1)-5);
gradient(2) = 2*(theta(2)-5);
```

octave:

```
initialTheta  =zeros(2,1)
options=optimset('GradObj','on','MaxIter','100');

[optthata,functionval,exitflag] =fminunc(@costfunction,initialTheta,options)

```

#multiclass classification



## The Problem of Overfitting

### Underfitting(high bias)
- Underfitting, or high bias, is when the form of our hypothesis function h maps poorly to the trend of the data. 
- caused by a function that is too simple or uses too few features

### Overfitting (high variance)
- is caused by a hypothesis function that fits the available data but does not generalize well to predict new data. 
- usually caused by a complicated function that creates a lot of unnecessary curves and angles unrelated to the data.

### how to slove overfitting
1. Reduce the numbers of features.
	- manually select which features to keep.
	- use a model selection algorithm.
2. Regularization
	- keep all features, but reduce the magnitude of $\theta_j$
	- regularization works well when we have a lot of silghtly useful features.


## cost function

eliminate the influence of ($ \theta_3, \theta_4$)

$min_\theta \frac{1}{2m} \sum\limits^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})+1000 \cdot\theta_3^2+ 1000\cdot\theta_4^2$

We could also regularize all of our theta parameters in a single summation as:

$min_\theta \frac{1}{2m} \sum\limits^m_{i=1}(h_\theta(x^{(i)})-y^{(i)})+ \lambda \sum\limits^n_{j=1} \theta_j^2$

- $\lambda$ is the regularization parameter,it determines how much the cost of the theta parameters are inflated.
- Using the above cost function with the extra summation, we can smooth the output of our hypothesis function to reduce overfitting.
-  If lambda is chosen to be too large, it may smooth out the function too much and cause underfitting. 

## regularized linear regression

### Gradient Descent
- We will modify our gradient descent function to separate out $\theta_0$from the rest of the parameters because we do not want to penalize $\theta_0$

$\begin{align*} & \text{Repeat}\ \lbrace \newline & \ \ \ \ \theta_0 := \theta_0 - \alpha\ \frac{1}{m}\ \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})x_0^{(i)} \newline & \ \ \ \ \theta_j := \theta_j - \alpha\ \left[ \left( \frac{1}{m}\ \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)} \right) + \frac{\lambda}{m}\theta_j \right] &\ \ \ \ \ \ \ \ \ \ j \in \lbrace 1,2...n\rbrace\newline & \rbrace \end{align*}$
we can also represent $\theta_j$ as :

$\theta_j := \theta_j(1-\alpha \frac{\lambda}{m})- \alpha\frac{1}{m} \sum\limits^m_{i=1}(h_\theta(x^{(i)})-y^{(i)}) x_j^{(i)}$

- $1−α\frac{λ}{m}$ will always be less than 1.

- otice that the second term is now exactly the same as it was before

  

### Normal Equation

(Before: $\theta = (X^T X)^{-1}X^T y$)





- To add in regularization, the equation is the same as our original, except that we add another term inside the parentheses:
- L is a matrix with 0 at the top left and 1's down the diagonal, with 0's everywhere else.  It should have dimension (n+1)×(n+1).
- Recall that if m < n, then$ X^TX$ is non-invertible. However, when we add the term λ⋅L, then $X^TX$ + λ⋅L becomes invertible.

## regularized logistic regression

Recall that our cost function for logistic regression was:

$J(\theta) =- \frac{1}{m}\sum\limits ^m_{i=1}[y^{(i)}log(h_\theta(x^{(i)})+(1-y^{(i)})log(1-h_\theta(x^{(i)}))]$

we can regularize the equation by adding a term to the end:

$J(\theta) =- \frac{1}{m}\sum\limits ^m_{i=1}[y^{(i)}log(h_\theta(x^{(i)}))+(1-y^{(i)})log(1-h_\theta(x^{(i)}))]+\frac{\lambda}{2m}\sum\limits^n_{j=1}\theta^2_j$

- not include $\theta_0$

$\begin{align*}& \text{Repeat}\ \lbrace \newline& \ \ \ \ \theta_0 := \theta_0 - \alpha\ \frac{1}{m}\ \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})x_0^{(i)} \newline& \ \ \ \ \theta_j := \theta_j - \alpha\ \left[ \left( \frac{1}{m}\ \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)} \right) + \frac{\lambda}{m}\theta_j \right] &\ \ \ \ \ \ \ \ \ \ j \in \lbrace 1,2...n\rbrace\newline& \rbrace\end{align*}$

- This is identical to the gradient descent function presented for linear regression.

