neron : 神经元
dendrite : 树突
cell body ：细胞体
nucleus :细胞核
axon ：轴突
myelin sheath ：髓鞘
schwann cell ：施万细胞
node of ranvier ：郎维结
axon terminal ：轴突终末


# Neural Networks

## Model Representation

Let's examine how we will represent a hypothesis function using neural networks.

At a very simple level, neurons are basically computational units that take inputs (**dendrites**) as electrical inputs (called "spikes") that are channeled to outputs (**axons**).

In our model, our dendrites are like the **input features**  $x_1\cdots x_n$, and the output is the result of our **hypothesis function.** 

- In this model our $x_0$ input node is sometimes called the **"bias unit."** It is always **equal to 1**.
- In neural networks, we use the same logistic function as in classification, $\frac{1}{1 + e^{-\theta^Tx}}$, yet we sometimes call it a **sigmoid (logistic) **activation function. 
- our "theta" parameters are sometimes called **"weights"**.



Visually, a simplistic representation looks like:

$\begin{bmatrix}x_0 \newline x_1 \newline x_2 \newline \end{bmatrix}\rightarrow\begin{bmatrix}\ \ \ \newline \end{bmatrix}\rightarrow h_\theta(x)$



- input : layer 1(input layer)

- hidden layer -  between the input and output layers

- Output layer -outputs the hypothesis function

- we label these intermediate or "hidden" layer nodes $a^2_0 \cdots a^2_n$and call them **"activation units."**

  

$\begin{align*}& a_i^{(j)} = \text{"activation" of unit $i$ in layer $j$} \newline& \Theta^{(j)} = \text{matrix of weights controlling function mapping from layer $j$ to layer $j+1$}\end{align*}$



If we had one hidden layer, it would look like:

$\begin{bmatrix}x_0 \newline x_1 \newline x_2 \newline x_3\end{bmatrix}\rightarrow\begin{bmatrix}a_1^{(2)} \newline a_2^{(2)} \newline a_3^{(2)} \newline \end{bmatrix}\rightarrow h_\theta(x)$


The values for each of the "activation" nodes is obtained as follows:
$\begin{align*} a_1^{(2)} = g(\Theta_{10}^{(1)}x_0 + \Theta_{11}^{(1)}x_1 + \Theta_{12}^{(1)}x_2 + \Theta_{13}^{(1)}x_3) \newline a_2^{(2)} = g(\Theta_{20}^{(1)}x_0 + \Theta_{21}^{(1)}x_1 + \Theta_{22}^{(1)}x_2 + \Theta_{23}^{(1)}x_3) \newline a_3^{(2)} = g(\Theta_{30}^{(1)}x_0 + \Theta_{31}^{(1)}x_1 + \Theta_{32}^{(1)}x_2 + \Theta_{33}^{(1)}x_3) \newline h_\Theta(x) = a_1^{(3)} = g(\Theta_{10}^{(2)}a_0^{(2)} + \Theta_{11}^{(2)}a_1^{(2)} + \Theta_{12}^{(2)}a_2^{(2)} + \Theta_{13}^{(2)}a_3^{(2)}) \newline \end{align*}$

This is saying that we compute our activation nodes by using a 3×4 matrix of parameters. We apply each row of the parameters to our inputs to obtain the value for one activation node. Our hypothesis output is the logistic function applied to the sum of the values of our activation nodes, which have been multiplied by yet another parameter matrix $ \Theta^{(2)}$
containing the weights for our second layer of nodes.



- Each layer gets its own matrix of weights,$ \Theta^{(j)}$  **j is the layer**.
- The dimensions of these matrices of weights is determined as follows:
  - $s_j$ : units in layer j  
  - $s_{j+1}$ : units in layer j+1,
  - $\Theta^j = s_{j+1} \cdot (s_j+1)$
  - 加1 的原因是，加上$x_0$

**向前传播**

## Examples and Intuitions

- AND  a= 1 and b=1 
- OR.  a=1 or b =1
- NOR not a and not b (a=b=0)  **或非**(有1出0，全0出1) 
- XNOR （a=b => True） ,（ a$\neq$b =>  False） (a=b=1 or a=b=0) **异或非**

AND  ---|

​		—— OR ——XNOR

NOR   ---|

-  we have the XNOR operator using **a hidden layer with two nodes!**
- AND OR NOR can only use a unit.
- The layer both is 3layers

**$x_1$ and $x_2$**

$\begin{align*}\begin{bmatrix}x_0 \newline x_1 \newline x_2\end{bmatrix} \rightarrow\begin{bmatrix}g(z^{(2)})\end{bmatrix} \rightarrow h_\Theta(x)\end{align*}$

$\Theta^{(1)}$ =[−30 20 20]

**Remember that x_0x0 is our bias variable and is always 1.**

This will cause the output of our hypothesis to only be positive if both $x_1$ and $x_2$ are 1. In other words:

$\begin{align*}& h_\Theta(x) = g(-30 + 20x_1 + 20x_2) \newline \newline & x_1 = 0 \ \ and \ \ x_2 = 0 \ \ then \ \ g(-30) \approx 0 \newline & x_1 = 0 \ \ and \ \ x_2 = 1 \ \ then \ \ g(-10) \approx 0 \newline & x_1 = 1 \ \ and \ \ x_2 = 0 \ \ then \ \ g(-10) \approx 0 \newline & x_1 = 1 \ \ and \ \ x_2 = 1 \ \ then \ \ g(10) \approx 1\end{align*}$



## Multiclass Classification

To classify data into multiple classes, we let our hypothesis function return a vector of values. Say we wanted to classify our data into one of four final resulting classes:

$\begin{align*}\begin{bmatrix}x_0 \newline x_1 \newline x_2 \newline\cdots \newline x_n\end{bmatrix} \rightarrow\begin{bmatrix}a_0^{(2)} \newline a_1^{(2)} \newline a_2^{(2)} \newline\cdots\end{bmatrix} \rightarrow\begin{bmatrix}a_0^{(3)} \newline a_1^{(3)} \newline a_2^{(3)} \newline\cdots\end{bmatrix} \rightarrow \cdots \rightarrow\begin{bmatrix}h_\Theta(x)_1 \newline h_\Theta(x)_2 \newline h_\Theta(x)_3 \newline h_\Theta(x)_4 \newline\end{bmatrix} \rightarrow\end{align*}$

Our final layer of nodes, when multiplied by its theta matrix, will result in another vector, on which we will apply the g() logistic function to get a vector of hypothesis values.

Our resulting hypothesis for one set of inputs may look like:
$h_\Theta(x) =\begin{bmatrix}0 \newline 0 \newline 1 \newline 0 \newline\end{bmatrix}$

Our final value of our hypothesis for a set of inputs will be one of the elements in y.