# Inception
- questions to ask
	- what is the vision and business case for the project?
	- is it feasible?
	- buy or build?
	- what is the cost estimate?
	- should we proceed or stop?
- the intent is to establish an initial common vision for the objectives of the project, determine if it is feasible and decide if it is worth some serious investigation in the elaboration phase

## Artifacts That May Start In Inception
- vision and business case (describes high-level goals and constraints)
- use case model (describes functional requirements and related non-functional requirements)
- supplementary specification (describes other requirements)
- glossary(key-domain terminology)
- risk list and risk management plan (describes business, technical, resource, and schedule risks and ideas for their mitigation or response)
- prototype/proof-of-concept
- iteration plan (describes what to do in the first elaboration iteration)
- phase plan & software development plan (guess for elaboration phase duration; tools, people, education, and other resources)
- development case (description of the customized UP steps and artifacts for this project)
- artifacts will be partially completed in this phase and refined in later iterations

## What Happened In Inception?
- a short (~1 week) requirements workshop
- most actors, goals, and use cases named
- most use cases are written in brief format (10-20% of the use cases are written in full detail to improve understanding of the scope and complexity)
- most influential and risky quality requirements identified
- proof-of-concept prototypes were developed
- plan for the first iteration

# Elaboration
- during elaboration
	- core and risky software is programmed and tested
	- majority of requirements are discovered and stabilized
	- major risks are mitigated or resolved
- best practices
	- do short timeboxed risk-driven iterations
	- start programming early
	- adaptively design, implement, and test the core and risky parts of the architecture
	- test early, often, and realistically
	- adapt based on feedback from tests, users, and developers
	- write most of the use cases and other requirements in detail

# Construction And Transition Phases
- elaboration phase -> understand most requirements
	- builds risky and architecturally significant core of the system
- construction -> build the remaining requirements
	- conduct alpha testing (developer side testing)
	- ends when system is ready for operational deployment
- transition phase -> putting system into production use
	- conduct beta testing (client-side testing)

# Iterations
## Iteration 1 Requirements
- emphasis on fundamental issues, requirements analysis, and OOA/OOD
- implement a basic key scenario of the use case (only short and simple use cases are completed in iteration 1)
	- ex. for a Process Sale use case, implement entering items and receiving payment
- no collaboration with external devices
	- ex for a Process Sale use case, no using a tax calculator or product database
- subsequent iterations will grow on this foundation

## Iteration 1 Result
- all software is rigorously tested
- customers feedback is obtained
- the system has been integrated and stabilized

## Iteration 2 Requirements
- emphasis on object design
- support for variations in third-party external services
	- ex. for the Process Sale, include complex pricing rules or design a GUI

## Iteration 3 Requirements
- emphasis on a variety of analysis and design

# Additional Unified Process Best Practices And Concepts
- central idea of UP -> short timeboxed iterative, adaptive development
- tackle high-risk and high-value issues in early iterations
- continuously engage users (at every iteration)
- early iterations focus on core architecture
- continuously verify quality
- carefully manage requirements

# Problems With The Waterfall Lifecycle
- tackles high-risk or difficult problems late
- assumes requirements are fully specified and doesn't change
- design of the system is inflexible
- dictates that architecture is fully specified once requirements are completed