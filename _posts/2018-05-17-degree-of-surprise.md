# 拍案惊奇
## 如何理解Entropy

Entropy, Cross Entropy, KL divergence如何理解，各方能让有不同的理解方式。Quora上的讨论有代表性。[Quora1](https://top.quora.com/What-is-a-good-laymans-explanation-for-the-Kullback-Leibler-divergence)
[Quora2](https://www.quora.com/Whats-an-intuitive-way-to-think-of-cross-entropy)总结起来，有bit学说/编码学说，惊奇学说/兴趣学说，等等，不一而足。我倾向于惊奇学说，因为它把概率看成是一种belief，大概率事件发生是稀松平常的事。不稀罕。定义惊奇度的概念(degree
of surprisingness)
$$
\log_{2}\frac{1}{p}
$$
如果p发生的概率是为1，则$\log_{2}1/p$=0 即没什么可惊奇的。

$$
\log_{2}(\frac{1}{0.5p})=\log_{2}(\frac{1}{p})+1
$$
表明概率小一半，其发生时惊奇度增加1个单位。

有了惊奇度的概念再来看Entropy。比如有两颗骰子，一颗公平(fair), 一个不公平(loaded)。我掷公平的骰子，我认为(期望)你有都惊奇呢？

$$
\mathcal{H}(P_{fair})=\sum_{n=1}^{6}P_{fair}(n)\log_{2}(\frac{1}{P_{fair}(n)})\approx2.58
$$
掷骰子会发生6种事件：掷出1-6点，掷出每点的实际概率$\times$每点发生的惊奇度的总和则是期望惊奇度。

另一种情况，这次我迷糊了，还是这颗骰子，但我以为它是不公平的那颗，这是我期望的惊奇度是：
$$
\mathcal{H}(P_{fair},P_{loaded})=\sum_{n=1}^{6}P_{fair}(n)\log_{2}(\frac{1}{P_{loaded}(n)})\approx4.73
$$

对比着两个数，$\mathcal{H}(P_{fair})=2.58$, 惊奇度意味着什么呢？实际上他意味着这颗公平的骰子能引发的最小惊奇了，要最小惊奇，前提是知道他的真实概率。而一旦我以为它是别的概率，那出来的结果会令我匪夷所思，自然惊奇度就高了。

同理，我掷不公平的骰子给你，其最小惊奇度是
$$
\mathcal{H}(P_{loaded})=\sum_{n=1}^{6}P_{loaded}(n)\log_{2}(\frac{1}{P_{loaded}(n)})\approx0.7
$$
而一旦误以为这是一颗公平的骰子，那指出来之后的惊奇度则是
$$
\mathcal{H}(P_{loaded},P_{fair})=\sum_{n=1}^{6}P_{loaded}(n)\log_{2}(\frac{1}{P_{fair}(n)})\approx2.58
$$
惊奇程度更高。

而这种惊奇程度的差异则是KL divergence，

$$
\mathcal{D}_{KL}(P_{fair}||P_{loaded})=\mathcal{H}(P_{fair},P_{loaded})-\mathcal{H}(P_{fair})=2.15
$$
这表明这颗公平的骰子，我认为他是某个不公平的骰子概率带来的惊奇程度和知道实际概率带来的惊奇程度的差异。有读者可能注意到$\mathcal{H}(P_{loaded},P_{fair})$和$\mathcal{H}(P_{fair})$是一样的，就起原因是$P_{fair}$是是均一分布。

## GPS方法中的KL

在GPS方法中的优化目标表示为:

$$
-D_{KL}(\hat{p}(\tau)||p(\tau))
$$
其中, $\hat{p}(\tau)$是施加控制能够获得的轨迹概率，$p(\tau)$是理想最优轨迹的概率，使KL最小的是最优策略。寻找这个定义的本来面目

我们这个是可以
$$p(\tau)  =  p(\mathcal{O}_{t}=1|s_{t},a_{t})=\exp(r(s_{t},a_{t}))$$
