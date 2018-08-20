# Cost function and Backpropagation(反向传播)

## cost function 

- L = total number of layers in the network
- $s_l$  = number of units (not counting bias unit) in layer $l$
- K = number of output units/classes

　$J(\theta) =- \frac{1}{m}\sum\limits ^m_{i=1}[y^{(i)}log(h_\theta(x^{(i)}))+(1-y^{(i)})log(1-h_\theta(x^{(i)}))]+\frac{\lambda}{2m}\sum\limits^n_{j=1}\theta^2_j$

For neural networks, it is going to be slightly more complicated:

$J(\Theta) =- \frac{1}{m}\sum\limits ^m_{i=1}\sum\limits ^K_{k=1}[y_k^{(i)}log((h_\Theta(x^{(i)}))_k)+(1-y_k^{(i)})log(1-(h_\Theta(x^{(i)}))_k)]+\frac{\lambda}{2m}\sum\limits_{l=1}^{L-1}\sum\limits_{i=1}^{s_l}\sum\limits_{j=1}^{sl+1}(\Theta_{j,i}^{(l)})^2$



## Backpropagation Algorithm

"Backpropagation" is neural-network terminology for minimizing our cost function, just like what we were doing with gradient descent in logistic and linear regression. Our goal is to compute:
$min_\Theta J(\Theta)$

we use to compute the partial derivative of J(Θ):

To do so, we use the following algorithm:**Back propagation Algorithm**



Given training set $\lbrace (x^{(1)}, y^{(1)}) \cdots (x^{(m)}, y^{(m)})\rbrace$

- Set $\Delta^{(l)}_{i,j}$ := 0 for all (l,i,j), (hence you end up having a matrix full of zeros)

 For training example t =1 to m:



