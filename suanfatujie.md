# 二分查找

> Conditions：
>
> - 仅当列表为有序的时候，二分查找才管用。

```python
def binary_search(list, item):
  low = 0
  high = len(list)—1
  while low <= high:
    mid = (low + high)
    guess = list[mid]
    if guess == item:
      return mid
    if guess > item:
      high = mid - 1
    else:
      low = mid + 1
  return None
# 例如
my_list = [1, 3, 5, 7, 9]
print binary_search(my_list, 3) # => 1
print binary_search(my_list, -1) # => None
```

## 线性时间

> 概念：逐个查找所求元素，查找猜测的次数与列表长度相同，这种称为线性时间。

## 对数时间

> 二分查找的运行时间为对数时间（或log时间）

![image-20220903201323711](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903201323711.png)

# 大O表示法

## 增速差异

​	随着元素数量的增多，二分查找和简单查找所增加的额外时间并不相同，

![image-20220903201753331](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903201753331.png)![image-20220903201803440](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903201803440.png)

因此在选择算法的时候，要知道算法具体的运行时间，还要知道运行时间如何随着列表增长而增加，从而有了大O表示法。

​	大O表示法指出了算法有多快。假设简单查找n个元素，则需要执行n个操作，用大O表示法，这个运行时间为O(n)。

> 大O表示法指的并非以秒为单位的速度。大O表示法让你能够比较操作数，他指出了算法运行时间的增速。二分查找则表示为：O(logn)

![image-20220903202432362](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903202432362.png)

​	大O表示法所指出的是可能出现的最糟的情况，最多的运行时间，同时需要考虑到平均情况的运行时间。

## 一些常见的大O运行时间

![image-20220903203322400](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903203322400.png)

- 算法的速度并非指的是时间，而是操作数的增速
- 谈论一个算法的速度的时候，是看随着输入的增加，运行时间以什么样的速度增加

## 旅行商问题

![image-20220903203907459](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903203907459.png)

one businessman want to go five places

![image-20220903204045746](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903204045746.png)![image-20220903204052238](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903204052238.png)

​	5个城市有5！种排列组合，需要120中操作，n个城市，则为n!次操作，大O指示法：O(n!)。目前还没有更快的算法。

## 小结

- 算法运行时间并不以秒为单位。
- 算法运行时间是从其增速的角度度量的。
- 算法运行时间用大O表示法表示。

# 选择排序

## 内存的工作原理

> 下方一个寄存柜有很多个柜子：
>
> ![image-20220903204751854](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903204751854.png)
>
> 每一个抽屉可以放一样东西，你有两样东西要寄存，因此要来了两个抽屉。![image-20220903204859840](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903204859840.png)
>
> 寄存完毕：
>
> ![image-20220903204929499](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903204929499.png)![image-20220903204937975](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903204937975.png)
>
> **计算机就是很多抽屉的集合，每一个抽屉都有地址。**

![image-20220903205122827](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903205122827.png)![image-20220903205126323](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903205126323.png)

​	需要存储多项数据时，有两种基本方式——数组和链表，但它们之间相差很大。

## 数组和链表

​	假设要把待办事项储存在内存中：

- 如果使用数组，代表所有的代办事项在内存中都是相连接的，紧靠在一起。

![image-20220903205434910](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903205434910.png)![image-20220903205449399](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903205449399.png)

​	假设此时他人占用了四个待办事项中的最后一个位置，则需要重新请求计算机分配一块可容纳4个待办事项的内存，再将所有待办事项移动至新空间。如果再有占用，则又要重新转移，添加同样是如此，但可以通过预留座位的方式，让计算机提前提供空间，但有缺点如下：

- 预留的空间可能用不上，造成内存的浪费，白白占用。
- 尽管有预留，但是预留满了之后仍需要转移。

### 链表

> - 链表中的元素可以储存在内存的任何地方。![image-20220903210221946](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903210221946.png)![image-20220903210227973](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903210227973.png)
>
> - 链表的每个元素都存储了下一个元素的地址，从而使得一系列随机的内存地址串在一起。

