# De-Slop Skill

I want you to De-Slop the codebase. The idea it to have files that is no more than 1K lines of code. I want to separate the code into the components (reuseable if it can be used to remove duplicate or very similar code elsewhere in the code). A codebase study must be done, thinking in possibilities to split the logic into single responsibility components. 

## Solid Principles

The SOLID principles are five object-oriented design principles that help create software that is easier to understand, maintain, test, and extend.

| Principle | Name                            | Core Idea                                                        |
| --------- | ------------------------------- | ---------------------------------------------------------------- |
| **S**     | Single Responsibility Principle | One component, one responsibility.                               |
| **O**     | Open/Closed Principle           | Extend behavior without modifying existing code.                 |
| **L**     | Liskov Substitution Principle   | Subtypes must be interchangeable with their base types.          |
| **I**     | Interface Segregation Principle | Prefer many small, specific interfaces over one large interface. |
| **D**     | Dependency Inversion Principle  | Depend on abstractions rather than concrete implementations.     |

S — Single Responsibility Principle (SRP)
Description: A class or module should have only one reason to change, meaning it should have a single, well-defined responsibility.
Goal: Improve maintainability by keeping each component focused on one task.

O — Open/Closed Principle (OCP)
Description: Software entities should be open for extension but closed for modification. New behavior should be added without changing existing, tested code.
Goal: Reduce the risk of introducing bugs when adding new features.

L — Liskov Substitution Principle (LSP)
Description: Objects of a derived type should be replaceable with objects of their base type without altering the correctness of the program.
Goal: Ensure inheritance preserves expected behavior and contracts.

I — Interface Segregation Principle (ISP)
Description: Clients should not be forced to depend on interfaces they do not use. Prefer several small, focused interfaces over one large, general-purpose interface.
Goal: Reduce unnecessary dependencies and improve flexibility.

D — Dependency Inversion Principle (DIP)
Description: High-level modules should not depend on low-level modules. Both should depend on abstractions, and abstractions should not depend on details.
Goal: Decouple components, making systems easier to test, extend, and maintain.

## Design Patterns

Below are 15 of the most commonly used software design patterns, grouped by their category as defined in the Gang of Four (GoF) design patterns.

| Pattern              | Category   | Brief Description                                                                                                                      |
| -------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Singleton**        | Creational | Ensures a class has only one instance and provides a global access point to it.                                                        |
| **Factory Method**   | Creational | Defines an interface for creating objects while allowing subclasses or implementations to decide which concrete object to instantiate. |
| **Abstract Factory** | Creational | Creates families of related or dependent objects without specifying their concrete classes.                                            |
| **Builder**          | Creational | Constructs complex objects step by step, allowing different representations of the same construction process.                          |
| **Prototype**        | Creational | Creates new objects by cloning existing ones instead of instantiating them from scratch.                                               |
| **Adapter**          | Structural | Allows incompatible interfaces to work together by translating one interface into another.                                             |
| **Decorator**        | Structural | Dynamically adds new behavior or responsibilities to an object without modifying its code.                                             |
| **Facade**           | Structural | Provides a simplified interface to a complex subsystem, making it easier to use.                                                       |
| **Composite**        | Structural | Treats individual objects and groups of objects uniformly using a tree-like structure.                                                 |
| **Proxy**            | Structural | Acts as a placeholder or surrogate for another object to control access, add caching, security, or lazy loading.                       |
| **Observer**         | Behavioral | Defines a one-to-many dependency so that when one object changes state, all its dependents are notified automatically.                 |
| **Strategy**         | Behavioral | Encapsulates interchangeable algorithms or behaviors, allowing them to be selected at runtime.                                         |
| **Command**          | Behavioral | Encapsulates a request as an object, enabling queuing, logging, and undo/redo functionality.                                           |
| **State**            | Behavioral | Allows an object to change its behavior when its internal state changes, as if it changed its class.                                   |
| **Template Method**  | Behavioral | Defines the skeleton of an algorithm while allowing subclasses to customize specific steps without changing the overall structure.     |

## Guidelines

- First pass on the codebase will identify sections/groupd by functionality. 
- Create a grouped list of methods for each file observed.
- Create a second list to identify the components required to split all methods.
- Create a third list to group the components by their functionalities.
- Beware of circular imports. A good way to avoid that is to use event driven architecture.
- Prefer raising exceptions rather then adding fallbacks. If the fallback is REALLY necessary; ask the user how to proceed.
- Never add 'backward-compatibility' or 'legacy-code' workarounds. If that is REALLY necessary; ask the user how to proceed.

## Grouping Directives 

Example 1:

Given the following functions:

- render_aliases_table
- render_settings_table
- render_configs_table
- render_properties_table
- run_aliases_proc
- run_settings_proc
- run_configs_proc
- run_aproperties_proc
- display_aliases_results
- display_settings_results
- display_configs_results
- display_properties_results

There are two possibilities here:

1. We can group by functionality

A. Renders:
  |- render_aliases_table
  |- render_settings_table
  |- render_configs_table
  |- render_properties_table

B. Runners:
  |- run_aliases_proc
  |- run_settings_proc
  |- run_configs_proc
  |- run_properties_proc

C. Displays:
  |- display_aliases_results
  |- display_settings_results
  |- display_configs_results
  |- display_properties_results

**This grouping is not very good, because its a very attached grouping, and this will hurt the 'Open' principle because if we need to ahnance anything we will have to edit verious files.**

2. Grouping by atomic features

A. Aliases:
  |- render_aliases_table
  |- run_aliases_proc
  |- display_aliases_results

B. Settings:
  |- render_settings_table
  |- run_settings_proc
  |- display_settings_results

C. Configs:
  |- render_configs_table
  |- run_configs_proc
  |- display_configs_results

D. Properties:
  |- render_properties_table
  |- run_properties_proc
  |- display_properties_results

**This is a much better approach , because we have atomically grouped the functionalities. This makes easier to extend to a new 'Procedures' ferature for example, because we would need only to create the new file containing what we want. And even better if we extracted a common interface/protocol to [render,run,display,...].**

## New Code

- Observer the above rules when adding new code to the repo. 
- Follow the same code style as the existing code. 
- If you find a checkstyle file, use it as the source of truth.
- Use SOLID and Design patterns - Preferrebly.

## Troubleshooting

- When troubleshooting code, make sure you narrow the possible causes until you are [95%-100%] certain of that issue.
- If you have already tried one approach, open for new possibilities or hidden causes.
- When very unsure of the cause, use git to track changes.

## Testing

- Avoid testing hardcoded strings.
- Ensure it does not contain unusefull string assertions like: "assert tab_name is 'anything'".
- Reinforce testing logic and features.
- Reinforce testing integration.