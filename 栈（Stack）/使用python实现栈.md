数据结构去算法笔记

1、栈（stack）又名堆栈，它是一种运算受限的线性表。其限制是仅仅允许在表的一端插入和删除运算。

栈允许进行插入和删除操作的一端称为栈顶(top)，另一端为栈底(bottom)；栈底固定，而栈顶浮动；栈中元素个数为零时称为空栈。插入一般称为进栈（PUSH），删除则称为退栈（POP）。

由于堆叠数据结构只允许在一端进行操作，因而按照后进先出（LIFO, Last In First Out）的原理运作。栈也称为后进先出表。

栈属于常见的一种线性结构，对于进栈和退栈而言，时间复杂度都为 O(1)

![wm](C:\Users\xiaoyulong\Desktop\Data Structure\栈（Stack）\img\wm.png)

2、栈的实现

​	（1）首先创建一个名为Stack的类，对栈进行初始化参数设计

```
class Stack(object):
    def __init__(self, limit=10):
        self.stack = []  # 存放栈元素
        self.limit = limit  # 栈容量
```

​	（2）push（进栈）

​			当要加入新元素时，将新元素放在栈顶，新元素入栈时，栈顶上移。

```
  def push(self, num):
        # 判断栈是否溢出
        if len(self.stack) >= self.limit:
            raise IndexError('超出栈容量极限')
        self.stack.append(num)
```

​	(3)pop（退栈）

​			从栈顶移除一个数据，将栈顶元素拷贝出来，栈顶下移，拷贝出来的栈顶作为函数的返回值

```
def pop(self):
        if self.stack:
            return self.stack.pop()
        else:
            raise IndexError('栈里面没有元素')
```

​	（4）其他函数

​			peek : 查看堆栈的最上面的元素

​			is_empty : 判断栈是否为空

​			size : 返回栈的大小

​			具体实现代码如下：

```
  def peek(self):
        if self.stack:
            return self.stack[-1]

    def is_empty(self):
    	# bool()函数用于将给定参数转换为布尔类型，如果没有参数，返回False
        return not bool(self.stack)

    def size(self):
        return len(self.stack)
```

综合以上，最终实现的代码块如下：

```
class Stack(object):
    def __init__(self,limit = 20):
        self.stack = []
        self.limit = limit

    def push(self,num):
        if len(self.stack) >= self.limit:
            raise IndexError("超出栈的承受范围")
        else:

    def pop(self):
        if self.stack is not None:
           return self.stack.pop()
        else:
            raise IndexError("栈里面没有元素")

    def peek(self):
        return self.stack[-1]

    def is_empty(self):
        return not bool(self.stack)

    def size(self):
        return len(self.stack)




```

栈还有着一些经典的应用,比如括号匹配以及后缀计算器



任务:检查括号是否完全匹配,要求使用一个堆栈来检查括号字符串是否平衡.

​	有效括号字符串需要满足:

​		左括号必须用相同类型的右括号闭合

​		左括号必须以正确的顺序闭合

​		注意空字符串可被认为是有效字符串

例如: ((())) True

​	 (())) False

要求:使用栈作为数据结构来检查括号字符串是否完全匹配

代码如下:

```
# 使用栈检查括号是否匹配
class Stack(object):
    def __init__(self,limit = 20):
        self.stack = []
        self.limit = limit

    def push(self,data):
        if len(self.stack) >= self.limit:
            raise IndexError("此栈已满")
        self.stack.append(data)

    def pop(self):
        if self.stack:
            return self.stack.pop()
        else:
            raise IndexError("栈里面没有元素")

    def peek(self):
        return self.stack[-1]
    def is_empty(self):
        return not bool(self.stack)
    def size(self):
        return len(self.stack)

def balance_parentheses(parentheses):
    stack = Stack()
    # 下面判断有个bug,如果给的是一个空的值,n那么就还会是True
    for parenthesis in parentheses:
        if parenthesis == '(':
            stack.push(parenthesis)
        elif parenthesis == ')':
            if stack.is_empty():
                return False
            stack.pop()
    return stack.is_empty()

if __name__ == '__main__':
    examples = ['((()))','((())','(()))','']
    print("最终结果如下:\n")
    for example in examples:
        print(example + ':'+ str(balance_parentheses(example)))
```

