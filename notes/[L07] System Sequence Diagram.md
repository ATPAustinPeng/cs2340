# System Behavior And System Sequence Diagram (SSD)
- **sequence diagram**: a picture that shows (for a particular scenario of a use case), the events that external actors generate, their order, and possible inter-system events
- all systems are treated as a black box
- the diagram places emphasis on events that cross the system boundary from actors to systems

## SSD Example
- simple cash-only process sale scenario
	- `Customer` arrives at POS checkout with goods to purchase
	- `Cashier` starts a new sale
	- `Cashier` enters item identifier
	- `System` records sale line item and presents item description, price, and running total
		- `Cashier` repeats this step until done
	- `System` presents total with taxes calculated

<img src="img/l07-ssd-ex.png" alt="ssd-ex" width="500">

## Naming System Events And Operations
- the set of all required system operations is determined by identifying the system events
	- ex. `makeNewSale()`, `addLineItem(itemID, quantity)`, `endSale()`

## System Sequence Diagrams: Fragments
- manage complex interactions with sequence fragments
	- loop -> iteration
	- alt -> alterations
	- opt -> option
	- ref -> reference

### Loop
<img src="img/l07-ssd-fragment-loop.png" alt="ssd-fragment-loop" width="200">

- calls notify() 10 times

### Alternatives
<img src="img/l07-ssd-fragment-alternative.png" alt="ssd-fragment-alternative" width="200">

- calls accept() if balance > 0
- calls reject() otherwise

### Option
<img src="img/l07-ssd-fragment-option.png" alt="ssd-fragment-option" width="200">

- post comments if there were no errors

### Reference
<img src="img/l07-ssd-fragment-reference.png" alt="ssd-fragment-reference" width="200">

- Web customer and Bookshop use (reference) interaction Checkout

## SSDs Within The Unified Process
- SSDs are not usually motivated in inception
- most SSDs are created during elaboration