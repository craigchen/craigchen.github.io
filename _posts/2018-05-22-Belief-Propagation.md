# Belief Propagation

Bayes学派的基本观点是把概率看成一种信念(Belief), 而信念传播(Belief Propagation)是一种优雅的方法。BP
来源于图方法.

## 直观例子

参考 [Quora](https://www.quora.com/How-do-you-explain-the-belief-propagation-algorithm-in-Bayesian-networks) 中的例子，以期对这个问题有清晰的阐释。在概率图模型中变量节点(Variable
Node)和因子节点(Factor Node)的概念，用机器学习中的讲法分别对应简单节点和特征(Feature)。假设有一例子，有三个简单节点A、B、C和两个特征F1,F2.
已知$F_{1}(A,B)$和$F_{2}(B,C)$. 希望能计算出$P(A)$, $P(B)$, $P(C)$. 概率图和赋值如图所示:
![belief](image/Belief-propagation.jpeg "BP-example")


如果不用BP方法,
则可以计算$F_{1}(A,B)$和$F_{2}(B,C)$的联合概率分布$P_{12}(A,B,C)$, 再通过
$$
P(A)=\int_{C}\int_{B}P_{12}(A,B,C)dBdC
$$
的方式可以计算出来. 这是很朴素的想法, 然而面对高维问题, 这种方式很难凑效. 如果采用BP, 思路是这样的.

在BP方法里面, 每个节点发信息给相邻的feature, 而每个feature 也发信息给相邻的节点. 

1. 节点向特征发消息, 所有节点的发$[1\ 1]$消息, 即. 

$$
M_{A1}=M_{B1}=M_{B2}=M_{C2}=[1\ 1]
$$

2. $F_{1}$发消息到$A$, 记为$M_{1A}$消息为除$A$以外所有邻居的乘积, 本例中只有$B$, 对B积分(加)以后为:
$$
M_{1A}=\int F_{1}(A,B)dB=[3\ 6]=[1\ 2]
$$
, 同理, $F_{1}$发消息到$B$的消息为
$$
M_{1B}=\int F_{1}(A,B)dA=[1\ 2]
$$
. 同理, $F_{2}$发消息到$B$是
$$
M_{2B}=\int F_{2}(B,C)dC=[4\ 5]
$$
, $F_{2}$发消息到$C$是
$$
M_{2C}=\int F_{2}(B,C)dB=[1\ 2]
$$

3. 对于$A$和$C$, 分别只有$F_{1}$和$F_{2}$邻居,没有其他邻居, 则:$A$向$F_{1}$发消息$M_{A1}=[1\ 1]$,
$C$向$F_{2}$发消息$M_{C2}=[1\ 1]$, $B$向$F_{1}$发的信息是所有邻居($F_{2}$)发给$B$的信息,
为$M_{B1}=[4\ 5]$, 同理, $B$向$F_{2}$发的信息为$M_{B2}=[1\ 2]$

4. 特性再向节点发信息. $M_{1A}=\int F_{1}(A,B)M_{B1}dB=[1\ 2]$, $M_{1B}=\int F_{1}(A,B)M_{A1}dA=[1\ 2]$,
$M_{2B}=\int F_{2}(B,C)M_{C2}dC=[4\ 5]$. $M_{2C}=\int F_{2}(B,C)M_{B2}dB=[2\ 5]$.

5. 节点向特征发消息, $M_{B1}=M_{2B}=[4\ 5]$, $M_{B2}=M_{1B}=[1\ 2]$

6. 由于3和5已经相同, 停止迭代. 计算节点消息乘积
$$
\phi(A)=M_{1A}=[1\ 2]
$$
$$
\phi(B)=M_{1B}M_{2B}=[2\ 5]
$$
$$
\phi(C)=M_{2C}=[2\ 5]
$$

7. 写成概率形式形式
$$
P(A=0)=\frac{1}{3}
$$
$$
P(B=0)=P(C=0)=\frac{2}{7}
$$


## 严格表述

根据上面例子,引出消息更新的一般规则, $i$向$j$发消息
$$
m_{ij}(x_{j})\leftarrow\sum_{x_{i}}\phi_{i}(x_{i})\psi_{ij}(x_{i},x_{j})\prod_{k\in N(i)\backslash j}m_{ki}(x_{i})
$$
其中$\phi_{i}$是局部特征(证据), $\psi_{ij}$是联合特征. 节点belief计算
$$
b_{i}(x_{i})=k\phi_{i}(x_{i})\prod_{j\in N(i)}m_{ji}(x_{i})
$$


## 程序代码

参考[David Barber : Brml  Software](http://web4.cs.ucl.ac.uk/staff/D.Barber/pmwiki/pmwiki.php?n=Brml.Software)





