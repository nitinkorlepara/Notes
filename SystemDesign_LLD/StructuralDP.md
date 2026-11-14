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

## Adapter

The adapter converts one interface into another interface expected by clients.

```java
interface PaymentProcessor {
	void pay(double amount);
}

class LegacyPaymentGateway {
	void makePayment(double amount) { System.out.println("Paid: " + amount); }
}

class PaymentAdapter implements PaymentProcessor {
	private final LegacyPaymentGateway gateway;

	PaymentAdapter(LegacyPaymentGateway gateway) { this.gateway = gateway; }

	public void pay(double amount) { gateway.makePayment(amount); }
}
```

**Benefits:** integrates legacy or third-party code without modifying it.

## Facade

The facade provides a simple interface to a complex subsystem.

```java
class CPU { void start() { System.out.println("CPU started"); } }
class Memory { void load() { System.out.println("Memory loaded"); } }
class Disk { void read() { System.out.println("Disk read"); } }

class ComputerFacade {
	private final CPU cpu = new CPU();
	private final Memory memory = new Memory();
	private final Disk disk = new Disk();

	void start() {
		cpu.start();
		memory.load();
		disk.read();
	}
}
```

**Benefits:** reduces coupling and hides subsystem complexity.

## Composite

The composite lets clients treat individual objects and groups of objects uniformly.

```java
interface FileSystemItem { void show(); }

class FileItem implements FileSystemItem {
	private final String name;
	FileItem(String name) { this.name = name; }
	public void show() { System.out.println(name); }
}

class Directory implements FileSystemItem {
	private final String name;
	private final java.util.List<FileSystemItem> children = new java.util.ArrayList<>();
	Directory(String name) { this.name = name; }
	void add(FileSystemItem item) { children.add(item); }
	public void show() {
		System.out.println(name);
		for (FileSystemItem child : children) child.show();
	}
}
```

**Benefits:** simplifies tree structures and client code.

## Proxy

The proxy controls access to another object, often for security, lazy loading, or caching.

```java
interface Image { void display(); }

class RealImage implements Image {
	private final String file;
	RealImage(String file) { this.file = file; load(); }
	private void load() { System.out.println("Loading " + file); }
	public void display() { System.out.println("Displaying " + file); }
}

class ImageProxy implements Image {
	private final String file;
	private RealImage image;
	ImageProxy(String file) { this.file = file; }
	public void display() {
		if (image == null) image = new RealImage(file);
		image.display();
	}
}
```

**Benefits:** adds control and defers expensive operations.

## Bridge

The bridge separates an abstraction from its implementation so both can vary independently.

```java
interface Device { void turnOn(); }

class TV implements Device {
	public void turnOn() { System.out.println("TV on"); }
}

abstract class Remote {
	protected final Device device;
	Remote(Device device) { this.device = device; }
	abstract void powerOn();
}

class BasicRemote extends Remote {
	BasicRemote(Device device) { super(device); }
	void powerOn() { device.turnOn(); }
}
```

**Benefits:** avoids a permanent class hierarchy and supports independent extension.

## Flyweight

The flyweight shares immutable intrinsic state to reduce memory usage.

```java
class TreeType {
	private final String name;
	TreeType(String name) { this.name = name; }
	void draw(int x, int y) { System.out.println(name + " at " + x + "," + y); }
}

class TreeFactory {
	private static final java.util.Map<String, TreeType> types = new java.util.HashMap<>();

	static TreeType get(String name) {
		return types.computeIfAbsent(name, TreeType::new);
	}
}
```

**Benefits:** reduces the number of objects and saves memory when state is shared.
