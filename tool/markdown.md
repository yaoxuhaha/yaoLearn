
from https://www.jianshu.com/p/191d1e21f7ed

from http://note.youdao.com/iyoudao/?p=2411

## 标题部分语法

# 一级标题
## 二级标题
### 三级标题
#### 四级标题


## 字体部分语法

我想要将**文字**加粗

我想要将*文字*变为斜体

我想要将***文字***变为斜体加粗

我想要将~文字~变为删除线

## 引用
> 这是引用的内容 床前明月光
>> 这是引用的内容  

## 分割线

---------
********
----------
## 上传图片
![image](https://note.youdao.com/favicon.ico)

![image](C:/Users/YAO/Desktop/markdown5.jpg "注意这里是反斜杠")


## 超链接
[百度](www.baidu.com "百度")
[简书](http://jianshu.com)


<a href="https://www.jianshu.com/u/1f5ac0cf6a8b" target="_blank">简书</a>


## 无序列表
- 列表内容
+ 列表内容
* 列表内容

## 有序列表
1. term1
2. term2
3. term3

注意 符号和内容之间有空格



## 表格
表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容

第二行分割表头和内容。
- 有一个就行，为了对齐，多加了几个
文字默认居左
-两边加：表示文字居中
-右边加：表示文字居右
注：原生的语法两边都要用 | 包起来。此处省略

## 代码


    
    <?xml version="1.0" encoding="UTF-8"?> 
    
    <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
             version="3.1">
             
    </web-app>
    
换行需要加一行空格
每行前边有个tab键



    public static void main(String [] args){

        System.out.println("hi github");

    }
