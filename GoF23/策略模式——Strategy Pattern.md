# 策略模式——Strategy Pattern

策略模式定义了算法族，并将算法族分别封装起来，让它们之间可以**互相替换**（即一个类的行为或其算法可以在运行时更改），此模式让算法的变化独立于使用算法的客户。

**使用场景：**

1、如果在一个系统里面有许多类，它们之间的区别仅在于它们的行为，那么使用策略模式可以动态地让一个对象在许多行为中选择一种行为。

2、一个系统需要动态地在几种算法中选择一种。 

3、如果一个对象有很多的行为，如果不用恰当的模式，这些行为就只好使用多重的条件选择语句来实现。

**优点：**

1、算法可以自由切换。 

2、避免使用多重条件判断。 

3、扩展性良好。

**缺点：** 

1、策略类会增多。 

2、所有策略类都需要对外暴露。

**注意事项：**

如果一个系统的策略多于四个，就需要考虑使用混合模式，解决策略类膨胀的问题。

类图：

![Strategy Pattern-导出](D:\JavaNote\GoF23\UML.assets\Strategy Pattern-导出.png)

举例：

#### Step1 创建一个接口

##### Strategy.java

```java
public interface Strategy {   
	public int doOperation(int num1, int num2);
}
```



#### Step2 创建实现接口的实体类

##### OperationAdd.java

```java
public class OperationAdd implements Strategy{
    @Override   
    public int doOperation(int num1, int num2) {
    	return num1 + num2;   
    } 
}
```



##### OperationSubtract.java

```java
public class OperationSubtract implements Strategy{   
    @Override   
    public int doOperation(int num1, int num2) {
    	return num1 - num2;   
    } 
}
```



##### OperationMultiply.java

```java
public class OperationMultiply implements Strategy{
    @Override   
    public int doOperation(int num1, int num2) { 
    	return num1 * num2;   
    } 
}
```



#### Step3 创建 *Context* 类。

##### Context.java

```java
public class Context {   
    private Strategy strategy; 
    
    public Context(){
        
    }    
    
    public int executeStrategy(int num1, int num2){   
        return strategy.doOperation(num1, num2); 
    } 
    
    public void setStrategy(Strategy strategy){
        this.strategy = strategy;
    }
}
```



#### Step4 使用 *Context* 来查看当它改变策略 *Strategy* 时的行为变化。

##### StrategyPatternDemo.java

```java
public class StrategyPatternDemo {   
    public static void main(String[] args) {      
    	Context context = new Context();
        context.setStrategy(new OperationAdd());
        System.out.println("10 + 5 = " + context.executeStrategy(10, 5));  
    	context.setStrategy(new OperationSubtract());          
        System.out.println("10 - 5 = " + context.executeStrategy(10, 5));    
    	context.setStrategy(new OperationMultiply());
        System.out.println("10 * 5 = " + context.executeStrategy(10, 5));   
    } 
}
```



#### Step5 执行程序，输出结果：

```java
10 + 5 = 15
10 - 5 = 5
10 * 5 = 50
```