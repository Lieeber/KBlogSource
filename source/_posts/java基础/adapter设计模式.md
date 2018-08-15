---
title: 适配器模式
tags:
  - 设计模式
  - java
  - 适配器模式
categories:
  - java基础
date: 2018-6-12 12:18:15
---

### 适配器模式的定义

将一个接口转换成客户希望的另一个接口，适配器模式使接口不兼容的那些类可以一起工作。另外也称作包装器（Wrapper）


<!-- more -->

### 三个角色

Adapter(适配器接口):即目标角色，定义把其他类转换为何种接口，也就是我们期望的接口。

Adaptee(被适配角色):即源角色，一般是已存在的类，需要适配新的接口。

ConcreteAdapter(具体适配器):实现适配器接口，把源角色接口转换为目标角色期望的接口。

### 对象适配器具体实现
引用网上的一个例子：笔记本电脑电源一般用的都是5V电压，但是家用电是220V，我们要让笔记本充上电，最好的办法应该是通过一个工具把220V的电压转换成5V，这个工具就是适配器

#### 创建适配器接口
现在我们需要定义一个220V转换成5V的接口：

```java 
interface Adapter {//适配器类
    int convert5v();//装换成5V
}

```

#### 创建被适配角色
被适配角色，一般是已存在的类，需要适配新的接口。生活中的220V电源无处不在：

```java 
public class Electric {// 电源
    public int output220v() {//输出220V
        return 220;
    }
}

```

#### 创建具体适配器
我们需要一个具体适配器，这个适配器就是变压器，能够将220V转为5V输出：

```java 
public class PhoneAdapter implements Adapter {//手机适配器类
    private Electric mElectric;//适配器持有源目标对象

    public PhoneAdapter(Electric electric) {//通过构造方法传入对象
        mElectric = electric;
    }

    @Override
    public int convert5v() {
        System.out.println("适配器开始工作：");
        System.out.println("输入电压：" + mElectric.output220v());
        System.out.println("输出电压：" + 5);
        return 5;
    }
}

```

#### 测试
```java 
public void test() {
    Electric electric = new Electric();
    System.out.println("默认电压：" + electric.output_220v());
    Adapter phoneAdapter = new PhoneAdapter(electric);//传递一个对象给适配器
    System.out.println("适配转换后的电压：" + phoneAdapter.convert_5v());

    }
    
```
#### 输出结果
```javascript
默认电压：220
适配器开始工作：
输入电压：220
输出电压：5
适配转换后的电压：5

```

### 类适配器的实现

创建具体适配器时，使用的是继承而不是组合，其他的和对象适配器一样
```java 

public class PhoneAdapter extends Electric implements Adapter {//通过继承源目标类的方式，不持有源目标对象

    @Override
    public int convert_5v() {
        System.out.println("适配器开始工作：");
        System.out.println("输入电压：" + output_220v());
        System.out.println("输出电压：" + 5);
        return 5;
    }
}


```

### 对象适配器模式与类适配器模式比较
- 类适配器采用了继承的方式来实现;而对象适配器是通过传递对象来实现，这是一种组合的方式。
- 类适配器由于采用了继承，可以重写父类的方法;对象适配器则不能修改对象本身的方法等。
- 适配器通过继承都获得了父类的方法，客户端使用时都会把这些方法暴露出去，增加了一定的使用成本;对象适配器则不会。
- 类适配器只能适配他的父类，这个父类的其他子类都不能适配到;而对象适配器可以适配不同的对象，只要这个对象的类型是同样的。
- 类适配器不需要额外的引用;对象适配器需要额外的引用来保存对象。

总的来说，使用对象适配器比较好。


