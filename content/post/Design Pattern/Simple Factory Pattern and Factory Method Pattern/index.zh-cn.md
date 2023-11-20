---
title: 简单工厂模式 和 工厂方法模式
description: Simple Factory Pattern and Factory Method Pattern
date: '2020-09-10'
categories:
    - Design Pattern
tags:
    - Design Pattern
    - Java
---

# 简单工厂模式 和 工厂方法模式

## 简单工厂模式

### 简单工厂模式概念

&nbsp;&nbsp;&nbsp;&nbsp;简单工厂模式并不属于GoF的23种经典设计模式，但通常将它作为学习其他工厂模式的基础。

&nbsp;&nbsp;&nbsp;&nbsp;**简单工厂模式（Simple Factory Pattern）：** 定义一个工厂类，它可以根据参数的不同返回不同类的实例，被创建的实例通常都具有共同的父类。

### 简单工厂模式结构

&nbsp;&nbsp;&nbsp;&nbsp;**简单工厂模式结构：** 简单工厂模式的结构比较简单，其核心是工厂类的设计。

![Simple Factory Pattern Structure](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Design%20Pattern/Simple%20Factory%20Pattern%20and%20Factory%20Method%20Pattern/simple-factory-pattern-and-factory-method-pattern1.png)

&nbsp;&nbsp;&nbsp;&nbsp;**（1）Factory（工厂角色）：** 工厂角色即工厂类，它是简单工厂模式的核心，负责实现创建所有产品实例的内部逻辑；工厂类可以被外界直接调用，创建所需的产品对象；在工厂类中提供了静态的工厂方法factoryMethod()，它的返回类型为抽象产品类型Product。

&nbsp;&nbsp;&nbsp;&nbsp;**（2）Product（抽象产品角色）：** 它是工厂类创建的所有对象的父类，封装了各种产品对象的公有方法，它的引入将提高系统的灵活性，使得在工厂类中只需定义一个通用的工厂方法，因为所有创建的具体产品对象都是其子类对象。

&nbsp;&nbsp;&nbsp;&nbsp;**（3）ConcreteProduct（具体产品角色）：** 它是简单工厂模式的创建目标，所有被创建的对象都充当这个角色的某个具体类的实例。每一个具体产品角色都继承了抽象产品角色，需要实现在抽象产品中声明的抽象方法。

### 简单工厂模式实现

&nbsp;&nbsp;&nbsp;&nbsp;典型的抽象产品类代码如下：

```java
public abstract class Product {
	//所有产品类的公共业务方法
	public void methhodSame() {
		//公共方法的实现
	}

	//声明抽象业务方法
	public abstract void methodDiff();
}
```
&nbsp;&nbsp;&nbsp;&nbsp;典型的具体产品类的代码如下：
```java
public class ConcreteProduct extends Product {
	//实现业务方法
	public void methodDiff() {
		//业务方法实现
	}
}
```
&nbsp;&nbsp;&nbsp;&nbsp;典型的工厂类的代码如下：
```java
public class Factory {
	//静态工厂方法
	public static Product getProduct(String arg) {
		Product product = null;
		if (arg.equalsIgnoreCase("A")) {
			product = new ConcreteProductA();
			//初始化设置product
		}
		else if (arg.equalsIgnoreCase("B")) {
			product = new ConcreteProductB();
			//初始化设置product
		}
		return product;
	}
}
```

&nbsp;&nbsp;&nbsp;&nbsp;在客户端代码中，通过调用工厂类的工厂方法即可得到产品对象。其典型代码如下：

```java
public class Client {
	public static void main(String[] args) {
		Product product;
		product = Factory.getProduct("A");//通过工厂类创建产品对象
		product.methodSame();
		product.methodDiff();
	}
}
```

### 简单工厂模式优缺点和适用环境

&nbsp;&nbsp;&nbsp;&nbsp;**简单工厂模式优点**

&nbsp;&nbsp;&nbsp;&nbsp;（1）工厂类包含必要的判断逻辑，可以决定在什么时候创建哪一个产品类的实例，客户端可以免除直接创建产品对象的职责，而仅仅“消费”产品，简单工厂模式实现了对象创建和使用的分离。

&nbsp;&nbsp;&nbsp;&nbsp;（2）客户端无须知道所创建的具体产品类的类名，只需要知道具体产品类所对应的参数即可，对于一些复杂的类名，通过简单工厂模式可以在一定程度上减少使用者的记忆量。

