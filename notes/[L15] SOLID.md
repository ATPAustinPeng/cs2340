# SOLID
- 5 principles about class design
	- S -> Single Responsibility Principle (SRP)
	- O -> Open/Closed Principle (OCP)
	- L -> Liskov Substitution Principle (LSP)
	- I -> Interface Segregation Principle (ISP)
	- D -> Dependency Inversion Principle (DIP)
- 6 principles about packages (talked about in [L15] Advanced SOLID)
	- package cohesion: REP, CCP, CRP
	- package coupling: ADP, SDP, SAP

## Purpose Of SOLID
- make code more maintainable
- makes easier to extend the system with new functionality without breaking the existing one
- makes code easier to read and understand so less time spent on what it does and more time to develop
- introduced by Robert Martin (Uncle Bob), named by Michael Feathers

## Single Responsibility Principle (SRP)
- each class has a single responsibility
- each class has one reason why it should change
- use precise names for small classes and generic names for large classes

### Bad
```
public class EmployeeStore implements IEmployeeStore {
	@Override
	public Employee getEmployeeById(long id) {
		return null;
	}
	
	@Override
	public void addEmployee(Employee employee) {
	}
	
	@Override
	public void sendEmail(Employee employee, String content) {
	}
}
```

### Good
```
public interface IEmployeeStore {
	public Employee getEmployeeById(long id);
	
	public void addEmployee(Employee employee);
}

public class EmployeeStore implements IEmployeeStore {
	// inject in runntime
	private IEmailSender emailSender;
	
	@Override
	public Employee getEmployeeById(long id) {
		return null;
	}
	
	@Override
	public void addEmployee(Employee employee) {
	}
}

public interface IEmailSender {
	public void sendEmail(Employee employee, IEmailContent content);
}

public class EmailSender implements IEmailSender {
	@Override
	publicvoid sendEmail(Employee employee, IEmailContent content) {
		// logic
	}
}

public interface IEmailContent {
}

public class EmailContent implements IEmailContent {
	private String type;
	private String content;
}
```

### Benefits
- easy to understand and maintain
	- interface with less methods
	- changes related to the class's responsibility are isolated
- improved usability
	- can be used in other parts without exposing unrelated functionality

## Open/Closed Principle (OCP)
- objects are open to extension but closed to modification
- extension via polymorphism, inheritance
- extend functionality by adding code instead of changing the existing one
- separate behaviors so that system can be easily extended and not broken
- the goal is to get to a point where you can never break the core of the system

### Bad
```
public interface IOperation {
}

public class Addition implements IOperation {
	private double firstOperand;
	private double secondOperand
	private double result = 0.0;
	
	public Addition(double firstOperand, double secondOperand) {
		this.firstOperand = firstOperand;
		this.secondOperand = secondOperand;
	}
	
	public interface ICalculator {
		void calculate(IOperation opreation);
	}
	
	public class SimpleCalculator implements ICalculator {
		@Override
		public void calculate(IOperation operation) {
			if (operation == null) {
				throw new InvalidParameterException("some message");
			}
			if (operation instanceof Addition) {
				Addition obj = (Addition) operation;
				obj.setResult(obj.getFirstOperand() + obj.getSecondOperand());
			} else if (operation instanceof Subtraction) {
				Addition obj = (Addition) operation;
				obj.setResult(obj.getFirstOperand() - obj.getSecondOperand());
			}
		}
	}
}
```

### Good
```
public interface IOperation {
	void perform operation();
}

public class Addition implements IOperation {
	private double firstOperand;
	private double secondOperand;
	private double result = 0.0;
	
	public Addition(double firstOperand, double secondOperand) {
		this.firstOperand = firstOperand;
		this.secondOperand = secondOperand;
	}
	
	// setters and getters
	
	@Override
	public void performOperation() {
		result = firstOperand + secondOperand
	}
}

public interface ICalculator {
	void calculate(IOperation operation);
}

public class SimpleCalculator implements ICalculator {
	@Override
	public void calculate(IOperation operation) {
		if (operation == null) {
			throw new InvalidParameterException("some message");
		}
		
		operation.performOperation();
	}
}
```
- OCP discussion
	- a guideline for how to develop code that allows change over time
	- if you follow agile practices, with each sprint new requirements are inevitable and should be embraced
	- by ensuring OCP, you disallow future changes to existing classes which forces creation of new classes that plug into extension points

