Python中的类没有公有与私有的概念，但是C++中有。

（Python中若要将方法标记为私有，一般采用在函数名称前添加下划线的方法）

eg.

```Python
class Human(object):
    a = 0 # 类属性
    def __init__(self):
        # 实例属性，与类属性同名的话会把类属性屏蔽掉
        # （感觉又有点像C++中的继承屏蔽（但也只是像而已））
        self._name = '' # 标记为私有，但外界能够访问
        self._age = 0
        
    def set(self): # 未标记为私有
        pass
    
    # 没有指定 @classmethod，是实例方法，需要等类实例化之后再调用；如果在实例化前调用的话需要手动传入 self
    def _process(self): # 标记为私有，但外界仍然能够访问
        pass
    
    @classmethod # 指定为类方法，绑定到的是类本身，操作的是类属性，通过隐式或显式传入的cls来操作
    def handle(cls, data):
        cls.a = data.a
        
    @staticmethod # 指定为静态方法，不与任何对象绑定，只是“碰巧”定义在了类中，与普通函数没有什么区别。
    def who_asked_you(person):
        pass

# Python 中的所谓“私有标记”只是约定俗成而已，硬要访问还是可以访问到的
# 实际上全部相当于 public

class Student(Human): # Python 中像这样继承，要继承多个的话就在括号内用逗号分隔
    pass
```

```c++
class Human{
    public: // 公有
        void set(int new_value); // 可以只声明不定义
        void get(void){ // 也可以直接定义
            
        }
        
    private: // 私有，从外部和子类中都不能访问
    	string name;
        int age;

    protected: // 受保护
        // 与 private 差不多，但在子类中能访问
        
    
}
void Human::set(int new_value){ // 定义成员函数 set，但开头需要用::表示属于哪个类
    age = new_value;
}

class Student: public Human{
    // C++ 中像这样继承，继承多个就用逗号分隔
    // 此处的 public 表示继承方式，不写默认是 private
    // public 继承：父类的成员属性都保持不变
    // private 继承：父类的成员全部变成private
    // protected 继承：父类的public成员变成protected，其余不变
    public:
        // 当成员函数的名字与类的名字相同时，相当于Python的 __init__()
        void Student(void){}
        // 用static定义静态成员函数，相当于Python中的 @staticmethod
        static void handle(void){}
}
```
