# 算法分析

## 运行时间

### 一般法则

- 法则1-FOR循环：

  - 一次FOR循环的运行时间至多是改for循环内语句（包括测试）的运行时间乘以迭代的次数。

- 法则2-嵌套的for循环：

  - ```c
    for(i=0;i<N;i++)
    	for(j=0;j<N;j++)
    		k++;
    ```

- 法则3-顺序语句:

  - 将各个语句的运行时间求和即可，其中的最大值就是所得的运行时间。

  - ```c
    # 下面的例子中，先用去O(N)，再花费O(N²)，总的开销哦啊也是O(N²)
    for(i=0;i<N;i++)
        A[i]=0;
    for(i=0;i<N;i++)
        for(j=0;j<N;j++)
            A[i]+=A[j]+1+j;
    
    ```

    

- 法则4-IF/ELSE语句

  - ```c
    if(condition)
    	S1
    else
    	S2
    ```

  - 一个if/else语句的运行时间从不超过判断再加上S1和S2运行时间长者的总的运行。
