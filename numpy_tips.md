numpy 知识点
=========

numpy 是一个python的开源数值计算扩展包。其包括：

1. **ndarray**：一个具有矢量计算运算和复2杂广播能力的快速且节约空间的多维数组

2. **ufunc**：对整组数据进行快速运算的标准数学函数

3. **工具包**：用于整合C/C++和Fortran代码

4. 使用的线代，傅里叶变换和随机生成函数。numpy与稀疏矩阵运算宝scipy配合使用更方便。

ndarray介绍
---------

 - n dimensional array
 - 一个array中的元素为相同类型
 - 元素的类型由dtype对象指定
 - 大小固定，一旦创建好就不会改变

**ndarray 属性**

1. ndim表示维度的数量
2. shape 各维度大小的元组（类似于长宽高）
3. dtype 说明数组数据类型的对象
4. size 元素的总个数

例如：

    a = np.array([
    [
	    [1,2,3,4],
	    [1,2,3,4]
    ],
    [
	    [1,2,3,4],
	    [1,2,3,4]
    ],
    [
	    [1,2,3,4],
	    [1,2,3,4]
    ]
    ])

通过这种方式取数据：a[0][0][0]

**ndarray的常见创建方式**

 - array函数：接受一个普通的list转化为ndarray，如上例
 - zeros函数：创建指定长度或形状的全零数组。 `a= np.zeros((3,4))` 三行四列，全为0的数组
 - ones函数：创建指定长度或形状全为1的数组。 `a= np.ones((3,4))` 三行四列，全为1的数组
 - empty函数：创建一个没有任何具体值的数组  `a = np.empty((2,3,4))`
 - arange 函数：`a = arange(0,20,1)` 通过指定开始值，终值，步长的方式创建以为数组，注意数组不包含终值。`a = np.arange(12).reshape(3,4)`
 - linspace函数：通过指定开始值，终值和元素个数来创建一维数组，可以通过endpoint关键字指定是否包括终值，缺省设置和包括终值。`a = np.linspace(0,10,5,endpoint=True)` 在0到10中桶步长取出五个数，其中endpoint=True表示10也在结果中
 - logspace函数与linspace相似，`np.logspace(0,2,5)` 表示0到10的2次方之间取5个数
 - 使用随机数 `a = np.random.random((2,2,4))` 可以产生三维数组，内容随机

**numpy的数据类型**

1. a.dtype ： 返回数据类型
2. b = a.astype('int32') ：转化数据类型返回一个新的array

**改变ndarray的形状**

 - 直接改变ndarray的shape值 `a.shape = 5,-1` 将a的行改为5行，-1表示列将自动计算
 - 通过reshape函数，可以创建一个改变了尺寸的新数组，但是新数组与原数组公用内存，修改将对会两个都其作用 b = a.reshape(5,2)

**numpy的基本操作**

 - 数组与标量之间的运算： 数组不用循环即可对每个元素执行批量运算，这称为**矢量化**。a = a + 2 将会对a中每个元素都加上2。
 - 数组矩阵积：即矩阵间的点乘。 `np.dot(arr,arr2)`
 - numpy数组的切片：例如a[1,:,1:3] 其中冒号表示那一维的数据都要

**布尔型索引**

 - `a[a<10]` 返回a中所有小于10的数，组成一个array返回
 - a<10 ：将返回一个与原数组维度相同的数组，但是内容为True或False

**数组转置与轴对称**

 - a.T
 - a.transpose() 返回一个转置后的数组

**ufunc**：一种对ndarray中的数据执行元素级运算的函数

 - np.sqrt(arr)  求arr的开方
 - substract(a,b) a数组减去b数组
 - 等等

**聚合函数**：对一组值进行操作，返回一个值。

 - arr.max()
 - arr.mean() 等等

**np.where 函数**：三元表达式 x if condition else y

 - `result = [(x if c else y) for x,y,c in zip(xarr,yarr,condition)]` 等价于 `np.where(condition,xarr,yarr)`
 - np.uinque(arr) 返回arr中仅出现过一次的元素
 
 **存取文本文件**

    np.savetxt('test.csv',x,delimiter=',')
    np.getfromtxt('data.csv',delimiter',',names=True)