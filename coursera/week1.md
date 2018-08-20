# Introduction

## Definition 

A computer program is said to learn from **experience E** with respect to some **task T** and some **performance measure P**, if its performance on T, as measured by P, improves with experience E.

## Machine learning algorithms:

- supervised learning
- unsupervised learning
- others
	- Reinforcement learning(强化学习)
	- Recommender systems(推荐系统)

### Supervised learning 
- Regression 
	- linear regression with one variable
		- cost function
		- gradient descent
			- batch gradient dscent
- classification
	
	In supervised learning, we are **given a data set** and already know what our **correct output should look like**, having the idea that there is a relationship between the input and the output.
	
	Supervised learning problems are categorized into **"regression"** and **"classification"** problems.
	
	In a regression problem, we are trying to predict results **within a continuous output**, meaning that we are trying to map input variables to some continuous function. 
	In a classification problem, we are instead trying to predict results **in a discrete output**. In other words, we are trying to map input variables into discrete categories.
	
	- Example
		- Given data about the size of houses on the real estate market, try to predict their price. 
		- Given a picture of a person, we have to predict their age on the basis of the given picture(Regression)
		- Given a patient with a tumor, we have to predict whether the tumor is malignant or benign.(Classification)


### Unsupervised learning 
Unsupervised learning allows us to approach problems with little or **no idea what our results should look like**. 
	
We can derive structure from data where we don't necessarily know the effect of the variables.We can derive this structure by clustering the data based on relationships among the variables in the data.
	
With unsupervised learning there is **no feedback based on the prediction results**.
	
- Example:
	- Clustering: Take a collection of 1,000,000 different genes, and find a way to automatically group these genes into groups that are somehow similar or related by different variables, such as lifespan, location, roles, and so on.
	- Non-clustering: The "Cocktail Party Algorithm", allows you to find structure in a chaotic environment. (i.e. identifying individual voices and music from a mesh of sounds at a cocktail party).

# linear regression with one variable

- $x^{(i)}$ denote the "input" varialbes(**input features**)
- $y^{(i)}$ denote the "output varialbes"(**target variables**)
- m denote numbers of the traning examples 
- a pair $(x^{(i)}$ ,$y^{(i)})$ is called a **training example**,a list of it and i=1,...,m—is called a training set. 
- **X** denote  the space of input value, **Y** denote the space of input value. in this example,X=Y=$\mathbb{R}$

	To describe the supervised learning problem slightly more formally, our goal is, given a training set, to learn **a function h : X → Y** so that h(x) is a “good” predictor for the corresponding value of y. For historical reasons, this function h is called a **hypothesis**.
	

## hypothesis
$h_{\theta}(x)=\theta_0+\theta_{1}x$	 
$\theta_i$ denote parameters

x from $x^{(i)}$

target: choose $\theta_0,\theta_{1}$ so that  $h_{\theta}(x)$ is close to y for our tranning examples(x,y)

## cost function
$J(\theta_0,\theta_{1}) = \frac{1}{2m}\sum\limits_{i=1}^m(h_{\theta}(x^{(i)}-y^{(i)})^2$ 

goal: make $J(\theta_0,\theta_{1})$ minimize

This function is otherwise called the **"Squared error function"**, or **"Mean squared error"**. The mean is halved $(\frac{1}{2})$ as a convenience for the computation of the gradient descent, as the derivative term of the square function will cancel out the $(\frac{1}{2})$ term.

## gradient descent

we want min $J(\theta_0,\theta_{1})$
outline:

- start with some $\theta_0,\theta_{1}$
- keep changing $\theta_0,\theta_{1}$ to reduce  $J(\theta_0,\theta_{1})$ untill end up at a minimum

### gradient descent algorithm
 repeat untill convergence{

 $\theta_{j} := \theta_{j} - \alpha \frac{\partial}{\partial\theta_j}J(\theta_0,\theta_{1}))$  (for j =0 and j=1)

 }

 - **$\alpha$** : learning rate
		- a=0 do not work
		- a is very small,it will be too slow
		- a is very large,it will fail to convergence
	
 - **simultaneous update** $\theta_0 , \theta_1$