​	这犹如寻宝游戏。你前往第一个地址，那里有一张纸条写着“下一个元素的地址为123”。因此，你前往地址123，那里又有一张纸条，写着“下一个元素的地址为847“。

​	在链表中添加元素很简单：只需要将其放入内存，并将其地址存储到前一个元素中。

​	链表相当于在电影院6个人不能在一起坐的时候，提出“我们分开来坐”。因此不用担心没有足够的内存空间。

​	链表的缺点：

- 当你需要访问链表最后一个元素的时候，不可以直接读取，必须从第一个元素，再第二个元素依次直到访问到最后一个元素。

- 同时访问全部元素的时候，链表的效率很高；访问单个元素的时候，链表的效率很低。

### 数组

​	在排行榜网站上，一个页面显示不全所有的信息，想要找到第一名要翻查到最后，这体现了链表的缺点，相反数组的效率高了起来。

### 数组和链表区别

![image-20220903211911618](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903211911618.png)

​	从中间插入元素时，链表更为方便，如下将”买茶叶“添加到待办事项。

![image-20220903212226591](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903212226591.png)

链表：![image-20220903212230976](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903212230976.png)

数组：

![image-20220903212242232](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903212242232.png)

### 删除

​	删除元素的更好选择也是链表，只需要更改前一个元素所指向的地址即可，若使用数组则需要将其他元素向前移动。![image-20220903212741939](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220903212741939.png)

### 专业术语

- 索引：元素的位置，从0开始。
- 顺序访问和随机访问：链表只能顺序访问；数组支持随机访问。

### 选择排序

- 遍历数组，一遍一遍找到最大值，进行排序

  - 大O表示法：假设有n个元素，则每个元素都需要遍历整个数组O(n)，需要总的时间O(n2)
  - ![image-20220904095822394](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904095822394.png)![image-20220904095934249](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904095934249.png)
  - 需要检查的元素越来越少
    - 随着排序的进行，每次需要检查的元素数在逐渐减少，最后一次需要检查的元素都只有一个。既然如此，运行时间怎么还是O(n2)呢？这个问题问得好，这与大O表示法中的常数相关。第4章将详细解释，这里只简单地说一说。你说得没错，并非每次都需要检查n个元素。第一次需要检查n个元素，但随后检查的元素
      数依次为n -1, n – 2, …, 2和1。平均每次检查的元素数为1/2 × n，因此运行时间为O(n × 1/2 × n)。但大O表示法省略诸如1/2这样的常数（有关这方面的完整讨论，请参阅第4章），因此简单地写作O(n × n)或O(n2)。
  - 是一种灵巧的算法，但是速度不是很快。

- 快速排序：

  - 运行时间：O(n log n)

  - For example：

    - ```python
      def findSmallest(arr):
        smallest = arr[0] //储存最小值
        smallest_index = 0 //储存最小值的索引
        for i in range(1, len(arr)):
          if arr[i] < smallest:
            smallest = arr[i]
            smallest_index = i
        return smallest_index
      ```

      现在使用上面这个函数来编写排序算法：

      ```python
      def selectionSort(arr):
        newArr = []
        for i in range(len(arr)):
            smallest = findSmallest(arr)
            newArr.append(arr.pop(smallest))
      return newArr
      print selectionSort([5, 3, 6, 2, 10])
      ```

      

### 小结

- 数组用的更多。
- 同一数组中，所有元素的类型必须相同。

# 递归

​	**“俄罗斯套娃”**

- ![image-20220904101339316](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904101339316.png)![image-20220904101350234](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904101350234.png)![image-20220904101407737](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904101407737.png)

