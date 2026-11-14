 # Creational Design Patterns

Creational patterns focus on **how objects are created**, while hiding creation details and making code easier to extend and test.

## 1. Singleton

Ensures that a class has only one instance and provides a global access point.

```java
public final class Database {
	private Database() {}

	private static class Holder {
		private static final Database INSTANCE = new Database();
	}

	public static Database getInstance() {
		return Holder.INSTANCE;
	}
}
```

**Use when:** one shared, stateless resource is required, such as a configuration or connection manager. Avoid it when global state makes testing difficult.

## 2. Factory Method

Defines an interface for creating an object, allowing subclasses or methods to decide the concrete type.

```java
interface Notification {
	void send(String message);
}

class EmailNotification implements Notification {
	public void send(String message) { System.out.println("Email: " + message); }
}

class SmsNotification implements Notification {
	public void send(String message) { System.out.println("SMS: " + message); }
}

class NotificationFactory {
	static Notification create(String type) {
		return switch (type.toLowerCase()) {
			case "email" -> new EmailNotification();
			case "sms" -> new SmsNotification();
			default -> throw new IllegalArgumentException("Unknown type: " + type);
		};
	}
}
```

## 3. Abstract Factory

Creates **families of related objects** without specifying their concrete classes.

```java
interface Button { void render(); }
interface Checkbox { void check(); }

interface UiFactory {
	Button createButton();
	Checkbox createCheckbox();
}

class DarkButton implements Button {
	public void render() { System.out.println("Dark button"); }
}
class DarkCheckbox implements Checkbox {
	public void check() { System.out.println("Dark checkbox"); }
}
class DarkUiFactory implements UiFactory {
	public Button createButton() { return new DarkButton(); }
	public Checkbox createCheckbox() { return new DarkCheckbox(); }
}
```

**Use when:** objects must be compatible, such as light and dark UI components.

## 4. Builder

Constructs complex objects step by step, especially when there are many optional fields.

```java
class User {
	private final String name;
	private final String email;
	private final int age;

	private User(Builder b) {
		this.name = b.name;
		this.email = b.email;
		this.age = b.age;
	}

	static class Builder {
		private final String name;
		private String email;
		private int age;

		Builder(String name) { this.name = name; }
		Builder email(String email) { this.email = email; return this; }
		Builder age(int age) { this.age = age; return this; }
		User build() { return new User(this); }
	}
}

User user = new User.Builder("Nitin")
		.email("nitin@example.com")
		.age(25)
		.build();
```

## 5. Prototype

Creates new objects by copying an existing object, useful when construction is expensive.

```java
class Report implements Cloneable {
	String title;
	String content;

	Report(String title, String content) {
		this.title = title;
		this.content = content;
	}

	public Report clone() {
		try {
			return (Report) super.clone();
		} catch (CloneNotSupportedException e) {
			throw new AssertionError(e);
		}
	}
}

Report copy = new Report("Template", "Default content").clone();
```

## Quick comparison

| Pattern | Main idea | Typical use |
|---|---|---|
| Singleton | One shared instance | Configuration manager |
| Factory Method | Create one product type | Notification creation |
| Abstract Factory | Create related products | UI themes |
| Builder | Step-by-step construction | Complex request objects |
| Prototype | Copy an existing object | Expensive object creation |

### Selection guide

- Need exactly one instance? **Singleton**
- Need to choose one implementation? **Factory Method**
- Need matching groups of implementations? **Abstract Factory**
- Need readable construction with optional fields? **Builder**
- Need fast copies of an existing object? **Prototype**