$\begin{align*} \text{repeat until convergence: } \lbrace & \newline \theta_0 := & \theta_0 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m}(h_\theta(x_{i}) - y_{i}) \newline \theta_1 := & \theta_1 - \alpha \frac{1}{m} \sum\limits_{i=1}^{m}\left((h_\theta(x_{i}) - y_{i}) x_{i}\right) \newline \rbrace& \end{align*}$

- why $\theta_0$ no need multiply $x_i$?
	
	> because the param of $\theta$ is 1

- why $\alpha \frac{\partial}{\partial\theta_j}J(\theta_0,\theta_{1}))$ transfer to 
$\alpha\frac{1}{m}\sum\limits_{i=1}^{m}((h_\theta(x_{i}) - y_{i}) x_{i})$

$\alpha \frac{\partial}{\partial\theta_j}J(\theta_0,\theta_{1}))$ 
 => $\alpha\frac{\partial}{\partial\theta_j}\frac{1}{2m}\sum\limits_{i=1}^m(h_{\theta}(x^{(i)}-y^{(i)})^2$

 same as:


$\frac{\partial}{\partial\theta_j}J(\theta_0,\theta_{1}))$ 
 => $\frac{\partial}{\partial\theta_j}\frac{1}{2m}\sum\limits_{i=1}^m(h_{\theta}(x^{(i)}-y^{(i)})^2$
 =>$\frac{1}{m}\sum\limits_{i=1}^m(h_{\theta}(x^{(i)}-y^{(i)})^{2}x_j^{(i)}）$

 when $\theta=0$.   $x_0^i$ =1

 > 此处证明过程略，**别忘了把学习速率a补上**

## Matrices and Vectors

### Scalar

a sigle vlaue 

### Matrices
$$
 \begin{bmatrix}
   1 & 2 & 3 \\
   4 & 5 & 6 \\
   7 & 8 & 9
  \end{bmatrix} 
$$

- denote by uppercase
- m*n (row col)
- $A_{ij}$ refter to ith row and jth col element.
- In general, all our vectors and matrices will be 1-indexed. Note that for some programming languages, the arrays are 0-indexed.


### vectors
$$
 \begin{bmatrix}
   1 \\
   4 \\
   7 
  \end{bmatrix}
$$

- denote by lowercase
- m*1 
- $v_i$ refer to the ith row element
- Matrices are usually denoted by uppercase names while vectors are lowercase.

### calculate
- addition 
- multiplication
- ...

#### matrix and vector multiplication

$\begin{bmatrix} a & b \newline c & d \newline e & f \end{bmatrix} *\begin{bmatrix} x \newline y \newline \end{bmatrix} =\begin{bmatrix} a*x + b*y \newline c*x + d*y \newline e*x + f*y\end{bmatrix}$

- the result is a vector
- colums of matrix must equal the rows of vector

#### matrix and matrix multiplication

$\begin{bmatrix} a & b \newline c & d \newline e & f \end{bmatrix} *\begin{bmatrix} w & x \newline y & z \newline \end{bmatrix} =\begin{bmatrix} a*w + b*y & a*x + b*z \newline c*w + d*y & c*x + d*z \newline e*w + f*y & e*x + f*z\end{bmatrix}$

- An m x n matrix multiplied by an n x o matrix results in an m x o matrix

#### matrix multiplicaton properties

$A * B \not= B * A$ (A or B is not I)

$(A * B)* C = A * (B* C)$

#### indentity matrix (I)

$\begin{bmatrix} 1 & 0 & 0 \newline 0 & 1 & 0 \newline 0 & 0 & 1 \newline \end{bmatrix}$

$A * I = I * A = A$

#### inverse and transpose 

- not all number have a inverse ,for example, 0.

##### matrix inverse

if A is an m*m matrix,and if it has an inverse

$A * A^{-1} = A^{-1} * A = I$

matrix that don't have an inverse called."singular" or "degenerate"

#### matrix transpose

$A = \begin{bmatrix} a & b \newline c & d \newline e & f \end{bmatrix}$

$A^T = \begin{bmatrix} a & c & e \newline b & d & f \newline \end{bmatrix}$

$A_{ij} = A^{T}_{ij}$