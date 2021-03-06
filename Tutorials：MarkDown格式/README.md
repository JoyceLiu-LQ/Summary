# MarkDown教程

## 一.标题

### ！写法

1. "#"代表标题
2. "#"必须在最左侧
3. "#"后面必须加空格
4. 多一个"#"号标题小一号

```
"# "代表  一级标题
"## "代表  二级标题
"### "代表  三级标题
"#### "代表  四级标题
"##### "代表  五级标题
"###### "代表  六级标题
```
### ！示例

# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

<br/>

## 二.无序序列

### ！写法

1. "-"或"*"或"+"代表无序序列
2. "-"后面必须加空格
3. "-"多级序列的每层序列前同样使用"-"
4. 对于多级序列，在每一个内层序列前加多加一个"Tab"键
5. 每一层序列的符号都是"-"，但实际效果是每层序列的标志都不一样


```
"- "代表第一层序列
"Tab"+"- " 代表第二层序列
"Tab"+"Tab"+"- " 代表第三层序列
```
### ！示例

- 第一层序列
    - 第二层序列
        - 第三层序列
        - 第三层序列
- 第一层序列


## 三.有序序列

### ！写法

1. 序列前面全部使用 数字+小数点+空格 的方式表示
2. 多级序列前面加"Tab"
3. 小数点必须用英文输入法下的小数点，不能用句号
4. 空格必须用英文输入法下的空格

```
"1. "  代表第一级序列的第一个
"Tab"+"1. "  代表第二级序列的第一个
"2. "  代表第一级序列的第二个
```

### ！示例
1. 第一级序列的第一个
    1. 第二级序列的第一个
        1. 第三级序列的第一个
        2. 第三级序列的第二个
    2. 第二级序列的第二个
2. 第一级序列的第二个


## 四.段落

1. 段落的换行是使用两个以上空格加上回车
2. 也可以在段落后面使用一个空行来表示重新开始一个段落

## 五.字体

```
*斜体文本*
_斜体文本_
**粗体文本**
__粗体文本__
***粗斜体文本***
___粗斜体文本___
```

## 六.分隔线

1. 一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。  
2. 你也可以在星号或是减号中间插入空格

```
***

* * *

*****

- - -

----------
```

### ！示例

* * *

## 七. 删除线
1. 文字的两端加上两个波浪线 ~~ 即可

### ！示例

~~BAIDU.COM~~

## 八. 脚注
```
[^要注明的文本]
```
### ！示例
创建脚注格式类似这样 [^RUNOOB]。

[^RUNOOB]:  菜鸟教程 -- 学的不仅是技术，更是梦想！！！

## 九.区块引用
1. 段落开头使用 > 符号 ，然后后面紧跟一个空格符号
2. 嵌套的引用，一个 > 符号是最外层，两个 > 符号是第一层嵌套，以此类推

### ！示例
> 区块引用一  
> > 区块引用二  
> > > 区块引用三  



## 十.代码
1. 用两个"`"把一句代码包起来
2. 用两个"```"把多行代码包起来


### ！示例
```
javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```

## 十一. 链接
### ！写法

1. [链接名称] (链接地址)： 两个括号之间没有空格
2. 或<链接地址>
3. 链接也可以用变量来代替，文档末尾附带变量地址：[Google][代号]，然后在文档的结尾为变量赋值（网址） 

### ！示例

这是一个链接 [谷歌](https://www.google.com)  

<https://www.baidu.com>

这个链接用 1 作为网址变量 [Google][1]  
这个链接用 runoob 作为网址变量 [Runoob][runoob]  
  [1]: http://www.google.com/  
  [runoob]: http://www.runoob.com/
  

## 十二. 图片
### ！写法 
1. ![alt 属性文本] (图片地址) 两个括号中间没有空格
2. ![alt 属性文本] (图片地址 "可选标题") 两个括号中间没有空格
3. 图片网址使用变量 网址变量 [RUNOOB][1]，  
然后在文档的结尾位变量赋值（网址）[1]: http:...

### ！示例

![MJ](https://img.huffingtonpost.com/asset/57daced2180000c706314cc5.jpeg?cache=ibt0lhqisv&ops=crop_0_191_2480_1659,scalefit_720_noupscale)

## 十三.表格

### ！写法
1. 使用 | 来分隔不同的单元格，使用 - 来分隔表头和其他行
```
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```
2. 我们可以设置表格的对齐方式：
```
-: 设置内容和标题栏居右对齐。
:- 设置内容和标题栏居左对齐。
:-: 设置内容和标题栏居中对齐。
```

### ！示例

|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |

| 左对齐| 右对齐 | 居中对齐 |
| :----- | ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |


## 十四.转义

以下这些符号前面加上反斜杠"\\"来帮助插入普通的符号：
```
\   反斜线
`   反引号
*   星号
_   下划线
{}  花括号
[]  方括号
()  小括号
#   井字号
+   加号
-   减号
.   英文句点
!   感叹号
```


