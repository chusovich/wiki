# Design Patterns

## Chapter 1: Design Pattern Wa
rm Up
### What are Design Patterns?

a template for solving a commo
n problem
benefits

- no need to reinvent the whee
l
- tested and proven

- more readable code

- common vocabulary among deve
lopers
biggest caveat: knowing when t
o use them!
### Design Pattern Classification
#### Creational

separate system from how its o
bject are created and composed
- factor

- abstract factory

- builder

- prototype

#### Structural

looks for simple way to realiz
e relationships between entities
structure 

- MVC

- Façade

- Proxy

- Decorator

- Adapter

#### Behavioral

identify and realize common co
mmunication patterns between objects
- command 

- interpreter

- state

- chain of responsibility
- strategy
- observer
- memento
- template
- reactive design patterns

## Advanced Python Topics
### Iterables and Iterators
iterable: is an object that you can get an iterator from
iterator: an object with a next or __next__ method
list comprehension: transformation any iterable into a new list
### Decorators
decorator: a function that takes another function and extends the behavior of the second function without explicitly modifying it 

## Inheritance in Python
overriding: subclass implements logic for a function of the parent classs 
overloading: multiple functions with the same name but different arguments
```python 
super() calls the parent method

class.__bases__() # this returns parent class of class
class.__subclass__() # this returns the sub classes 
```
multiple inheritance
```python
# resolution order = order of inheritance priority
class.__mro__() # get method resolution
```
# Chapter 2: Producing with Factories