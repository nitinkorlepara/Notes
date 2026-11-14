## Behavioral Design Patterns

Behavioral design patterns focus on communication and responsibility between objects. They make it easier to change how objects interact without tightly coupling them.

Common examples include **Strategy**, **Observer**, **Command**, **State**, and **Chain of Responsibility**.

### Example: Strategy Pattern

The Strategy pattern encapsulates interchangeable algorithms behind a common interface.

```java
interface PaymentStrategy {
	void pay(int amount);
}

class UpiPayment implements PaymentStrategy {
	public void pay(int amount) {
		System.out.println("Paid ₹" + amount + " using UPI");
	}
}

class Checkout {
	private final PaymentStrategy strategy;

	Checkout(PaymentStrategy strategy) {
		this.strategy = strategy;
	}

	void pay(int amount) {
		strategy.pay(amount);
	}
}

// Usage: new Checkout(new UpiPayment()).pay(500);
```

**Benefit:** New payment methods can be added without modifying `Checkout`.

### Observer Pattern

The Observer pattern lets an object notify multiple dependents when its state changes.

```java
interface Observer { void update(String message); }

class Subscriber implements Observer {
	public void update(String message) { System.out.println(message); }
}

class NewsChannel {
	private final List<Observer> observers = new ArrayList<>();

	void subscribe(Observer observer) { observers.add(observer); }
	void publish(String news) {
		for (Observer observer : observers) observer.update(news);
	}
}
```

**Benefit:** Publishers and subscribers remain loosely coupled.

### Command Pattern

The Command pattern encapsulates a request as an object.

```java
interface Command { void execute(); }

class Light { void on() { System.out.println("Light on"); } }
class TurnOnCommand implements Command {
	private final Light light;
	TurnOnCommand(Light light) { this.light = light; }
	public void execute() { light.on(); }
}

class Remote { void press(Command command) { command.execute(); } }
```

**Benefit:** Commands can be queued, logged, or undone.

### State Pattern

The State pattern changes an object's behavior when its internal state changes.

```java
interface VendingState { void insertCoin(VendingMachine machine); }

class NoCoinState implements VendingState {
	public void insertCoin(VendingMachine machine) {
		System.out.println("Coin accepted");
		machine.setState(new HasCoinState());
	}
}
class HasCoinState implements VendingState {
	public void insertCoin(VendingMachine machine) { System.out.println("Already paid"); }
}
class VendingMachine {
	private VendingState state = new NoCoinState();
	void setState(VendingState state) { this.state = state; }
	void insertCoin() { state.insertCoin(this); }
}
```

**Benefit:** State-specific behavior is separated from a large conditional block.

### Chain of Responsibility Pattern

This pattern passes a request along a chain until a handler processes it.

```java
abstract class Handler {
	private Handler next;
	Handler next(Handler next) { this.next = next; return next; }
	void handle(int amount) {
		if (next != null) next.handle(amount);
	}
}

class Manager extends Handler {
	public void handle(int amount) {
		if (amount <= 1000) System.out.println("Manager approved");
		else super.handle(amount);
	}
}
```

**Benefit:** The sender does not need to know which object handles the request.

### Template Method Pattern

The Template Method pattern defines an algorithm's skeleton while allowing subclasses to customize steps.

```java
abstract class DataProcessor {
	final void process() { read(); parse(); save(); }
	abstract void read();
	abstract void parse();
	void save() { System.out.println("Saved data"); }
}
```

**Benefit:** Common workflow is reused while selected steps remain extensible.

### Iterator Pattern

The Iterator pattern provides sequential access to a collection without exposing its representation.

```java
class NameCollection implements Iterable<String> {
	private final List<String> names = List.of("Asha", "Ravi");
	public Iterator<String> iterator() { return names.iterator(); }
}

// for (String name : new NameCollection()) { System.out.println(name); }
```

**Benefit:** Collection traversal is consistent and independent of storage details.

### Mediator Pattern

The Mediator pattern centralizes communication between related objects.

```java
class ChatRoom {
	void send(String message, User sender) { System.out.println(sender.name + ": " + message); }
}
class User {
	final String name; private final ChatRoom room;
	User(String name, ChatRoom room) { this.name = name; this.room = room; }
	void send(String message) { room.send(message, this); }
}
```

**Benefit:** Components communicate through one coordinator instead of many direct links.

### Memento Pattern

The Memento pattern captures and restores an object's state without exposing its internals.

```java
record EditorMemento(String text) {}
class Editor {
	private String text = "";
	void write(String text) { this.text = text; }
	EditorMemento save() { return new EditorMemento(text); }
	void restore(EditorMemento memento) { text = memento.text(); }
}
```

**Benefit:** Undo and restore operations can be implemented safely.

### Visitor Pattern

The Visitor pattern adds operations to object structures without changing their classes.

```java
interface Shape { void accept(ShapeVisitor visitor); }
interface ShapeVisitor { void visit(Circle circle); }
class Circle implements Shape {
	public void accept(ShapeVisitor visitor) { visitor.visit(this); }
}
class AreaVisitor implements ShapeVisitor {
	public void visit(Circle circle) { System.out.println("Calculate circle area"); }
}
```

**Benefit:** New operations can be added without modifying stable element classes.

### Interpreter Pattern

The Interpreter pattern represents a grammar and evaluates expressions in that language.

```java
interface Expression { boolean interpret(String context); }
class EqualsExpression implements Expression {
	private final String expected;
	EqualsExpression(String expected) { this.expected = expected; }
	public boolean interpret(String context) { return expected.equals(context); }
}
```

**Benefit:** Small, rule-based languages can be extended by adding expression classes.