&nbsp;&nbsp;&nbsp;&nbsp;（3）通过引入配置文件，可以在不修改任何客户端代码的情况下更换和增加新的具体产品类，在一定程度上提高了系统的灵活性。

&nbsp;&nbsp;&nbsp;&nbsp;**简单工厂模式缺点**

&nbsp;&nbsp;&nbsp;&nbsp;（1）由于工厂类集中了所有产品的创建逻辑，职责过重，一旦不能正常工作，整个系统都要受到影响。

&nbsp;&nbsp;&nbsp;&nbsp;（2）使用简单工厂模式势必会增加系统中类的个数（引入了新的工厂类），增加了系统的负责度和理解程度。

&nbsp;&nbsp;&nbsp;&nbsp;（3）系统扩展困难，一旦添加新产品就不得不修改工厂逻辑，在产品类型较多时有可能造成工厂逻辑过于复杂，不利于系统的扩展和维护。

&nbsp;&nbsp;&nbsp;&nbsp;（4）简单工厂模式由于使用静态工厂方法，造成工厂角色无法形成基于继承的等级结构。

&nbsp;&nbsp;&nbsp;&nbsp;**简单工厂模式适用环境**

&nbsp;&nbsp;&nbsp;&nbsp;（1）工厂类负责创建的对象比较少，由于创建的对象比较少，由于创建的对象较少，不会造成工厂方法中的业务逻辑过于复杂。

&nbsp;&nbsp;&nbsp;&nbsp;（2）客户端只知道传入工厂类的参数，对于如何创建对象并不关心。

## 工厂方法模式

### 工厂方法模式概念

&nbsp;&nbsp;&nbsp;&nbsp;在工厂方法模式中不再提供一个统一的工厂类来创建所有的产品对象，而是针对不同的产品提供不同的工厂，系统提供一个与产品等级结构对应的工厂等级结构。

&nbsp;&nbsp;&nbsp;&nbsp;**工厂方法模式：** 定义一个用于创建对象的接口，但是让子类决定将哪一个类实例化。工厂方法模式让一个类的实例化延迟到其子类。

### 工厂方法模式结构

&nbsp;&nbsp;&nbsp;&nbsp;**工厂方法模式结构：** 工厂方法模式提供一个抽象工厂接口来声明抽象工厂方法，而由其子类来具体实现工厂方法，创建具体的产品对象。