- 盒中有盒，要找到某个盒子中的钥匙，有以下两种办法：

  - 方法①![image-20220904101414595](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904101414595.png)

  - 方法②![image-20220904101701179](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904101701179.png)

  - 方法的程序表示：

    - 方法①：使用的是while循环，盒中不为空，则继续查找，对应while循环不为假则继续执行。
    ```python
      def look_for_key(main_box):
        pile=main_box.make_a_pile_to_look_through()
        while pile is not empty:
          box = pile.grab_a_box()
          for item in box:
           if item.is_a_box():
             pile.append(item)
           elif item.is_a_key():
             print "found the key!"
    ```

      

    - 方法②：

      ```python
      def look_for_key(box):
        for item in box:
          if item.is_a_box():
            look_for_key(item)
        elif item.is_a_key():
          print "found the key!"
      ```

  - 总结：循环使得程序的性能可能更高；但是使用递归，程序可能更容易理解。
  
## 基线条件和递归条件

  ​	编写递归函数时，必须告诉函数何时停止递归。因此，每个递归函数都有两部分：基线条件（base case）和递归条件（recursive case）。

  - 递归条件是指函数调用自己。
  - 基线条件是指函数不再调用自己，从而避免陷入死循环。
  
     只有递归条件：

  ```python
  def countdown(i):
      print i
      countdown(i-1)
  ```

既有递归条件也有基线条件：

  ```python
  def countdown(i):
      print i
      if i<=0
       return   //基线条件
      else
       countdown(i-1) //递归条件
  ```

  ![image-20220904103707131](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904103707131.png)![image-20220904103714155](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904103714155.png)

## 栈

​	调用栈（call stack），举例待办事项清单：

​	栈的压入和弹出，对应（插入）（删除并读取）。

![image-20220904104305913](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904104305913.png)![image-20220904104316101](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904104316101.png)

​	![image-20220904104508850](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904104508850.png)![image-20220904104536592](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904104536592.png)

​	这种数据结构成为栈，，一种简单的数据结构

## 调用栈

​	计算机在内部使用被称为调用栈的栈。

```python
def greet(name):
    print "hello, " + name + "!"
    greet2(name)
    print "getting ready to say bye..."
    bye()
```

   这个函数问候用户，再调用另外两个函数。这两个函数代码如下。

