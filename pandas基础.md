pandas tips
===========

Series
------

创建一个带有序号的一维数组，可通过s[index] 访问数据

     s = pd.Series([1,3,5,np.nan,6,8])

**Series的创建**

 - 通过一维数组：n = Series(arr), 指定索引：n = Series(arr, index = index_array)
 - 通过字典来创建：n = Series({'la':1,'ha':2,'hei':3})

**Series可以通过索引取值或者顺序序号取值**

 - Series['la'] 或者Series[0]
 - numpy的运算在Series中都保留

**Series缺失值检测**

 - pandas中的isnull或notnull函数可用于Series缺失值的检测 `pd.isnull(scores)`
 - numpy中的isnan可用于缺失值检测：`np.isnan(scores)`

**Series自动对齐**

不同Series间进行算术运算会自动对齐，相同索引的放在一起计算。

    price = pd.Series([1,2,3,4],index=['p1','p4','p3','p2'])
    table = pd.Series([4,5,6,7],index = ['p4','p3','p1','p2'])
    table*price   #得出的结果是索引相对齐后相乘的结果

DataFrame
---------

创建一个二维的，异构的，可变结构的数组。

    pd.DataFrame([[1,2,3],[4,5,6]]) 得到一个两行三列的矩阵，而且包含行和列序号

DataFrame 共六列，每列有四个随机数，其中index=dates将data作为序数，四列的列名分别为A，B，C，D。

    dates = pd.date_range('20130101', periods=6)  产生6个日期递增的日期
     df = pd.DataFrame(np.random.randn(6,4), index=dates, columns=list('ABCD'))


通过传入一个dict创建一个、dataFrame。

     df2 = pd.DataFrame({ 'A' : 1.,
						  'B' : pd.Timestamp('20130102'),
                          'C' : pd.Series(1,index=list(range(4)),dtype='float32'),
                          'D' : np.array([3] * 4,dtype='int32'),
                          'E' : pd.Categorical(["test","train","test","train"]),
                          'F' : 'foo' })

查看数据：

显示二维数组的前五列和最后五列

    df.head()
    df.tail()
    df.index  显示index内容，即年月日
    df.column 显示列名称，即ABCD
    df.values 显示表格内容
    df.describe() 对数据的描述，如平均值，最大最小值等
    df.T  二维数组的转置
    
按轴排序

    df.sort_index(axis=1, ascending=False) 结果按D,C,B,A逆序显示
    
根据值排序

    df.sort_values(by='B') 结果按B列值的升序排列

Selection 选择数据
---------
通过标签获取数据（index）

    df['A']  返回一个series，即包含index以及A的那一列
	df[1:3]  1,2列显示，左闭右开
	df['20130102':'20130104'] 选择index在这区间上的数据，包括边界
	df.loc[dates[0]] 选择一个index ，返回这个index行的值
	df.loc[:,['A','B']] 第一个参数设置index范围， ：表示显示所有的index，之后的['A','B'] 表示index对应的'A','B'
	 df.at[dates[0],'A'] 快速获取某个值

通过位置获取（position）

    df.iloc[3]  显示第三行的数据
    df.iloc[3:5,0:2] 选择第三，四行，前两列的数据显示
    df.iloc[[1,2,4],[0,2]] 选择1,2,4行的0,2列显示
    df.iloc[1:3,:] 选择1到3行的所有列显示
    df.iloc[1,1] 选择某个位置的值
    df.iat[1,1] 快速定位，与上面的方法相同

Boolean indexing
----------------

通过一些判断运算符计算出满足要求的列

    df[df.A > 0]  A列中大于0的那一行将会显示
    df[df>0] 显示出列中大于0的元素，如不满足，则显示为NAN
    df2[df2['E'].isin(['two','four'])] E列中满足two，或four的行显示出来
    

Setting
-------

自动生成一列

    df['E'] = ['one', 'one','two','three','four','three']
    s1 = pd.Series([1,2,3,4,5,6], index=pd.date_range('20130102', periods=6))
    df['F'] = s1 元素将按照index的位置插入相应的行中

通过label来设置相应位置的值

    df.at[dates[0],'A'] = 0
    df.iat[0,1] = 0  通过位置设值
    df.loc[:,'D'] = np.array([5] * len(df)) 通过numpy设置
    df[df > 0] = -df  将所有整数变为负数
    
数据缺失用nan表示，取出含nan的行

    df.dropna(how='any')
    df.fillna(values = '5') 将表中nan的元素填充为5
    pd.isna(df)  将表格变为bool类型，是nan为true，否则为false
    

Operation
---------

    df.mean() 计算每一列的平均值
    df.mean(1) 计算每一行的平均值
    s = pd.Series([1,3,5,np.nan,6,8], index=dates).shift(2) 将值按顺序移动两个，用于不同维度的对齐操作
    df.sub(s,axis='index') 不同维度的减法操作，如果s中含有nan，相减的结果也为nan

Apply
-----

对数据应用一些函数

    df.apply(np.cumsum) 返回一路上的累加的数值，[1,2,3] 返回[1,3,6]
    df.apply(lambda x: x.max() - x.min())

Histograming
------------

    s = pd.Series(np.random.randint(0, 7, size=10)) 返回一列，十个数，数值在0到7
    s.value_counts() 对不同的数值进行统计

String method
-------------
对一些String的元素进行一下操作

    s.str.lower() 大写变小写

Merge 合并
--------

    s = [s1,s2] 这样合并的s有两个列名
    pd.concat(s) 用于合并s，使得s变成真正的一个表
    left = pd.DataFrame({'key': ['foo', 'foo'], 'lval': [1, 2]})
    right = pd.DataFrame({'key': ['foo', 'foo'], 'rval': [4, 5]})
    pd.merge(left, right, on='key')

Append
------

    df.append(s, ignore_index=True) 将s添加到df尾巴，并忽视其原来的index

Grouping
--------

    df.groupby('A').sum() 对A列进行合并同类，其他类相加
    df.groupby(['A','B']).sum()
     

Categoricals 类型
------------

这个变量类型指的是明确的，固有的类型，有点类似于下拉列表的选项

    df["grade"].cat.categories = ["very good", "good", "very bad"]

Plotting
--------

    ts = pd.Series(np.random.randn(1000), index=pd.date_range('1/1/2000', periods=1000))
    ts.cumsum()
    ts.plot()

Get data in/out
---------------

**CSV**

    df.to_csv('foo.csv') 写到csv中去
    pd.read_csv('foo.csv') 从csv中读出来

**HDF5**

pandas的压缩文件，是一个类似字典对象的一个文件

    df.to_hdf('foo.h5','df') 写文件
    pd.read_hdf('foo.h5','df') 读文件
    store = pd.HDFStore('store.h5')
    store['data'] = df 类似于dict的方式对文件进行存取

Excel
-----

    df.to_excel('foo.xlsx', sheet_name='Sheet1') 写excel
    pd.read_excel('foo.xlsx', 'Sheet1', index_col=None, na_values=['NA']) 读excel
    