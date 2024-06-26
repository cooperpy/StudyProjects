StudyProjects——记录学习过程中的笔记

# 《流畅的Python》学习笔记
## 第一章
- namedtuple 用以构建只有少数属性但是没有方法的对象，比如数据库条目
- __repr__所返回的字符串应该准确、无歧义，并且尽可能表达出如何用代码创建出这个被打印的对象。
- __repr__和__str__的区别在于，后者是在str()函数被使用，或是在用print函数打印一个对象的时候才被调用的，并且它返回的字符串对终端用户更友好。
- 如果你只想实现这两个特殊方法中的一个，__repr__是更好的选择，因为如果一个对象没有__str__函数，而 Python 又需要调用它的时候，解释器会用__repr__作为替代。
- 默认情况下，我们自己定义的类的实例总被认为是真的，除非这个类对__bool__或者__len__函数有自己的实现。bool(x)的背后是调用x.__bool__()的结果；如果不存在__bool__方法，那么bool(x)会尝试调用x.__len__()。若返回 0，则bool会返回False；否则返回True。

## 第二章
- 通常的原则是，只用列表推导来创建新的列表，并且尽量保持简短。如果列表推导的代码超过了两行，你可能就要考虑是不是得用for循环重写了
- 列表推导可以帮助我们把一个序列或是其他可迭代类型中的元素过滤或是加工，然后再新建一个列表。
- filter和map合起来能做的事情，列表推导也可以做，而且还不需要借助难以理解和阅读的lambda表达式。
- 创建一个具名元组需要两个参数，一个是类名，另一个是类的各个字段的名字。后者可以是由数个字符串组成的可迭代对象，或者是由空格分隔开的字段名组成的字符串.
- 如果赋值的对象是一个切片，那么赋值语句的右侧必须是个可迭代对象。即便只有单独一个值，也要把它转换成可迭代的序列
- 如果在a * n这个语句中，序列a里的元素是对其他可变对象的引用的话，你就需要格外注意了，因为这个式子的结果可能会出乎意料。比如，你想用my_list = [[]] * 3来初始化一个由列表组成的列表，但是你得到的列表里包含的 3 个元素其实是 3个引用，而且这 3 个引用指向的都是同一个列表。这可能不是你想要的效果
- 有时我们会需要初始化一个嵌套着几个列表的列表，譬如一个列表可能需要用来存放不同的学生名单，或者是一个井字游戏板上的一行方块。想要达成这些目的，最好的选择是使用列表推导
- board = [['_'] * 3 for i in range(3)   比较  weird_board = [['_'] * 3] * 3
- memoryview是一个内置类，它能让用户在不复制内容的情况下操作同一个数组的不同切片
- collections.deque类（双向队列）是一个线程安全、可以快速从两端添加或者删除元素的数据类型。而且如果想要有一种数据类型来存放“最近用到的几个元素”，deque也是一个很好的选择。这是因为在新建一个双向队列的时候，你可以指定这个队列的大小，如果这个队列满员了，还可以从反向端删除过期的元素，然后在尾端添加新的元素

from collections import deque  # 双端队列
from queue import Queue, SimpleQueue, LifoQueue, PriorityQueue # 线程安全
from multiprocessing import Queue, JoinableQueue  # 进程安全
import heapq  # 堆排序

## 第三章
- from collections import OrderedDict, ChainMap, Counter
- 就创造自定义映射类型来说，以UserDict为基类，总比以普通的dict为基类要来得方便
- 从 Python 3.3 开始，types模块中引入了一个封装类名叫MappingProxyType。如果给这个类一个映射，它会返回一个只读的映射视图。虽然是个只读视图，但是它是动态的。这意味着如果对原映射做出了改动，我们通过这个视图可以观察到，但是无法通过这个视图对原映射做出修改。
- 
