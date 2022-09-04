



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