## Liskov Substitution Principle (LSP)
- Let <img src="https://render.githubusercontent.com/render/math?math=\phi(x)"> be a property provable about objects x of type T. Then <img src="https://render.githubusercontent.com/render/math?math=\phi(y)"> should be true for objects y of type S, where S is a subtype of T. (created by Barbara Liskov)
- subclasses should be substitutable for their base classes
- any derived class should be able to substitute its parent class without the consumer knowing
- every class that implements an interface must be able to substitute any reference throughout the code that implements that interface
- every part of the code should get the expected result no matter what instance of a class you send it to, given it implements the same interface

### Bad
```
public class RubberDuck extends Duck {
	public String quack() throws Exception {
		var person = new Person();
		
		if (person.squeezeDuck(this)) {
			return "The duck is quacking";
		} else {
			throw new Exception("A rubber duck can't quack on its own");
		}
	}
	
	public String fly() throws Exception {
		throw new Exception("A rubber duck can't fly");
	}
	
	public String swim() throws Exception {
		var person = new Person();
		
		if (person.throwDuckInnTub(this)) {
			return "This duck is swimming";
		} else {
			throw new Exception("A rubber duck can't swim on its own");
		}
	}
}	
```

### Better, But Still Bad
```
public interface QuackableInterface {
	public String quack();
}

public interface SwimmableInterface {
	public String swim();
}

public interface FlyableInterface {
	public String fly();
}

publi class RubberDuck implements QuackableInterface, SwimmableInterface {
	public String quack() throws Exception {
		var perosn = new Person();
		
		if (person.squeezeDuck(this)) {
			return "The duck is quacking";
		} else {
			throw new Exception("A rubber duck can't quack on it's own");
		}
	}
	
	public String swim() throws Exception {
		var person = new Person();
		
		if (person.throwDuckInTub(this)) {
			return "The duck is swimming";
		} else {
			throw new Exception("A rubber duck can't swim on its own");
		}
	}
}


```

- the example above still violates LSP because quack and swim do not work in certain conditions
	- the abstraction is wrong
	- a good subclass would be the following

```
public class FemaleDuck extends Duck {
	private FemaleDuckButt _butt
	
	public FemaleDuck() {
		// initialization of female stuff
		this._butt = new FemaleDuckButt();
	}
	
	public Egg layAnEgg() {
		Egg egg = this._butt.layAnEgg();
		return egg;
	}
}
```

## Interface Segregation Principle (ISP)
- don't make large multipurpose interfaces
- make several small focused ones
- don't make clients depend on interface they don't use
- classes should depend on each other through the smallest possible interface

### Bad
```
public interface Athlete {
	void compete();
	void swim();
	void highJump();
	void longJump();
}

public class JohnDoe implements SwimmingAthlete {
	@Override
	public void compete() {
		System.out.println("John Doe started competing");
	}
	
	@Override
	public void swim() {
		System.out.println("John Doe started swimmingn");
	}
	
	@Override
	public void highJump() {
	}
	
	@Override
	public void longJump() {
	}
}
```

### Good
```
public interface Athlete {
	void compete();
}

public interface SwimmingAthlete extends Athlete {
	void swim();
}

public interface JumpingAthlete extends Athlete {
	void jump();
}

public class JohnDoe implements SwimmingAthlete {
	@Override
	public void compete() {
		System.out.println("John Doe started competing");
	}
	
	@Override
	public void swim() {
		System.out.println("John Doe started swimmingn");
	}
}
```

## Dependency Inversion Principle/Dependency Injection (DIP)
- high level modules should not depend on low level modules
- both high and low level modules should depend on abstractions
- abstractions should not depend on details but rather details should depend on abstractions

### Bad
```
public class BackEndDeveloper {
	public void writeJava() {
	}
}

public class FrontEndDeveloper {
	public void writeJavascript() {
	}
}

public class Project {
	private BackEndDeveloper backEndDeveloper = new BackEndDeveloper();
	private FrontEndDeveloper frontEndDeveloper = new FrontEndDeveloper();
	
	public void implement() {
		backEndDeveloper.writeJava();
		frontEndDeveloper.writeJavascript();
	}
}
```

### Good
```
public interface IDeveloper {
	void develop();
}

public class BackEndDeveloper implements IDeveloper {
	@Override
	public void develop() {
		writeJava();
	}
	
	private void writeJava() {
		System.out.println("We're writing Java!");
	}
}

public class FrontEndDeveloper implements IDeveloper {
	public void develop() {
		writeJavascript();
	}

	private void writeJavascript() {
		System.out.println("We're writing Javascript!");
	}
}
```

# Conclusions
- don't get trapped by SOLID
	- SOLID design principles are not laws
	- use common sense
	- don't over fragment code for SRP or SOLID
	- don't try to achieve SOLID, use SOLID to achieve maintainability