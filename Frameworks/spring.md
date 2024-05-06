# Spring Framework

## Coupling 
#### Tight coupling
 ```java
public class GreetingService{
    public String sayHello(){
        return "Hello";
    }
}
public class Application{
    public static void main(String args[]){
    GreetingService service =new GreetingService();
    service.sayHello();
    }
}
 ``` 
#### Loose coupling
```java
public interface ServiceInterface{
    public String sayHello();
}
public class GreetingService implements ServiceInterface{
    public String sayHello(){
        return "Hello Spring";
    }
}
public class Application{
    public static void main(String args[]){
    ServiceInterface service =new GreetingService();
    service.sayHello();
    }
}
 ``` 
 <br>
 [link1](https://stackoverflow.com/questions/2832017/what-is-the-difference-between-loose-coupling-and-tight-coupling-in-the-object-o)
 [link2](https://www.geeksforgeeks.org/coupling-in-java/)
 
