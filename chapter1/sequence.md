## 序列家族
序列可以理解为一系列有序的元素(item)，比如上一节中我们讲的字符串，通过序号我们可以找到字符串中的每一个字符，序号是字符的位置官方的说法是索引(index)，序列的开始索引是0，看下面这个例子：
    >>> nums = [1,5,10,6,8,3,20,9]
    >>> lucky_index = 5
    >>> nums[0], nums[2], nums[luck_index]
    (1, 10, 3)
    >>> nums[-1]
    95
    >>> nums[8]
    ...
    IndexError: list index out of range
    >>> nums[-9]
    ...
    IndexError: list index out of range
看下图中这条蛇找元素的时候我们可以从蛇头（0）开始向右正数，或者向左负数，比如“6”的索引可以是`3`也可以是`-5`。

![](image/sequence_nums.png)


注意代码中最后的那两个`IndexError`，不要让索引值超过蛇的长度，那样会咬到尾巴。

### 列表
列表(list)是值的序列，在字符串中，这些值是字符，在列表中，值可以是任何类型，而且可以不必类型完全相同。创建列表最简单的方法是用方括号“[]”将元素括起来，比如：
    >>> ex_list0 = ['abc', 10, 20]
    >>> ex_list1 = [ex_list0, 'nested']
    >>> ex_list2 = list()
    >>> ex_list3 = []
    >>> print(ex_list0, ex_list1, ex_list2, ex_list3)
    ['abc', 10, 20] [['abc', 10, 20], 'nested'] [] []
第三行和第四行中的`[]`和`list()`可以建立一个空的列表。
#### 列表方法——修改
###### append()
append()方法会在原来的列表尾追加一个元素，方法和函数不同，通常需要以合适的“对象.方法名”来调用，比如：
    >>> list_1 = [9,8,0,5]
    >>> print(list_1.append(7))
    None
print()的结果是None，因为append()方法本身并没有返回值，只是追加了一个元素到列表尾。

##### pop()
pop的意思是“砰”功能和名字一样，pop()方法和append()的基本相反，不加参数的时候pop()方法“砰”掉列表尾的元素，如果加了参数（瞄准），就定向的“砰”。比如：
    >>> list_7 = ['a','c','v','z','t','y']
    >>> list_7.pop()
    'y'
    >>> list_7
    ['a', 'c', 'v', 'z', 't']
    >>> list_7.pop(2)
    'v'

##### insert()
当然我们也有可以定向追加元素的方法，比如：
    >>> nums = [0,1,2,3,4,5]
    >>> nums.insert(3, 'here')
    >>> nums
    [0, 1, 2, 'here', 3, 4, 5]
它接收两个参数，第一个是插入位置，第二个是插入内容。

##### remove()
我们除了可以用以用pop()方法做定向删除，还可以使用remove()做匹配删除，比如：
    >>> ex_list5 = ['I', 'love', 'dear', 'and', 'love', 'my', 'sketch']
    >>> ex_list5.remove('love')
    >>> ex_list5
    ['I', 'dear', 'and', 'love', 'my', 'sketch']
    >>> ex_list5.remove('heart')
    ...
    ValueError: list.remove(x): x not in list

它只会移除第一个匹配项，如果在列表中没有匹配内容会引发一个ValueError。

#### 列表方法——顺序
##### reverse()
reverse()方法会让原列表变成反向（好像从尾到头一样），比如：
    >>> nums = [1,5,10,6,8,3,20,9]
    >>> nums.reverse()
    >>> nums
    [9, 20, 3, 8, 6, 10, 5, 1]
    
##### sort()
    >>> abc = [5,6,9,1,2,0]
    >>> abc.sort()
    >>> abc
    [0, 1, 2, 5, 6, 9]
    >>> num_str = [20,'gao',10,'10','a','c','8']
    >>> num_str.sort()
    ...
    TypeError: unorderable types: str() < int()    # 不能进行不同类型的混合排序
    >>> num_str = ['20','gao','11','10','a','c','8']
    >>> num_str.sort()
    >>> num_str
    ['10', '11', '20', '8', 'a', 'c', 'gao']
    
reverse()和sort()方法对原始列表内容进行了修改，通常这也是我们想要的结果，当然如果我们不希望这样，有两个内建函数可以把修改内容作为返回值，而不是直接改动原列表。我们会在后面用到的时候介绍，如果你现在就迫不急待想知道，去看一下附录中的内容然后在交互环境中输入help(内建函数名)查看文档信息。看完后'q'键或者'Esc'键退出。

### 元组
除了上文提到的字符串、列表外，常用的内建序列还有元组，你可以简单的理解为元组是不可变的列表。创建元组的语法很简单，还记得我们在“基本运算”那一节最后同时输出'a','b'两个值的写法吗？其实那样就创建了一个元组，下面是一些更全面的例子：

    >>> 1, 2, 3
    (1, 2, 3)
    >>> a = ()    # 空元组
    >>> b = tuple()    # 空元组
    >>> c = (1)
    >>> type(c)    # 内建函数用来判定变量类型
    <class 'int'>
    >>> d = (1,)    # 创建单值的元组需要额外加个逗号
    >>> type(d)
    <class 'tuple'>
    
### 序列通用操作
我们已经提到了Python中的最常用的三种序列，除了索引(indexing)操作外，所有的序列还可以进行一些其它的通用操作：分片(sliceing)、加(adding)、乘(multiplying)，检测某个元素是否属于序列，此外len()、max()、min()三个内建函数也可以对序列进行操作，具体用法都很简单，不过乘操作或许会让你小小惊讶一下：

#### 分片
分片操作是对原来的列表进行切片，它会得到一个新的序列，具体操作需要使用形如`[start:end:step]`这样的写法，三个参数都可以不写，`step`默认值是`1`。
    >>> tag = '<a href="http://www.gaosir.com">my Unfinished web site </a>'
    >>> tag[9:30]
    'http://www.gaosir.com'
    >>> tag[32:-4]
    'my Unfinished web site'
    >>> tag[::-1]
    ...    # 试一下是什么^_^
    >>> nums = [1,2,3,4,5,6,7,8,9,10]
    >>> nums[:-2]
    [1, 2, 3, 4, 5, 6, 7, 8]
    >>> nums[-4:]
    [7, 8, 9, 10]
    >>> nums[::2]
    [1, 3, 5, 7, 9]
    >>> nums[::-2]
    [10, 8, 6, 4, 2]

