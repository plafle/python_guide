### Some special method in class

这篇文档假设你已经了解了class的基本机制。若没有，请pull-request，我会补充

> 代码块下面的那一个表示的是上面的代码的输出结果
>
> 请重点关注代码



##### Class attribute

```python
class Person:
    number_of_people = 0
    def __init__(self, name):
        self.name = name
        Person.number_of_people += 1
        
p1 = Person("tim")
print(Person.number_of_people)
p2 = Person("jill")
print(Person.number_of_people)
```

```
1
2
```

普通的attribute是属于某一个object的，例如name就是这样一个attribute。

class attribute则是属于整个class的，例如number_of_people就是这样一个class attribute。



##### Static method

```python
class Math:
    @staticmethod
    def add5(x):
        return x + 5
   	
    @staticmethod
    def add10(x):
        return x + 10
    
    @staticmethod
    def pr():
        print("run")
x = 10
Math.pr()  
x = Math.add5(x)
print(x)
```

```
run
15
```



在普通的method前面加上`@staticmethod`修饰，可以将一个普通的method变成static method

如果在Math这个class中定义了add5这个static method，就可以通过Math.add5来调用add5这个函数。static method用于将多个method整合起来，从而便于迁移。例如我有以下几个函数: fun1,fun2,fun3,fun4,我可以定义一个class，比如用tools来命名这个class吧，然后让这几个函数都变成tools里面的static method。然后，其他人就可以通过一句`import tools`来吧这几个函数都引用进来。



##### `__len__` method && `__bool__` method

```python
class rnge:
    def __init__(self,x,y):
        self.x = x
        self.y = y

    def __len__(self):
        return self.y - self.x + 1

a = rnge(2,3)
print(len(a))
if a:
    print("a is true")
else:
    print("a is false")
```

```
2
a is true
```

**Notice:** `__len__` **function could only return a non-negative integer**

**Notice: If a** `__bool__` **function is defined in a class, then the True/False value of the object will be determined by the return value of the** `__bool__` **function, otherwise it will be determined by the return value of the** `__len__` **function. If it is determined by the** `__len__` **function, then it would be true when**`__len__` **function returns a positive value and it would be false when len function returns a negative number**



