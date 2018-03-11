# SOLID

## SOLID Principles

Single Responsibility Principle — Classes should have only one reason to change

Open Closed Principle — Open for extension, closed for modification

Liskov's Substitution Principle — Base types should be replaceable by subtypes

Interface Segregation — Better to have many smaller interfaces than a big one

Dependency Inversion — Depend upon abstractions not concretions


### Single Responsibility Principle

- only one reason to change
- small class
- separation of concerns
- do one thing, and do it well
- high cohesion, low coupling

e.g. It is not the responsibility of User to know how a booking is made. User should not change when booking logic changes.


### Open, Closed

- open for extension, closed for modification
- existing code shouldn't be modified when adding new features
- abstractions, interfaces

e.g. Don't add another `elif` clause that checks a type, instead add another class that does exactly what you need.


### Liskov's Substitution
Objects of type may be replaced with objects of a subtype without altering the correctness of the program.


### Interface Segregation

Better to have many smaller interfaces than a big one.
Don't force classes to implement methods that don't concern them.

e.g. You don't need card details when making a cash payment.


### Dependency Inversion

Depend on an interface not on a concrete class.

e.g. The base class should depend on a interface (have a interface as a member instead of a concrete class). The consuming class should receive the correct object that implements the interface. Don't do type checking.


SOLID principles [part 1][solid-1], [part 2][solid-2] on YouTube.

[solid-1]: https://www.youtube.com/watch?v=hCsqBIyT1pI
[solid-2]: https://www.youtube.com/watch?v=hCMAcnm4z3I



## Encapsulation and SOLID - Pluralsight

Command-query separation

  - queries return data
    - do not mutate state
    - idempotent
    - safe to invoke
  - commands have side effects
    - ok to invoke queries from commands


Postel's law (Robustness principle)

- Be conservative in what you send (guarantees about output, contract)
- Be liberal in what you accept (tolerant of inputs)
    - Fail fast


Abstraction is the process of hiding complexity: separate what you want from how you do it.  
e.g. function call vs function body; the function hides the complexity of how the task is performed.


Encapsulation  
Hide the representation of data, and provide functions for setting, retrieving and manipulating data.

1. Hide the details of how information is stored.
   Separate what you are storing from how it is stored
2. Do something extra when a value is set e.g. update a counter, save in database, error-checking.
