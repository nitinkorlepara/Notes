 # Design Patterns — Quick Overview

Design patterns are reusable approaches to common software design problems. They are guidelines, not ready-made code.

## 1. Creational Patterns

Control how objects are created.

- **Singleton:** Ensures only one instance exists.
- **Factory Method:** Lets subclasses decide which object to create.
- **Abstract Factory:** Creates related families of objects.
- **Builder:** Constructs complex objects step by step.
- **Prototype:** Creates objects by cloning existing ones.

## 2. Structural Patterns

Define how classes and objects are composed.

- **Adapter:** Makes incompatible interfaces work together.
- **Decorator:** Adds behavior dynamically without changing the original class.
- **Facade:** Provides a simple interface to a complex subsystem.
- **Proxy:** Controls access to another object.
- **Composite:** Treats individual objects and groups uniformly.
- **Bridge:** Separates abstraction from implementation.
- **Flyweight:** Shares common state to reduce memory usage.

## 3. Behavioral Patterns

Manage communication and responsibility between objects.

- **Observer:** Notifies dependent objects when state changes.
- **Strategy:** Encapsulates interchangeable algorithms.
- **Command:** Encapsulates a request as an object.
- **State:** Changes behavior when an object's state changes.
- **Template Method:** Defines an algorithm skeleton with customizable steps.
- **Chain of Responsibility:** Passes a request along a chain of handlers.
- **Mediator:** Centralizes communication between objects.
- **Iterator:** Traverses a collection without exposing its structure.
- **Memento:** Captures and restores an object's state.

## Choosing a Pattern

First identify the problem—object creation, structure, or behavior—then select the simplest pattern that improves flexibility, maintainability, or reuse. Avoid using patterns unnecessarily.
