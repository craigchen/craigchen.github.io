# 理解高维数组


在使用matlab或者python等语言进行数据处理时，高维数组是常用基本数据结构。
高维数组对应的数学概念就是张量(**tensor**)。在tensorflow和theano等机器学习框架中也使用tensor的概念。


Tensor可以理解为高维数组，在matlab中对高维数据做如下规定

- The first references array dimension 1, the row.
- The second references dimension 2, the column.
- The third references dimension 3. This illustration uses the concept of a page to represent dimensions 3 and higher.


这里用到了row，column，page等术语，可以将其可视化，参考[matlab官方文档](http://cn.mathworks.com/help/matlab/math/multidimensional-arrays.html)

![image](http://upload-images.jianshu.io/upload_images/273407-0c6d8611e7fcc6f0.gif?imageMogr2/auto-orient/strip)


问题是：如果有第4维呢？该如何想象？

row, column, page的概念还有一个缺陷在于，如果进行维数扩展或者进行转置（transpose）操作，不利于直观想象。



所以在阅读或使用高维数组时，[知乎网友](https://www.zhihu.com/question/29687900/answer/45302495)建议:



> 需要和高维数组(Tensor)打交道的话，思考时不要想着row, column, page这些术语, 要用*dim_1, dim_2,... dim_M* 来思考。好多地方说Matlab是先存column， 用我们的术语其实就是Matlab按照从左到右：dim_1, dim_2,... dim_M的顺序存储元素。例如想想下面 2 x 4 x 3 x 5 矩阵的存储顺序：


```
sz = [2, 4, 3, 5]; % dim_1 = 2, dim_2 = 4, dim_3 = 3, dim_4 = 5
A = reshape( 1 : prod(sz), sz );
```


### 语法糖
高维数组可以理解为语法糖，在存储的时候，还是按1维数组来存储的。



### 如何可视化高维数组

考虑一下这种方式, 

![image](https://qph.ec.quoracdn.net/main-qimg-3d4ccee98df63ddafc77a43dd5150f60?convert_to_webp=true)

来源[Quora: How do I visualize multidimensional arrays?](https://www.quora.com/How-do-I-visualize-multidimensional-arrays)


### 如何学习

遇上高维数组，画出数据结构，观察数据是如何组织的，知道你的大脑习惯这种数组组织形式。当在遇上其他高级数据结构时，清楚发生了什么。


拿出纸和笔，画出来！
