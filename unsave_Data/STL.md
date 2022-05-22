# STL

### 【目录】

### 一、容器

#### 1、vector

###### 1.1、构造函数

| vector()                  | 空的vector              |
| ------------------------- | ----------------------- |
| vector(int size)          | 元素个数为size          |
| vector(int size,const &t) | 元素个数为size，且都为T |
| vector(const vector&)     | 复制构造函数            |
| vector(begin,end)         | 复制区间[begin,end)区间 |

> ```c++
> vector<T>::iterator p;
> ```

###### 1.2、增加函数

| void push_back(const T&x)                                    | 向量尾部增加元素      |
| ------------------------------------------------------------ | --------------------- |
| iterator insert(iterator it,const T& x)                      | 位置前增加一元素      |
| iterator insert(iterator it,int count,const T& x)            | 位置前增加count个元素 |
| iterator insert(iterator it,const-iterator frist,const-iterator last) | 从[frist,last)的数据  |

###### 1.3、删除函数

| iterator earse(iterator it)                  | 删除指定元素，返回值指向下一个元素 |
| -------------------------------------------- | ---------------------------------- |
| iterator earse(iterator frist,iterator last) | 删除从[frist，last)的元素          |
| void pop_back()                              | 删除最后一个元素                   |
| void clear()                                 | 清空元素                           |

###### 1.4、遍历函数

| reference at(int pos)     | 返回pos位置元素的引用              |
| ------------------------- | ---------------------------------- |
| reference front()         | 返回首元素                         |
| reference back()          | 返回尾元素                         |
| reference begin()         | 指向第一个元素                     |
| reference end()           | 指向最后一个元素的下一个位置       |
| reverse_iterator rbegin() | 反向迭代器，最后一个元素           |
| reverse_iterator rend()   | 反向迭代器，第一个元素之前一个元素 |

###### 1.5、判断函数

| bool empty() | 判断向量为空 |
| ------------ | ------------ |

###### 1.6、大小函数

| int size()     | 向量的元素个数     |
| -------------- | ------------------ |
| int capacity() | 向量的当前最大空间 |
| int max_size() | 最大的vector空间值 |

###### 1.7、其他函数

| void swap(vector &)                                   | 交换同类型的向量数据        |
| ----------------------------------------------------- | --------------------------- |
| void assign(int n,const T& x)                         | 设置第n个元素的值           |
| void assign(const_iterator frist,const_iterator last) | 设置从[frist,end)中元素的值 |

