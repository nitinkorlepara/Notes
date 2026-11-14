 # Structural Design Patterns

Structural design patterns describe how classes and objects are composed to form larger, flexible structures. They reduce tight coupling and make it easier to extend or reuse existing code.

Common patterns include **Adapter**, **Decorator**, **Facade**, **Composite**, **Proxy**, **Bridge**, and **Flyweight**.

### Example: Decorator Pattern (Java)

The decorator adds behavior to an object without changing its original class.

```java
interface Coffee {
	String getDescription();
}

class SimpleCoffee implements Coffee {
	public String getDescription() { return "Coffee"; }
}

class MilkDecorator implements Coffee {
	private final Coffee coffee;

	MilkDecorator(Coffee coffee) { this.coffee = coffee; }

	public String getDescription() {
		return coffee.getDescription() + ", Milk";
	}
}

Coffee coffee = new MilkDecorator(new SimpleCoffee());
System.out.println(coffee.getDescription()); // Coffee, Milk
```

**Benefits:** flexibility, reuse, and adherence to the Open/Closed Principle.