```python
def greet2(name):
	print "how are you, " + name + "?"
def bye():
print "ok bye!"
```

  假设调用greet(“maggle”），计算机首先为该函数调用分配一块内存。

  变量名name被设置为maggle，并存储在内存中。

![image-20220904105458736](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904105458736.png)![image-20220904105503200](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904105503200.png)

​	每当调用函数的时候，计算机都会进行上述的操作，同时计算机会为这个函数调用分配一块内存。![image-20220904105730024](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904105730024.png)![image-20220904105736077](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904105736077.png)

计算机使用一个栈来表示这些内存块，第二个内存块位于第一个之上。当打印 how are you, maggie?，此时栈顶的内存块被弹出。

![image-20220904110209087](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904110209087.png)弹出之后，此时栈顶是函数greet，即返回到了函数greet。调用函数，函数处于未完成暂停的状态。greet函数所有变量的值仍在内存中。从greet函数离开的位置继续向下运行，首先打印getting ready to say bye…，接着调用函数bye。![image-20220904110514700](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904110514700.png)打印ok bye!函数返回，bye弹出

![image-20220904110606115](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904110606115.png)

​	总结下来，这个栈用于存储函数多个变量，被称为调用栈。

​	递归函数也是调用栈，

```python
def fact(x):
	if x == 1:
		return 1
	else:
		return x * fact(x-1)
```

​	分析调用`fact(3)`时调用栈是如何变化的。栈顶的方框表示当前程序执行到了什么地方，![image-20220904111146785](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904111146785.png)![image-20220904111152772](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904111152772.png)

![image-20220904111312034](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904111312034.png)![image-20220904111348454](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904111348454.png)![image-20220904111354917](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904111354917.png)![image-20220904111416126](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904111416126.png)

## 栈的缺点

​	使用栈虽然很方便，但是储存在栈中的信息可能占用大量的内存。每一个函数调用都要占用一定的内存，栈很高，意味着计算机存储了大量函数调用的信息。

## 小结

- 递归指的是调用自己的函数。
- 每个递归函数都有两个条件：基线条件和递归条件。
- 栈有两种操作：压入，弹出。
- 所有函数调用都进入调用栈。
- 调用栈可能很长，将占用大量内存。

# 快速排序

> 分而治之：divide and conquer（D&C）
>
> 一种著名的递归式解决问题的方法，优雅代码的典范。

For example：

​	假设你是农场主，需要将一小块土地均匀的分成方块，且分出的方块要尽可能的大。![image-20220904113049273](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904113049273.png)显然下面的分法都不符合要求![image-20220904113117915](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904113117915.png)

使用D&C解决问题包括两个步骤：

1. 找出基线条件，基线条件应尽可能简单。
2. 不断将问题分解（或者说缩小规模）。

进行分析，能使用的最大方块有多大，另一条边为另一条边的整数倍，640*640的方块可以分出两个，剩下的可以继续分。![image-20220904114554061](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904114554061.png)![image-20220904114559155](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904114559155.png)

![image-20220904114722161](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904114722161.png)![image-20220904114729794](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904114729794.png)

再用同样的方法进行分块，

![image-20220904120203982](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904120203982.png)![image-20220904120215015](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904120215015.png)

![image-20220904120226142](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904120226142.png)![image-20220904120231227](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904120231227.png)

此时基线条件出现，因此再往下分刚好两个正方形，没有产生剩余![image-20220904120459878](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904120459878.png)

再倒退可得，适用的全部相同的最大方块为80*80。![image-20220904120515358](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904120515358.png)

## 再谈大O表示法

![image-20220904193834816](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904193834816.png)![image-20220904193904322](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904193904322.png)

## 平均情况和最糟情况

​	快速排序的性能高度依赖于你选择的基准值。假设你总是以第一个为基准值，大部分时候都会导致调用栈非常长。这属于最糟情况。	![image-20220904201125308](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904201125308.png)![image-20220904201148322](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904201148322.png)

​	倘若从中间开始，调用栈将大大缩短，这是最佳情况。![image-20220904201211679](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904201211679.png)![image-20220904201226227](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904201226227.png)

- 最糟情况：栈长O(n)
- 最佳情况：栈长O(log n)

​	即使以不同方式划分数组，每次也将涉及O(n)个元素。因此，完成每层所需的时间都为O(n)

![image-20220904201907241](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904201907241.png)![image-20220904201918764](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904201918764.png)

![image-20220904202307539](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904202307539.png)

## 小结

- D&C将问题逐步分解。使用D&C处理列表时，基线条件很可能时空数组或只包含一个元素的数组。
- 实现快速排序时，请随机地选择用作基准值的元素。快速排序的平均运行时间为O(nlogn)
- 大O表示法中的常量有时候事关重大，这就是快速排序比合并排序快的原因所在。
- 列表很长时，常量对二分查找和简单查找的影响并不大，O(logn)的速度比O(n)快很多。

# 散列表

> 再次提醒二分查找只针对**有序列表**

## 散列函数

> 散列函数：无论输入什么数据，都将获得一个数字。![image-20220904203948822](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904203948822.png)
>
> 满足以下要求：
>
> - 它必须是一致的。例如，假设你输入apple得到的是4，那么每次输入apple时，得到的都必须为4.如果不是这样，散列表将毫无用处。
> - 它将不同的输入映射到不同的数字。例如，如果一个散列函数不管输入是什么都返回1，则它就不是一个好的散列函数，最理想的情况，将不同的输入映射到不同的数字。

散列函数将输入映射为数字，可以实现O(1)查找，假设：

![image-20220904204559763](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904204559763.png)![image-20220904204954900](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904204954900.png)代表散列函数![image-20220904204604128](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904204604128.png)

![image-20220904204616221](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904204616221.png)![image-20220904204623833](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904204623833.png)

![image-20220904204629801](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904204629801.png)

......

![image-20220904204643582](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904204643582.png)

假设要查找avocado的值，只需要将avocado作为输入交给散列函数。![image-20220904204652604](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904204652604.png)

![image-20220904204706398](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220904204706398.png)

## 散列表

​	![image-20220905105916576](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905105916576.png)

```python
book=dict()
```

​	在字典中添加一些商品的价格

```python
>>> book["apple"] = 0.67
>>> book["milk"] = 1.49
>>> book["avocado"] = 1.49
>>> print book
{'avocado': 1.49, 'apple': 0.67, 'milk': 1.49}
进行查询avocado
>>> print book["avocado"]
1.49
```

​	散列表由键和值组成。在前面的散列表book中，键为商品名，值为商品价格。散列表将键映射到值。

​	创建散列表的方式：

```python
//方法1
book=dict()
//方法2
book={}
//添加键值对
book["jack"]=12345
book["merry"]=89798
//查找信息
print book["merry"]
```

​	DNS解析≈散列表

## 防止重复

首先创建一个散列表，函数get将它返回，如果存在这个键，将返回对应的值，如果不存在，则返回None。

```python
>>> voted{}
>>> value=voted.get("tom")
```

![image-20220905151747685](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905151747685.png)

投票代码：

```python
voted = {}
def check_voter(name):
	if voted.get(name):
		print "kick them out!"
	else:
		voted[name] = True
		print "let them vote!"
        
//测试
>>> check_voter("tom")
let them vote!
>>> check_voter("mike")
let them vote!
>>> check_voter("mike")
kick them out!
```

## 将散列表用于缓存

缓存是一种常用的加速方式，举例：

![image-20220905152401698](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905152401698.png)![image-20220905152420773](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905152420773.png)

![image-20220905152619607](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905152619607.png)![image-20220905152635990](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905152635990.png)

## 总结

​	散列表适合

- 模拟映射关系
- 防止重复
- 缓存or记忆数据，加速访问

## 冲突

> 给两个键分配的相同的位置

解决方法就i是：

- 在共同的位置上创建一个链表，但是一旦链表所包含的元素越多，将会造成访问速度大大降低。![image-20220905153228523](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905153228523.png)![image-20220905153245474](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905153245474.png)

- 优化散列函数，尽量使得键均匀的映射到散列表的不同位置。

## 性能

散列表执行各种操作时间都是O(1)。O(1)为常量时间，例如从一个数组中获取一个元素时间都是固定的，平均情况下，散列表的速度确实快。![image-20220905153921399](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905153921399.png)

![image-20220905154609277](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905154609277.png)

## 填装因子

​	填装因子=散列表所包含的元素数/位置总数

![image-20220905154910251](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905154910251.png)

填装因子大于0.7，就调整散列表的长度，通常增长一倍。

## 散列函数

良好的散列函数可以让数组中的值呈现均匀分布，与差劲的散列函数形成对比：![image-20220905155452145](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905155452145.png)![image-20220905155433941](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905155433941.png)

> SHA函数可用作散列函数。

# 时间-专业术语

常量时间O(1)![image-20220905154230349](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905154230349.png)

线性时间O(n)![image-20220905154236923](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905154236923.png)

对数时间O(logn)![image-20220905154243016](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905154243016.png)

# 广度优先搜索

> 它是一种图算法，解决最短路径问题的算法称为广度优先算法。

## 图简介

最短路径问题：![image-20220905160035390](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905160035390.png)

第一步所能到达地点圈出

![image-20220905160308236](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905160308236.png)第二步![image-20220905160317673](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905160317673.png)

第三步

![image-20220905160349527](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905160349527.png)

最短路径

![image-20220905160359415](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905160359415.png)

以上例子解决问题的步骤：

1. 使用图来建立问题模型
2. 使用广度优先搜索解决问题

## 图是什么

​	图模拟了一种连接，图用于模拟不同的东西之间是如何连接的，例如欠钱关系图

![image-20220905160732887](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905160732887.png)

包含：![image-20220905160748753](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905160748753.png)

## 广度优先搜索

​	和二分查找一样都是一种查找算法。可解决两类问题

1. 从A出发，存不存在前往B的路径
2. 从A出发，到B的路径中，哪一条是最短的

### 查找最短路径

![image-20220905161414568](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905161414568.png)![image-20220905161426771](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905161426771.png)

上图中，一度关系在二度关系之前加入查找名单，必须按顺序进行检查，不然不能保证是最短路径，队列这种数据结构可以实现。

### 队列

​	队列和生活中排队非常类似，排在前面的先“上车”，队列和栈类似，不能随意的访问队列中的元素，队列只支持：入队，出队。![image-20220905162251294](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905162251294.png)

​	队列是一种先进先出的数据结构，而栈是一种后进后出的数据结构![image-20220905165029102](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905165029102.png)

## 实现图

```python
graph = {}
graph["you"] = ["alice", "bob", "claire"]
```

graph["you"]是一个数组，其中包含了“你”的所有邻居。

![image-20220905165330647](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905165330647.png)![image-20220905165338451](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905165338451.png)

```python
//同理用来表示的python代码如下
graph = {}
graph["you"] = ["alice", "bob", "claire"]
graph["bob"] = ["anuj", "peggy"]
graph["alice"] = ["peggy"]
graph["claire"] = ["thom", "jonny"]
graph["anuj"] = []
graph["peggy"] = []
graph["thom"] = []
graph["jonny"] = []
```

下面两图等价![image-20220905165540085](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905165540085.png)

## 实现算法

![image-20220905165645930](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905165645930.png)

`python`的队列表示

```python
from collections import deque
search_queue = deque()
search_queue += graph["you"]
```

`graph["you"]`是一个数组，其中包含你的所有邻居，如["alice", "bob",
"claire"]。这些邻居都将加入到搜索队列中。

```python
while search_queue: //只要队列不为空
	person = search_queue.popleft()//就读取其中第一个人
	if person_is_seller(person)://检查此人是否为目标对象
		print person + " is a mango seller!"//成功找到对象
		return True
	else:
		search_queue += graph[person]//如果不是，将其关联对象加入队列
return False //如果运行至此，说明队列中不存在对象
```

用于判断是否为目标对象函数

```python
def person_is_seller(name):
	return name[-1] == 'm'
```

![image-20220905170843382](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905170843382.png)![image-20220905170851517](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905170851517.png)

程序停止情况：

- 找到目标对象
- 队列变为空，在队列中找不到目标对象，Peggy既是Alice的朋友又是Bob的朋友![image-20220905172606434](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905172606434.png)

​	出现两次，不应该重复检查，故在检查完一个人之后，应该将其标记为已检查，且再不检查他，可以新建一个列表来记录已经检查过的人，考虑这一部分之后，最终的代码就是：

```python
def search(name):
	search_queue = deque()
	search_queue += graph[name]
	searched = []
	while search_queue:
		person = search_queue.popleft()
		if not person in searched:
			if person_is_seller(person):
				print person + " is a mango seller!"
				return True
			else:
				search_queue += graph[person]
				searched.append(person)
	return False
search("you")
```

## 运行时间

​	在整个图中，沿着每一条路线前进，因此运行时间至少为O(边数)，其中图中每一个节点添加到队列中所需要的时间是O(人数)，所以总的广度优先搜索的运行时间就是O(人数＋边数)，通常写作O(V+E)，其中V为顶点数，E为边数。

# 狄克斯特拉算法 

## 使用狄克斯特拉算法

![image-20220905200329517](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905200329517.png)

​	每个数字代表的都是时间，单位分钟。

​	若使用广度优先搜索，将得到下面这条段数最少的路径

![image-20220905200539766](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905200539766.png)

​	若使用狄克斯特拉算法将包含以下四个步骤：

1. 找出“最便宜”的节点，即可在最短时间内到达的节点。
   1. 从起点开始前往A或B所需的时间，进行对比可知，在假设到达终点所需要的时间为无穷大，可知节点B此时为最近节点![image-20220905201356210](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905201356210.png)
2. 更新该节点的邻居的开销，其含义就是B前往各个“邻居”所需要的时间
   1. ![image-20220905201454948](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905201454948.png)
   2. 在这里找到了前往A的更短的时间，到达终点的时间由无穷大变成7min
3. 重复上述过程，直到对图中的每个节点都这样做了
   1. 对A进行相同操作![image-20220905202229677](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905202229677.png)
   2. 更新A点的所有开销，发现前往终点的时间为6min
   3. 对每个节点都运行狄克斯特拉算法（终点除外），![image-20220905202645569](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905202645569.png)
4. 计算最终路径

​	使用广度优先搜索算法时，“最短路径”的意思是所经过的段数最少；

​	而使用狄克斯特拉算法时，每一段路径都拥有了权重，狄克斯特拉算法的目标时找到权重最小的那一条路径。

![image-20220905203037591](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905203037591.png)

## 术语

狄克斯特拉算法每条线路上的数字代表的是“权重”

![image-20220905215409284](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905215409284.png)

带有权重的称为加权图，不带权重的称为非加权图

![image-20220905215537892](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905215537892.png)

非加权图适合用广度优先搜索算法

加权图适合用狄克斯特拉算法，且狄克斯特拉算法只适用于有向无环图

![image-20220905215950725](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905215950725.png)

![image-20220905215957042](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220905215957042.png)

主要步骤示意图：![image-20220906190526323](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906190526323.png)

```python
node = find_lowest_cost_node(costs)
//在未处理的节点中找出开销最小的节点
while node is not None:
    // 这个while循环在所有节点都被处理过后结束
	cost = costs[node]
	neighbors = graph[node]
	for n in neighbors.keys():
        // 遍历当前节点的所有邻居
		new_cost = cost + neighbors[n]
		if costs[n] > new_cost:
            //如果经当前节点前往该邻居更近
			costs[n] = new_cost
            //就更新该邻居的开销
			parents[n] = node
            //同时将该邻居的父节点设置为当前节点
	processed.append(node)
    //将当前节点标记为处理过
	node = find_lowest_cost_node(costs)
    //找出接下来要处理的节点，并循环
    
    
def find_lowest_cost_node(costs):
	lowest_cost = float("inf")
	lowest_cost_node = None
	for node in costs:
		cost = costs[node]
		if cost < lowest_cost and node not in processed:
			lowest_cost = cost
			lowest_cost_node = node
	return lowest_cost_node
```

​	每个节点都有开销，

![image-20220906191726630](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906191726630.png)

新旧开销进行对比：![image-20220906191741224](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906191741224.png)

![image-20220906192145740](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906192145740.png)

## 小结

- 广度优先算法用于非加权图中查找最短路径
- 狄克斯特拉算法用于在加权图中查找最短路径
- 仅当权重为正时，狄克斯特拉算法才管用
- 如果图中权重包含负权重边，则需要使用贝尔曼-福德算法

# 贪婪算法

## 举例：教室调度问题

![image-20220906200037187](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906200037187.png)

![image-20220906200105238](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906200105238.png)![image-20220906200110283](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906200110283.png)

​	你希望在这件教室尽可能多的安排可以教学的课，如何选出尽可能多的且时间不冲突的课程呢？

​	算法的步骤：

1. 首先选出结束最早的课，它就是要在这间教室要上的第一堂课。
2. 接下来选出第一堂课后才开始的课，在第一堂课结束之后才开始的课中，选出结束时间最早的课，这就是这件教室要上的第二堂课。
3. 重复以上步骤就可以找出答案，如下图所示

![image-20220906200522875](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906200522875.png)

![image-20220906200531815](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906200531815.png)

![image-20220906200539029](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906200539029.png)

![image-20220906200555064](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906200555064.png)

> 贪婪算法优点：简单易行！
>
> 贪婪算法的贪婪之处体现在，贪婪算法的每一步都是局部最优解，最终得到的就是全局最优解，但也并非所有情况之下都有效。

## 背包问题

​	你只有：![image-20220906200935409](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906200935409.png)

而现在![image-20220906200950296](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906200950296.png)

如果按照贪婪算法来说，选择将最贵的音箱装入袋中，将无法装下其他物品，但是这并不是获利最多的情况。

​	因此可以知道，贪婪算法只能近似的取得接近最优解的结果。

## 集合覆盖问题

举例：

![image-20220906201726027](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906201726027.png)

已知现在需要将广播尽可能的让50个州的民众都可以收听到，但是各个广播台所覆盖的州都不相同，有的甚至有所重叠。

![image-20220906201816363](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906201816363.png)![image-20220906201822657](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906201822657.png)

![image-20220906201833478](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906201833478.png)

1. 列出每个可能的广播台集合，这被称为幂集，可能的子集有2的n次方个

   ![image-20220906202037961](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906202037961.png)

2. 在这些集合中，选出覆盖全美50个州的最小集合。

​	问题在于计算每个可能的广播台子集需要很长时间，由于可能的集合2的n次方个，因此运行时间为O(2的n次方)。如果广播台数量过大将会造成所需时间激增。

## 近似算法

1. 选出一个广播台，它的特征是：覆盖大部分未覆盖州，即便这个广播台覆盖了一些已经覆盖的州，也先不管
2. 重复第一步，再选择一个覆盖大部分未覆盖州的广播台。

​	这是一种近似算法。在获得精确解需要的时间太长的时候，可使用近似算法。

​	判断近似算法优劣标准

- 算法速度快慢
- 得到的近似解与最优解的近似程度

### 准备工作

1. 创建一个列表，其中包含“50州”即要覆盖的州，

   ```python
   states_needed = set(["mt", "wa", "or", "id", "nv", "ut","ca", "az"])
   ```

   []内的数组将会变为集合，区别与数组的不同是集合中同样的元素只能出现一次，即集合不能包含重复的元素，例如

   ```python
   >>> arr = [1, 2, 2, 3, 3, 3]
   >>> set(arr)
   set([1, 2, 3])
   ```

   ![image-20220906203855660](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906203855660.png)

​		可供选择的“广播台”清单，我选择使用散列表来表示它。

```python
stations = {}
stations["kone"] = set(["id", "nv", "ut"])
stations["ktwo"] = set(["wa", "id", "mt"])
stations["kthree"] = set(["or", "nv", "ca"])
stations["kfour"] = set(["nv", "ut"])
stations["kfive"] = set(["ca", "az"])
```

​		用于存储最终选择的广播台。

```python
final_stations = set()
```

2. 计算答案

将从中选出的覆盖了最多未覆盖的广播台存储在`best_station`，

```python
best_station = None
states_covered = set()
for station, states_for_station in stations.items():
```

`states_covered` 是一个集合，包含该广播台覆盖的所有未覆盖的州。`for`循环迭代每个广播台，并确定它是否是最佳的广播台。

```python
covered = states_needed & states_for_station//计算两个集合的交集
if len(covered) > len(states_covered):
	best_station = station
	states_covered = covered
```

## 集合

​	水果集合

![image-20220906205929587](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906205929587.png)

​	蔬菜集合

![image-20220906205941996](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906205941996.png)

![image-20220906210001871](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906210001871.png)![image-20220906210007774](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906210007774.png)

![image-20220906210016855](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906210016855.png)

- 差集意味着将从一个集合中剔除出现在另一个集合中的元素
- 集合类似列表，但是不能包含重复的元素，可以进行并集、交集、差集运算。

​	states_covered就是最优解，需要不断优化。

​	不断地循环，直到states_needed为空，完整代码：

```python
while states_needed:
	best_station = None
	states_covered = set()
	for station, states in stations.items():
		covered = states_needed & states
		if len(covered) > len(states_covered):
			best_station = station
			states_covered = covered
            
states_needed -= states_covered
final_stations.add(best_station)
```

```python
>>> print final_stations
set(['ktwo', 'kthree', 'kone', 'kfive'])
```

## NP完全问题

![image-20220906212956218](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906212956218.png)

![image-20220906214140851](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906214140851.png)

![image-20220906214233900](https://cdn.jsdelivr.net/gh/WINNERZR01/ImageHosting/writeimg/image-20220906214233900.png)

# 动态规划

