---
layout:     post
title:      "Python技术小结二"
subtitle:   "python小知识 "
date:       2018-08-21 14:45:00
author:     "Makes.Z"
header-img: "img/post-think-try-write.jpg"
tags:
    - Python
---

## python小知识。

1.python中的接口
    一:在python的语法中并没有像Java那样有专门的声明定义接口的存在，它是依靠抽象类
实现完成的。使用abc模块，@abstractmethod是声明抽象函数的，@abstractproperty声明
抽象属性。

      ```
        from abc import ABCMeta,abstractmethod
        class Payment(metaclass=ABCMeta):
            @abstractmethod                 #调用@abstractmethod规定子类必须有pay方法
            def pay(self,money):
            pass

        class Wechatpay(Payment):
            def pay(self,money):
                print('微信支付了%s元'%money)
            obj = Wechatpay()
      ```
    二:还可以使用第三方提供的python接口，zope.interface和python-interface，使用

    sudo pip install python-interface


    抽象接口
    ```
    from interface import Interface

    class MyInterface(Interface):

        def method1(self):
            pass

        def method2(self, arg1, arg2):
            pass
    ```
    实现接口
    ```
    from interface import implements

    class MyClass(implements(MyInterface)):

        def method1(self):
            return "method1"

        def method2(self, arg1, arg2):
            return "method2"
    ```

    以上就是比较常用的两种python接口使用的方式

2.鸭子类型
    在python中有一种很特殊的类型称之为鸭子类型，那么什么叫鸭子类型呢。

    “当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。”

    在鸭子类型中，关注的不是对象类型的本身，而是如何使用该对象。

    ```
    class A:    
    def prt(self):    
        print "A"    

    class B(A):    
        def prt(self):    
            print "B"    

    class C(A):    
        def prt(self):    
            print "C"    

    class D(A):    
        pass    

    class E:    
        def prt(self):    
            print "E"    

    class F:    
        pass    

    def test(arg):    
        arg.prt()    

    a = A()    
    b = B()    
    c = C()    
    d = D()    
    e = E()    
    f = F()    

    test(a)    
    test(b)    
    test(c)    
    test(d)    
    test(e)    
    test(f)   
    ```
    运行结果如下:
    ---

    A  
    B  
    C  
    A  
    E  
    Traceback (most recent call last):  
      File "/Users/shikefu678/Documents/Aptana Studio 3 Workspace/demo/demo.py", line 33, in <module>  
        test(a),test(b),test(c),test(d),test(e),test(f)  
      File "/Users/shikefu678/Documents/Aptana Studio 3 Workspace/demo/demo.py", line 24, in test  
        arg.prt()  
    AttributeError: F instance has no attribute 'prt'  
    ---
    a，b，c，d都是A类型的变量，所以可以得到预期的效果（从java角度的预期），e并不是A类型的变量但是根
    据鸭子类型，走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子，e有prt方法，
    所以在test方法中e就是一个A类型的变量，f没有prt方法，所以f不是A类型的变量。
