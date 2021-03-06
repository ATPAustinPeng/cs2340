# Code Smells
- Martin Fowler: "a code smell is a surface indication that usually corresponds to a deeper problem in the system"
	- something that is quick to spot
	- indicator of a bigger problem with your code
- generally, you find code smells when examining the code, or doing refactoring

## Where Do Code Smells Come From?
- not always programmer ignorance
- usually comes from a rushed design and a disregard for technical debt (the amount of work you create when you try to ave time up front)
	- do it the right way - use best practices and develop a design that can scale and grow; takes longer
	- do it the fast way - "hacked together" design; faster

## Design Stamina Hypothesis
<img src="img/l13-design-stamina-hypothesis.png" alt="design-stamina-hypothesis" width="600">

## Taxonomy For Bad Code Smells by Mantyla and Lassenius
|Group Name|Smells In Group|
|-|-|
|bloaters|long method, large class, long parameter list, data clumps|
|object-orientation abusers|switch statements, refused bequest|
|change preventers|divergent change, shotgun surgery|
|dispensables|lazy class, data class, duplicated code|
|couplers|feature envy, inappropriate intimacy, middle man|

### Bloaters: Large Class, Long Method
- when a class is trying to do too much, it often has too many instance variables
- object programs with short methods live longest
	- the longer the method is, the harder it is to understand
	- possible heuristic -> whenever you feel the need to comment something, write a method instead

### Bloaters: Data Clumps
- with data clumps there exists a set of primitives that always appear together (ex. 3 integers for RGB colors)
- since these data items are not encapsulated in a class this increases the sizes of methods and classes

### Bloaters: Long Parameter List
- more than three or four parameters for a method
- hard to understand such lists
- reasons for the problem
- several types of algorithm are merged in a single method

### Object-Orientation Abusers: Switch Statements
- you have a complex switch operator or a sequence of if statements
- relatively rare use of switch and case operators is one of the hallmarks of object-oriented code

### Object-Orientation Abusers: Refused Bequest
- subclasses inherit the methods and data of their parents, but they do not want what they are given
- the unneeded methods may simply go unused or be redefined and give off exceptions
- possible reason -> someone was motivated to create inheritance between classes only by the desire to reuse code in a superclass

### Change Preventers: Shotgun Surgery
- every time you make a change, you must make changes to a lot of classes
- symptom that functionality is spread among classes
- too much coupling between classes and too little cohesion within classes

### Change Preventers: Divergent Change
- resembles shotgun surgery but is actually the opposite smell
	- **divergent change**: when many changes are made to a single class
	- **shotgun surgery**: when a single change is made to multiple classes simultaneously
- possible reasons -> due to poor program structure or "copypasta" programming

### Dispensables: Duplicated Code
- most common
- sections of code repeated all over the place
- sign of amateur work
- when refactoring duplicated code, you must effectively search for all instances of that code

### Dispensables: Lazy Class
- if a class doesn'nt do enough to earn your attention, it should be deleted
- possible reasons:
	- class was designed to be fully functional but after some refactoring it has become ridiculously small
	- it was designed to support future development work that never got done

### Dispensables: Data Class
- a class that contains only field and crude methods for accessing them (getters and setters)
	- these are simply containers for data used by other classes
- these classes do not contain any additional functionality and can't independently operate on their data

### Couplers: Feature Envy
- a method that seems more interested in a class other than the one it is in
- most common focus of the envy is the data
- possible heuristic -> determine which class has most of the data and put the method with that data

### Couplers: Inappropriate Intimacy
- classes spend too much delving in each other's private parts
- inheritance often leads to overintimacy
	- subclasses are always going to know more about their parents than their parents would like them to know

### Couplers: Middle Man
- if a class performs only one action, delegating work to another class, why does it exist at all?
- possible reasons -> can be the result of the useful work of a class being gradually moved to other classes; the class remains as an empty shell that doesn't do anything other than delegate

# Object-Oriented Design (OOD)
- OOD is sometimes taught as:
	- after identifying your requirements and creating a domain model, add methods to the appropriate classes, and define the messaging between the objects to fulfill the requirements
- such vague advice doesn't help because:
	- deciding what methods belong where and how objects should interact carries consequences
	- a large set of design principles and patterns will help to improve your design skills

# Responsibility-Driven Design (RDD)
- we think of software objects as having responsibilities (an abstraction of what they do)
- Rebecca Wirfs-Brock: a responsibility is an obligation to perform a task or know information
- clear distinction between behavior (doing) and data (knowing)
- a responsibility is not the same thing as a method
	- methods fulfill responsibilities
- RDD includes the idea of collaboration
	- responsibilities are implemented by means of methods that either act alone or collaborate with other methods and objects
- RDD is a general metaphor for thinking about OOD

## Doing And Knowing Responsibilities Example
```
public class Customer<Guid>
	extends Entity // knowing
	implements IAggregateRoot // knowing
{
	private List<Order> _orders; // knowing
	public String email; // knowing
	public String name; // knowing
	
	// doing something itself
	public void addOrder(Order order) throws BusinessRuleValidationException {
		//doing - initiated and coordinate actions with other objects
		this.addDomainEvent(new OrderAddedEvent(order));
	}
}
```