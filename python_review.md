# python_review

## str

~~~python
def demo_str():
    temp_str = "  asd asd   "
    # Title function in python is the Python String Method which is used to
    # convert the first character in each word to Uppercase and
    # remaining characters to Lowercase in string and returns new string.
    print(temp_str.title())
    print(temp_str.upper())
    print(temp_str.lower())
    print(len(temp_str))
    # strip可以删除开头和末尾多余的空格，不过是暂时的
    print(len(temp_str.rstrip()))
    print(len(temp_str.lstrip()))
    print(len(temp_str.strip()))
~~~

## list

~~~python
def demo_list():
    bicycles = ['trek', 1, 2]
    print(bicycles[2])
    # append
    bicycles.append('aa')
    print(len(bicycles))
    # insert
    bicycles.insert(0, 'bb')
    print(bicycles)
    # 这里的pop可以加参数，默认-1？
    # Raises IndexError if list is empty or index is out of range.
    bicycles.pop()
    print(bicycles)
    # remove,只删除第一个找到的值，也会报错
    bicycles.remove('bb')
    print(bicycles)
    # sorted时临时的，永久的是sort，数据类型需要相同
    temp_list = ['aa bb', 'aa ab']
    sorted(temp_list)
    print(temp_list)
    temp_list.sort()
    print(temp_list)
~~~

## for

~~~python
def demo_for():
    temp_list = ['aa bb', 'aa ab']
    temp_a = [(i, j) for i, j in enumerate(temp_list)]
    print(temp_a)
    temp_b = temp_a.copy()
    print(temp_b)
    # tuple在某种意义上是const的
    temp_tuple = (1, 2)
    print(temp_tuple)
~~~

## dict

~~~python
def demo_dict():
    temp_dict = {'a': 1, 'b': 2}
    # items、keys、values返回的是一个可迭代的类集合
    print(temp_dict.items())
    for key, value in temp_dict.items():
        print(key, value)
    print(temp_dict.keys())
    print(temp_dict.values())
~~~

## def函数

~~~python
def demo_test(temp_a, temp_list=[]):
    # 注意有默认值的参数放到后面
    temp_a = 2
    if temp_list:
        temp_list[0] = 1
    return temp_list


def demo_all_args(*args, **arugs):
    # *可以接任意数量的形式参数，返回tuple，**接受任意数量的实参，返回dict
    print(args)
    print(arugs)


# 按间距中的绿色按钮以运行脚本。
if __name__ == '__main__':
    print_hi('PyCharm')
    demo_str()
    demo_list()
    demo_for()
    demo_dict()
    a = 1
    temp_list = [2, 2, 2]
    # 这里的list仍然是传的地址,如果用list[:]可以起到copy()的效果
    test_list = demo_test(a, temp_list[:])
    print(a)
    print(test_list)
    print(temp_list)
    demo_all_args('aa', 'bb', aa=1, bb=2)
~~~

## class类

### 公有与私有

~~~python
class Dog(obzject):
    def __init__(self, name, age=0):
        # 决定了生成时需要传递的参数,仍然是有默认值的参数放后面
        # __name表示私有成员
        self.__name = name
        self.age = age

    def get(self):
        print(self.__name.title() + str(self.age))

    def __this(self):
        # __this表示私有函数
        print('hi')
~~~

### 继承

~~~python
class Ddog(Dog):
    def __init__(self, name, age, dd):
        super().__init__(name, age)
        self.dd = dd

    def get(self):
        super().get()
        print(self.dd)
~~~

### 声明与调用

~~~python
if __name__ == '__main__':
    temp_dog = Dog('aa')
    temp_dog.get()
    # 将name设置为私有，外部修改时不会报错，当然也不会修改
    # 必须用_class__attribute/way来调用或修改
    # 调用私有方法时似乎警告了些什么
    temp_dog._Dog__name = 'bb'
    temp_dog.get()
    temp_dog._Dog__this()
    temp_Ddog = Ddog('cc', 1, 22)
    temp_Ddog.get()
~~~