![Factory Method Pattern Structure](https://raw.githubusercontent.com/JavenJin/blog-image/master/content/post/Design%20Pattern/Simple%20Factory%20Pattern%20and%20Factory%20Method%20Pattern/simple-factory-pattern-and-factory-method-pattern2.png)

&nbsp;&nbsp;&nbsp;&nbsp;**（1）Product（抽象产品）：** 它是定义产品的接口，是工厂方法模式所创建对象的超类型，也就是产品对象的公共父类。

&nbsp;&nbsp;&nbsp;&nbsp;**（2）ConcreteProduct（具体产品）：** 它实现了抽象产品接口，某种类型的具体产品由专门的具体工厂创建，具体工厂和具体产品之间一一对应。

&nbsp;&nbsp;&nbsp;&nbsp;**（3）Factory（抽象工厂）：** 在抽象工厂类中声明了工厂方法（Factory Method），用于返回一个产品。抽象工厂是工厂方法模式的核心，所有创建对象的工厂类都必须实现该接口。

&nbsp;&nbsp;&nbsp;&nbsp;**（4）ConcreteFactory（具体工厂）：** 它是抽象工厂类的子类，实现了在抽象工厂中声明的工厂方法，并可由客户端调用，返回一个具体产品类的实例。

### 工厂方法模式实现

&nbsp;&nbsp;&nbsp;&nbsp;与简单工厂模式相比，工厂方法模式最重要的特点是引入了抽象工厂角色，抽象工厂可以是接口，也可以是抽象类或者具体类。其典型代码如下：

```java
public interface Factory {
	public Product factoryMethod();
}
```

&nbsp;&nbsp;&nbsp;&nbsp;在抽象工厂中声明了工厂方法但并未实现工厂方法，具体产品对象的创建由其子类负责，客户端针对抽象工厂编程，可在运行时再指定具体工厂类，具体工厂类实现了工厂方法，不同的具体工厂可以创建不同的具体产品。其典型代码如下：

```java
public class ConcreteFactory implements Factory {
	public Product factoryMethod() {
		return new ConcreteProduct();
	}
}
```

&nbsp;&nbsp;&nbsp;&nbsp;在实际使用时，具体工厂类在实现工厂方法时除了创建具体产品对象之外，还可以负责产品对象的初始化工作以及一些资源和环境配置工作，例如连接数据库、创建文件等。

&nbsp;&nbsp;&nbsp;&nbsp;在客户端代码中，开发人员只需关心工厂类即可，不同的具体工厂可以创建不同的产品。典型的客户端代码片段如下：

```java
···
Factory factory;
factory = new ConcreteFactory();
Product product;
product = factory.factoryMethod();
···
```

&nbsp;&nbsp;&nbsp;&nbsp;可以通过配置文件来存储具体工厂类ConcreteFactory的类名，再通过反射机制创建具体工厂对象，在更换新的具体工厂时无须修改源代码，系统扩展更为方便。

### 工厂方法模式优缺点和适用环境

&nbsp;&nbsp;&nbsp;&nbsp;**工厂方法模式优点**

&nbsp;&nbsp;&nbsp;&nbsp;（1）在工厂方法模式中，工厂方法用来创建客户所需要的产品，同时还向客户隐藏了哪种具体产品类将被实例化这一细节，用户只需要关心所需产品对应的工厂，无须关心创建细节，甚至无须知道具体产品类的类名。

&nbsp;&nbsp;&nbsp;&nbsp;（2）基于工厂角色和产品角色的多态性设计是工厂方法模式的关键。它能够让工厂自主确定创建何种产品对象，而如何创建这个对象的细节完全封装在具体工厂内部。工厂方法模式之所以又被称为多态工厂模式，正是因为所有的具体工厂类都具有同一抽象父类。

&nbsp;&nbsp;&nbsp;&nbsp;（3）使用工厂方法模式的另一个优先是在系统中加入新产品时无须修改抽象工厂和抽象产品提供的接口，无须修改客户端，也无须修改其他的具体工厂和具体产品，而只要添加一个具体工厂和具体产品即可，这样系统的可扩展性也就变的非常好，完全符合开闭原则。

&nbsp;&nbsp;&nbsp;&nbsp;**工厂方法模式缺点**

&nbsp;&nbsp;&nbsp;&nbsp;（1）在添加新产品时需要编写新的具体产品类，而且还要提供与之对应的具体工厂类，系统中类的个数将成对增加，在一定程度上增加了系统的复杂度，有更多的类需要编译和运行，会给系统带来一些额外的开销。

&nbsp;&nbsp;&nbsp;&nbsp;（2）由于考虑到系统的可扩展性，需要引入抽象层，在客户端代码中均使用抽象层进行定义，增加了系统的抽象性和理解难度。

&nbsp;&nbsp;&nbsp;&nbsp;**工厂方法模式适用环境**

&nbsp;&nbsp;&nbsp;&nbsp;（1）客户端不知道它所需要的对象的类。在工厂方法模式中，客户端不需要知道具体产品类的类名，只需要知道所对应的工厂即可，具体产品对象由具体工厂类创建，可将具体工厂类的类名存储在配置文件或数据库中。

&nbsp;&nbsp;&nbsp;&nbsp;（2）抽象工厂类通过其子类来指定创建那个对象。在工厂方法模式中，对于抽象工厂类只需要提供一个创建产品的接口，而由其子类来确定具体要创建的对象，利用面向对象的多态性和里氏代换原则，在程序运行时子类对象将覆盖父类对象，从而使得系统更容易扩展。

## “简单工厂模式”和“工厂方法模式”区别

&nbsp;&nbsp;&nbsp;&nbsp;（1）简单工厂模式在需要增加新的产品类时困难，需要改变原有的代码，不符合开闭原则；而工厂方法模式在增加新的产品类时不需要改变原有代码，完全符合开闭原则。

&nbsp;&nbsp;&nbsp;&nbsp;（2）工厂方法模式比简单工厂模式更复杂，更抽象，更耗费系统资源，更难以理解。

&nbsp;&nbsp;&nbsp;&nbsp;（3）简单工厂模式中工厂类集中了所有产品的创建逻辑，一旦不能正常工作，整个系统都会受到影响；而工厂方法模式将职责分化到每个工厂类，降低了每个类的职责。
