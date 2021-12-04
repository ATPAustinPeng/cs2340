# General Responsibility Assignment Software Patterns (GRASP)
- 5 "basic"
	- creator
	- information expert
	- loww coupling
	- controller
	- high cohesion
- 4 "advanced" (talked about in [L14] Advanced GRASP)
	- polymorphism
	- pure fabrication
	- indirection
	- protected variations

## Creator
- assign class B to create class A if
	- B contains A
	- B records A
	- B closely uses A
	- B has initializing data for A so it is an expert in creating A
	- if more than one applies, prefer aggregation
- benefits -> low coupling
- guidelines
	- composite object is a great choice to create its parts
	- look at the class with the initializing data
		- ex. a Payment instance must be initialized with the Sale total; so Sale is a candidate creator of Payment
	- in case of complex rules, consider delegation of creation to a helper class

## Information Expert
- assign responsibility to a class that has the information necessary to carry that responsibility out
- real-world analogy: responsibility is given to individuals that have the information necessary to fulfill a task
- benefit -> low coupling, high cohesion

## Low Coupling (High To Low)
- content -> one class modifies another (bad)
- common -> share global data (somewhat bad)
- control -> use a return code to control a different method (somewhat bad)
- stamp/data -> passing complex data between modules
	- use primitives when possible
	- may lead to data coupling if parameters exceed 3
- uncoupled -> no relationship
- examples:
	- X has an attribute that refers to Y
	- X calls on services of Y
	- X has a method that refers to Y
	- X is a subclass of Y
	- Y is an interface that X implements
- benefits -> not affected by changes in other classes, simple to understand, convenient to reuse
- Note: high coupling to stable elements is usually not a problem

## Controller
- represents the overall system
- not the UI
- delegates work to other objects
- facade controllers when you have few system events vs. use case controllers
- benefits -> potential for reuse and pluggable interfaces, opportunity to reason about the state of the use case
- responsibilities:
	- delegates work to other objects
	- coordinates activity
	- does not do a lot of work itself

## High Cohesion
- single class
- methods/responsibilities should be highly related
- low to high
	- coincidental -> unrelated (bad)
	- logical -> multiple logic sections
	- temporal -> related by phases of an operation
	- procedural -> required ordered of a task
	- communicational -> operates on the same dataset
	- functional -> all essential elements for a single function are in the same module
- coincidental cohesion
```
interface MyFuns {
	void initPrinter();
	double calcInterest();
	Date getDate();
}
```
- logical cohesion
```
interface AreaFuns {
	double circleArea();
	double rectangleArea();
	double triangleArea();
}
```
- temporal cohesion
```
interfae InitFuns() {
 void inintDisk();
 void initPrinter();
 void initMonitor();
}
```
- procedural cohesion
```
interface BakeCake {
	void addIngredients();
	void mix();
	void bake();
}
```
- functional cohesion
```
interface Plane {
	void takeoff();
	void fly();
	void land();
}
```

## Good
- low coupling
- high cohesion
- low representation gap
- separation of concerns

## Bad
- high coupling
- low cohesion
- needless complexity (YAGNI)
- needless repetition (DRY)
- **opacity (obscure, obtuse)**: code should be straightforward to understand
- **rigidity**: resistance to change; hard to predict how long it will take to make a change
- **fragility**: a change in one module breaks other modules
- **immobility**: same code doesn'nt work when moved to another project
- **hackability (viscosity)**: invites or accommodates workarounds more or less than fixes

# 3 Types Of Developers
- novice
	- brittle designs
	- easy to code
	- hard to maintain
- intermediate
	- overly fancy, flexible, generalized (and normally unused) designs
	- easy to maintain
	- hard to code
- expert
	- designs chosen with insight, balancing brittle with generalized
	- easy to maintain
	- hard only when required