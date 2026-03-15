[
![designpattern](https://user-images.githubusercontent.com/5803001/36413335-ddd675f0-1658-11e8-9326-4f4eb7aace4e.png)
](https://www.processon.com/view/link/5a8bd7f3e4b064e9ddc6783e)

# Design Pattern CheatSheet

Design patterns are solutions to recurring problems; guidelines on how to tackle certain problems. They are not classes, packages or libraries that you can plug into your application and wait for the magic to happen. These are, rather, guidelines on how to tackle certain problems in certain situations.

Design patterns are not a silver bullet to all your problems.
Do not try to force them; bad things are supposed to happen, if done so.
Keep in mind that design patterns are solutions to problems, not solutions finding problems; so don't overthink.
If used in a correct place in a correct manner, they can prove to be a savior; or else they can result in a horrible mess of a code.

# Creational Design Patterns

Creational patterns are focused towards how to instantiate an object or group of related objects.

## Simple Factory

In object-oriented programming (OOP), a factory is an object for creating other objects – formally a factory is a function or method that returns objects of a varying prototype or class from some method call, which is assumed to be "new".

Simple factory simply generates an instance for client without exposing any instantiation logic to the client

When creating an object is not just a few assignments and involves some logic, it makes sense to put it in a dedicated factory instead of repeating the same code everywhere.

## Factory Method

It provides a way to delegate the instantiation logic to child classes.

Useful when there is some generic processing in a class but the required sub-class is dynamically decided at runtime. Or putting it in other words, when the client doesn't know what exact sub-class it might need.

## Abstract Factory

A factory of factories; a factory that groups the individual but related/dependent factories together without specifying their concrete classes.

When there are interrelated dependencies with not-that-simple creation logic involved.

## Builder

Allows you to create different flavors of an object while avoiding constructor pollution. Useful when there could be several flavors of an object. Or when there are a lot of steps involved in creation of an object.

When there could be several flavors of an object and to avoid the constructor telescoping. The key difference from the factory pattern is that; factory pattern is to be used when the creation is a one step process while builder pattern is to be used when the creation is a multi step process.

## Prototype

Create object based on an existing object through cloning.

In short, it allows you to create a copy of an existing object and modify it to your needs, instead of going through the trouble of creating an object from scratch and setting it up.

When an object is required that is similar to existing object or when the creation would be expensive as compared to cloning.

## Singleton

Ensures that only one object of a particular class is ever created.

Singleton pattern is actually considered an anti-pattern and overuse of it should be avoided. It is not necessarily bad and could have some valid use-cases but should be used with caution because it introduces a global state in your application and change to it in one place could affect in the other areas and it could become pretty difficult to debug. The other bad thing about them is it makes your code tightly coupled plus mocking the singleton could be difficult.

# Structural Design Patterns

Structural patterns are mostly concerned with object composition or in other words how the entities can use each other. Or yet another explanation would be, they help in answering "How to build a software component?"

# Behavioral Design Patterns

It is concerned with assignment of responsibilities between the objects. What makes them different from structural patterns is they don't just specify the structure but also outline the patterns for message passing/communication between them. Or in other words, they assist in answering "How to run a behavior in software component?"
