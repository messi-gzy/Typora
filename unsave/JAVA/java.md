# Java

### 一、目录

### 二、基础

#### 1、集合

<img src="https://pic.imgdb.cn/item/6298c54f09475431298a8cd5.jpg" style="zoom: 33%;" />

##### 1、List

<img src="https://pic.imgdb.cn/item/6298c75c09475431298da359.jpg" style="zoom:50%;" />

##### 2、迭代器

遍历

```java
 Collection<String> collection=new ArrayList<String>();
        collection.add("a");
        collection.add("b");
        collection.add("c");
        //System.out.println(collection);
        Iterator <String> iter=collection.iterator();
        while (iter.hasNext()){
            System.out.println(iter.next());
        }
```



#### 2、泛型

