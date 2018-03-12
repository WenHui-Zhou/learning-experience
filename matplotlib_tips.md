matplotlib tips
===============

python 中最著名的绘图库，十分适用于交互式制图。

**figure 和 subplot**

matplotlib 的图像都位于Figure对象中，Figure对象下创建一个或多个subplot（axes）用于绘制图表

    import matplotlib.pyplot as plt
    import numpy as np
    #设置中文和负号
    from pylab import mpl
    mpl.rcParams['font.sans-serif'] = ['FangSong']
    mpl.rcParams['axes.unicode_minus'] = False
    #获得figure 对象
    fig = plt.figure(figsize=(8,6))
    #在figure对象上创建axes对象
    ax1 = fig.add_subplot(3,2,1)
    ax2 = fig.add_subplot(3,2,2)
    ax3 = fig.add_subplot(3,2,3)
    plt.plot(np.random.randn(50).cumsum(),'k--')
    ax1.hist(np.random.randn(300),bins = 20,color='k',alpha = 0.3)
    ax2.scatter(np.arange(30),np.arange(30)+3*np.random.randn(30))
    plt.show()

在matplotlib中绘图，主要使用plt.plot() 在plot中准备数据，设置x,y轴，以及图像样式等一些属性。

**matplotlib 正常显示中文以及负号**

    import matplotlib.pyplot as plt
    plt.rcParams['font.sans-serif'] = ['SimHei'] #正常显示中文
    plt.rcParams['axes.unicode_minus']=False#用于正常显示负号

基础
--

    plt.plot(np.random.randn(10))

向plot中提供一组一维的数组，那么matplotlib将默认它为一系列的y值，并由0开始自动生成一系列的x值[0,1,2,3...]，与y的长度相同。

**确定坐标的范围：**

    plt.axis([xmin,xmax,ymin,ymax])
    xlim([xmin,xmax]) #调整x轴
    ylim([ymin,ymax]) #调整y轴

**叠加图：**用一条指令画多条不同格式的线

    import numpy as np
    import matplotlib.pyplot as plt
     
    # evenly sampled time at 200ms intervals
    t = np.arange(0., 5., 0.2)
     
    # red dashes, blue squares and green triangles
    plt.plot(t, t, 'r--', t, t**2, 'bs', t, t**3, 'g^')
    plt.show()

其中plot中三个参数一组，表示x，y，图案的样式。

**plt.figure()：**用它来产生多张图，图片按顺序增加，所有的操作仅对当前图和当前坐标有效。

    import matplotlib.pyplot as plt
    plt.figure(1)                # 第一张图
    plt.subplot(211)             # 第一张图中的第一张子图
    plt.plot([1,2,3])
    plt.subplot(212)             # 第一张图中的第二张子图
    plt.plot([4,5,6])
     
     
    plt.figure(2)                # 第二张图
    plt.plot([4,5,6])            # 默认创建子图subplot(111)
     
    plt.figure(1)                # 切换到figure 1 ; 子图subplot(212)仍旧是当前图
    plt.subplot(211)             # 令子图subplot(211)成为figure1的当前图
    plt.title('Easy as 1,2,3')   # 添加subplot 211 的标题

其中plt.subplot(211) ： 211表示figure中共有两列，一行，现在正在画的第一个位置上的图。

**plt.text() 添加文字说明**

import numpy as np
import matplotlib.pyplot as plt
 
mu, sigma = 100, 15
x = mu + sigma * np.random.randn(10000)
 
# 数据的直方图

    n, bins, patches = plt.hist(x, 50, normed=1, facecolor='g', alpha=0.75)
    plt.xlabel('Smarts')  #x坐标
    plt.ylabel('Probability') #y坐标
    #添加标题
    plt.title('Histogram of IQ')
    #添加文字
    plt.text(60, .025, r'$mu=100, sigma=15$')
    plt.axis([40, 160, 0, 0.03])
    plt.grid(True)
    plt.show()

其中plt.hist() 参数由 arr 一维数组，bins 直方图柱数，normed 是否归一化等组成

**plt.annotate() 文本注释：**

    import numpy as np
    import matplotlib.pyplot as plt
    ax = plt.subplot(111)
    t = np.arange(0.0, 5.0, 0.01)
    s = np.cos(2*np.pi*t)
    line, = plt.plot(t, s, lw=2) 
    plt.annotate('local max', xy=(2, 1), xytext=(3, 1.5),
    arrowprops=dict(facecolor='black', shrink=0.05),  )     
    plt.ylim(-2,2)
    plt.show()

**plt.xticks()/plt.yticks()设置轴记号**

    # 导入 matplotlib 的所有内容（nympy 可以用 np 这个名字来使用）
    from pylab import *
     
    # 创建一个 8 * 6 点（point）的图，并设置分辨率为 80
    
        figure(figsize=(8,6), dpi=80)
    # 创建一个新的 1 * 1 的子图，接下来的图样绘制在其中的第 1 块（也是唯一的一块）
    subplot(1,1,1)
    X = np.linspace(-np.pi, np.pi, 256,endpoint=True)
    C,S = np.cos(X), np.sin(X)
    # 绘制余弦曲线，使用蓝色的、连续的、宽度为 1 （像素）的线条
    plot(X, C, color="blue", linewidth=1.0, linestyle="-")
    # 绘制正弦曲线，使用绿色的、连续的、宽度为 1 （像素）的线条
    plot(X, S, color="r", lw=4.0, linestyle="-")
    plt.axis([-4,4,-1.2,1.2])
    # 设置轴记号
    xticks([-np.pi, -np.pi/2, 0, np.pi/2, np.pi],
    [r'$-pi$', r'$-pi/2$', r'$0$', r'$+pi/2$', r'$+pi$'])
    yticks([-1, 0, +1],[r'$-1$', r'$0$', r'$+1$'])
    # 在屏幕上显示
    show()