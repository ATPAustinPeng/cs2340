# Object-Oriented Design
- emphasizes a conceptual solution that fulfills the requirements
- need to define software objects and how they collaborate to fulfill the requirements
	- ex. in the Library Information System, a *Book* software object may have a *title* attribute and a *getChapter* method
- designs are implemented in a programming language
	- ex. we will have a *Book* class in Java.

## From Design To Implementation
<img src="img/l11-design-to-implementation.png" alt="design-to-implementation" width="450">

# Design Class Diagrams (DCD)
<img src="img/l11-design-class-diagram.png" alt="design-class-diagram" width="450">

- Note: DCD shows software entities while Domain Models show real-world entities (DCD vs Domain Model)

## When To Create DCDs
- once the interaction diagrams have been completed it is possible to identify the specification for the software classes and interfaces
- a class diagram differs from a Domain Model by showing software entities rather than real-world concepts
- the UML has notation to define design details in static structure, or class diagrams.

## Class Attributes
- full format:
	- `visibility name` : `type multiplicity` = default {property-string}
- visibility marks:
	- `+` (public), `-` (private), `#` (protected)
- attributes assumed private if no visibility is given
- operations assumed public if no visibility is given

## Attribute Text vs. Association Line Notation For An Attribute
<img src="img/l11-attribute-text-vs-association-line.png" alt="attribute-text-vs-association-line" width="550">

## Idioms In Association Notation Usage In Different Perspectives
<img src="img/l11-idioms-in-association-notation.png" alt="idioms-in-association-notation" width="450">

## When to Use Attribute Text vs. Association Lines for Attributes
- guideline:
	- use the attribute text notation for data type objects
	- use the association line notation for others
- common data types: 
	- Boolean, Date, Number, Character, String (Text), SSN, ZIP, Phone #, etc.

<img src="img/l11-when-to-use-attribute-text-vs-association-lines1.png" alt="when-to-use-attribute-text-vs-association-lines1" width="500">
<img src="img/l11-when-to-use-attribute-text-vs-association-lines2.png" alt="when-to-use-attribute-text-vs-association-lines2" width="200">

## The UML Notation For An Association End
<img src="img/l11-uml-notation-for-association.png" alt="uml-notation-for-association" width="400">

## Note Symbols
-   a note symbol may represent several things
	-   UML note or comment
	-   UML constraint
	-   method body

<img src="img/l11-note-symbols.png" alt="note-symbols" width="500">

## Operations and Methods
- operation syntax, UML1:
	- visibility name (parameter-list) : return-type {property-string}
- operations are usually assumed public if no visibility is shown
- operations to access attributes are often excluded

## UML Keywords
<img src="img/l11-uml-keywords.png" alt="uml-keywords" width="500">

## Dependency
- you want low-coupling across classes because it allows for easier refactoring when dependencies change (if you touch something in one class, it doesn't greatly affect the other class)

<img src="img/l11-dependency.png" alt="dependency" width="350">

## Optional Dependency Labels
<img src="img/l11-optional-dependency-label.png" alt="optional-dependency-label" width="600">

## Interfaces
<img src="img/l11-interfaces.png" alt="interfaces" width="350">

## Inheritance
<img src="img/l11-inheritance1.png" alt="inheritance1" width="350">
<img src="img/l11-inheritance2.png" alt="inheritance2" width="350">

## Abstract Class
<img src="img/l11-abstract-class.png" alt="abstract-class" width="350">

## Composition Over Abstraction
- **aggregation**: “has-part” association relationship; hollow diamond shape

<img src="img/l11-aggregation.png" alt="aggregation" width="400">

- **composition**: whole-part association relationship; filled diamond shape

<img src="img/l11-composition.png" alt="composition" width="550">

## Constraints
<img src="img/l11-constraints.png" alt="constraints" width="400">

## Utility Class
<img src="img/l11-utility.png" alt="utility" width="200">

- the {leaf} notation means that this class can have no children

## Association Class
- many to many relationship

<img src="img/l11-association-class.png" alt="association-class" width="400">