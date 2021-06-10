created by luowang 2021/6/1

##matlab学习笔记##

clc：清除命令窗口的内容

clear：清除工作空间的所有变量
clear all：清除工作空间的所有变量，函数，和MEX文件

hold on:用于添加新绘图的时候保留当前绘图

axis主要是用来对坐标轴进行一定的缩放操作，其操作命令主要如下：

axis( [xmin xmax ymin ymax] )  ：设置当前坐标轴 x轴 和 y轴的限制范围

axis( [xmin xmax ymin ymax zmin zmax cmin cmax] ) :设置 x,y,z轴的限制范围和色差范围

 axis on:打开所有的坐标轴标签、刻度、背景

grid:打开或显示网格（grid on   grid off)

view([x,y,z]):设置视点的函数,xyz为三个方向角

colormap([x,yz]):设置色图

 meshgrid 函数用来生成网格矩阵，可以是二维网格矩阵。

exp1_1:生成二维网格，用法为：[x y]=meshgrid(a b);  % a 和b是一维数组，如a=[1 2 3]; b= [2 3 4]; 则生成的 X 和 Y 都是为 3X3 维的矩阵，
>> [x y]=meshgrid(a,b)
>>  x =
>> 1     2     3
>> 1     2     3
>> 1     2     3
>>  y =
>>  2     2     2
>>  3     3     3
>>  4     4     4    

exp1_2:生成二维网格，用法为：[x y]=meshgrid(a b);  % a 和b是一维数组，如a=[1 2 3]; b= [2 3]; 则生成的 X 和 Y 都是为 3X2 维的矩阵，
>> [x y]=meshgrid(a,b)
>>  x =
>> 1     2     3
>> 1     2     3
>>  y =
>> 2     2     2
>> 3     3     3

exp1_3:生成二维网格，用法为：[x y]=meshgrid(a b);  % a 和b是一维数组，如a=[1 2]; b= [2 3 4]; 则生成的 X 和 Y 都是为 2X3 维的矩阵，
>> [x y]=meshgrid(a,b)
>>  x =
>> 1     2
>> 1     2
>> 1     2
>>  y =
>> 2     2
>> 3     3
>> 4     4



surf([x,y,z]):用来绘画三维曲面,xyz为坐标矩阵



linspace(x1,x2,N)　　

功能：linspace是Matlab中的一个指令，用于产生x1,x2之间的N点行矢量。其中x1、x2、N分别为起始值、中止值、元素个数。若缺省N，默认点数为100。在matlab的命令窗口下输入help linspace或者doc linspace可以获得该函数的帮助信息。

例：

　　在matlab的命令窗口输入：

​    X=linspace(1,100)

　　将产生从1到100步长为1的数组。类似于在命令窗口中输入：

　　X=[1:1:100]

\>>  X=linspace(1,100)

X =


 Columns 1 through 21


   1   2   3   4   5   6   7   8   9   10   11   12   13   14   15   16   17   18   19   20   21


 Columns 22 through 42


  22   23   24   25   26   27   28   29   30   31   32   33   34   35   36   37   38   39   40   41   42


 Columns 43 through 63


  43   44   45   46   47   48   49   50   51   52   53   54   55   56   57   58   59   60   61   62   63


 Columns 64 through 84


  64   65   66   67   68   69   70   71   72   73   74   75   76   77   78   79   80   81   82   83   84


 Columns 85 through 100


  85   86   87   88   89   90   91   92   93   94   95   96   97   98   99  100



plot3（x，y，z）：绘制三维曲线（https://blog.csdn.net/qq_39979317/article/details/105414923?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522162252156516780357253042%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=162252156516780357253042&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-105414923.first_rank_v2_pc_rank_v29&utm_term=matlab+plot3%E5%87%BD%E6%95%B0&spm=1018.2226.3001.4187）
其中
参数x、y、z组成一组曲线的坐标。



fplot3（funx，funy，funz，tlims）
其中
funx、funy、funz代表定义曲线x、y、z坐标的函数，通常采用函数句柄的形式。
tlims为参数函数自变量的取值范围，用二元向量[tmin，tmax]描述，默认为[-5，5]。

![image-20210601123225959](C:\Users\luowang\AppData\Roaming\Typora\typora-user-images\image-20210601123225959.png)

xt = @(t) exp(-t/10).*sin(5*t);

 yt = @(t) exp(-t/10).*cos(5*t); 

zt = @(t) t; 

fplot3(xt, yt, zt, [-12, 12])



delete()：删除文件或对象图形





Matlab动画制作(一)——电影动画

电影动画的好处就是，一次可以多次播放，甚至可以直接生成avi，直接独立与环境播放。这是其它三种动画制作方法所不具备的。

MATLAB中，创建电影动画的过程分为以下四步：

***\*step1：\****调用moviein对内存进行初始化(该步骤在Matlab5.3以上均可省略)，创建一个足够大的，使之能够容纳基于当前坐标轴大小的一系列指定的（此处称为帧）。

***\*step2：\****调用getframe函数生成每个帧。该函数返回一个列矢量，利用这个矢量，就可以创建一个电影动画矩阵。

getframe函数可以捕捉动画帧，并保存到矩阵中。一般将该函数放到for循环中得到一系列的动画帧。
该函数格式有：
(1)F=gefframe，从当前图形框中得到动画帧
(2)F=gefframe(h)，从图形句柄h中得到动画帧
(3)F=getframe(h，rect)，从图形句柄h的指定区域rec中得到动画帧

**step3：**调用movie函数按照指定的速度和次数运行该电影动画。

当创建了一系列的动画帧后，可以利用movie函数播放这些动画帧。
该函数的主要格式有：
(1)movie(M)，将矩阵M中的动画帧播放一次
(2)movie(M,n)，将矩阵M中的动画帧播放n次
(3)movie(M,n,fps)，将矩阵M中的动画帧以每秒fps帧的速度播放n次

***\*step4：\****调用movie2avi函数可以将矩阵中的一系列动画帧转换成文件avi文件。这样，即使脱离了matlab环境都可以播放动画。

具体参见：

该方法的经典格式是：

1. %录制电影动画
2. ​    for j=1:n
3. ​     %
4. ​     %这里我们的
5. ​     %
6. ​     M(j) = getframe;
7. ​    end
8. ​    movie(M)
9. %单帧显示方法
10. ​    f = getframe(gcf);
11. ​    colormap(f.colormap);
12. ​    image(f.cdata);





matlab在线编辑网站：https://octave-online.net/