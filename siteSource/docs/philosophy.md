# Principles and Project Philosophy

Any open project inevitably reflects the personality of its author.  
These principles represent my personal guidelines, an expression of my values and preferences.  
This is the way I find the work most engaging.

## System Philosophy

### The System Focuses Exclusively on Agent (NPC) Behavior

The system is designed solely for describing NPC behavior. It does not provide access to game scene objects, particle systems, animations, sounds, or similar components. In cases where the system might be applied in other domains—for example, in robot control—it will likewise not provide access to low-level hardware management.

This design approach enables:

* Abstraction from other game components and even from the execution environment  
* Cleaner and more maintainable code  
* The possibility of applying the system beyond the game industry—in simulations, robotics control, expert systems, knowledge bases, and ontologies  

Since my current primary focus is the use of the system in game development, I will henceforth use the term NPC (Non-Player Character) to denote an agent.

### Declarativity, Expressiveness, and Readability

The developer should focus on the required behavioral logic rather than struggle with language or framework constructs.

Code must be easily readable, understandable, and aesthetically clean. The developer should be able to grasp, at first glance, what the code describes and what it performs.

The number of places requiring modifications should be minimized—ideally limited to a single location.

In the design of the system, priority is given to declarative means.

### Simplicity as Clarity and Expressiveness Through Understanding

In this system, simplicity is understood as a pursuit of clarity, expressiveness, and semantic transparency. It is a simplicity that arises from understanding rather than from the rejection of complexity.

My ideal is the simplicity found in Haskell: where expressive constructs allow complex behavior to be described concisely and intelligibly.

The system does not aim for artificial simplicity that restricts expressiveness. If, in the course of development, the system results in a very high entry threshold or even appears esoteric—so be it.

At the same time, it avoids excessive complexity that hinders comprehension. If, in the course of development, the system results in a very low entry threshold and appears overly primitive—so be it.

The essential requirement is that simplicity serves meaning, not form.

### Usability Takes Priority Over Dogmatic Adherence to a Specific Programming Paradigm

The system is not rigidly bound to a single programming paradigm. Any paradigm is acceptable if its use enhances declarativity, expressiveness, and readability, and makes the specification of NPC behavior more convenient.

It is not advisable to implement logical programming exclusively through imperative or functional programming constructs merely to remain within the boundaries of the corresponding paradigm. Such an approach results, at minimum, in a loss of expressiveness and makes it difficult to discern the required logic amid large amounts of auxiliary code.

Similarly, I do not consider it necessary to repeat the attempt made in Visual Prolog to express imperative code solely through logical programming constructs, simply to remain within Prolog.

A paradigm is merely a means to achieve results, not an end in itself.

### Implicitness Is Acceptable for Convenience and Expressiveness, but Control Must Also Be Possible

Implicitness helps avoid excessive amounts of code by removing the need to declare everything explicitly. This is a deliberate compromise: a trade-off of strictness and formal safety in favor of convenience and expressiveness.

Convenience requires reducing unnecessary code. Expressiveness requires freedom from technical noise.

At the same time, there must be optional mechanisms for controlling and overriding the system’s default behavior. The developer should have the ability to understand, refine, and modify implicit decisions.

The key is to maintain balance.

### Reducing Boilerplate Code Is Important, but Should Not Become Fanatical

Declarativity, expressiveness, readability, usability, and simplicity all imply minimizing template-like, repetitive code.

In this sense, the purpose of my system is precisely to reduce boilerplate code — for example, by allowing an entity to be declared without the need to register it in multiple places.

At the same time, eliminating every single "extra character" is not a priority, especially if declarativity, expressiveness, readability, usability, and simplicity are degraded as a result of such removal.  

Reducing unnecessary characters is a means, not an end. If a bracket helps clarify structure, it should remain.

### Determinism Is Important, but Non-Determinism Should Also Be Convenient When Needed

In human behavior, determinism manifests itself in logic, instructions, habits, rituals, and adherence to rules. This is a significant aspect, particularly when behavior must be explainable and reproducible.

Within the system, priority is given to determinism — so that behavior remains predictable, debuggable, and reproducible.

At the same time, mechanisms for enabling non-deterministic behavior are also necessary where appropriate. Randomness, variability, and improvisation are likewise part of realistic behavior, and they should be available without sacrificing transparency or controllability.

## Language Design

### Multiparadigm Approach

The language supports multiple paradigms simultaneously — object-oriented, functional, logical, and imperative.  
This enables developers to combine programming styles and leverage the strengths of each approach depending on the context.

### Domain Orientation

The primary objective is to facilitate the modeling of character behavior.  
To achieve this, the developer must directly operate with domain-specific concepts.

### Declarativity Without Compromising Applicable Paradigms

Declarative constructs allow the expression of intentions rather than step-by-step instructions.  
At the same time, the language does not restrict developers from using imperative or functional mechanisms, maintaining a balance between declarativity and practical applicability.

### Modularity and Incremental Development

The module system ensures separation of concerns and code reuse.  
Projects can be developed incrementally by adding new components without the need to rewrite existing ones.  
This makes the language suitable for long-term and evolving systems.

### Dynamic Typing with Optional Strict Typing

By default, the language is dynamically typed, which accelerates prototyping.  
For critical parts of the system, strict typing can be enabled to provide additional control and safety.  
This approach combines flexibility with reliability.

## Architectural Design

### Isolation of NPCs: From Each Other and from the Game Scene

Each agent (NPC) in the system is isolated—it has no direct access to the game scene or to the data of other NPCs.  
NPC behavior is formed on the basis of its own knowledge and the data obtained through perception channels.

### Modularity and Incremental Construction of Agent (NPC) Behavior

The behavior of agents (NPCs) can be described in parts, with the ability to gradually extend, override, and refine it. The system supports a modular structure in which each behavior block can be added, disabled, or adjusted without the need to rewrite the entire behavior.

Advantages of modularity:

* **Incrementality**: development can begin with simple behavior and gradually add new reactions, refinements, and scenario-specific exceptions.  
* **Reusability**: behavioral blocks can be structured as modules and reused across different contexts.  
* **Overriding**: more specific modules can override or refine behavior defined at a more general level.  
* **Isolation**: modules are not required to be aware of each other—they can be combined by the system based on priorities, context, or scenario.  

A module may be represented as a book, scroll, or artifact that grants an NPC new knowledge or abilities. This is particularly relevant in an architecture where NPCs are isolated and do not have global access to behavior definitions.

For example, a game scenario might proceed as follows:

1. The NPC finds, purchases, or receives a book from a teacher.  
2. The game triggers a reading scene or a knowledge-acquisition animation.  
3. At that moment, the engine attaches the corresponding module to the NPC.  
4. The NPC acquires new knowledge or a behavioral capability.  

This approach makes the architecture not only technically flexible but also narratively expressive—behavior becomes part of the world rather than merely code.

### Full Control over Execution

The system provides the ability to stop execution at any moment and save it as an image. After loading from the image, execution can be resumed exactly from the point at which it was interrupted.

In practice, this means:

* **Stop and Save**: execution can be interrupted at any point, preserving all data about the agent’s state, its modules, and its context.  
* **Resume**: after loading from the image, execution continues without loss of information—the NPC behaves as if no pause occurred.  
* **Deterministic Restoration**: it is guaranteed that the restored behavior is identical to the original, with no hidden discrepancies.  
* **Instrumentality**: developers or researchers can use save/resume functionality for debugging, experimentation, or scenario control.

### The Engine’s Application Should Not Be Limited to Games

The engine is designed as a universal platform for describing and executing agent behavior. Its application is not restricted to the game industry—the architecture is intended to support use in other domains where knowledge, logic, and control are essential.

Possible additional application areas:

* Knowledge base  
* CLI in the style of an interactive Prolog interpreter  
* AI for robot control (with server-side execution)

### All Execution Must Occur Locally on the User’s Computer Without Requiring Internet Connectivity

The engine must operate entirely locally on the user’s computer. All functions are executed without the need for an internet connection. This ensures autonomy, reliability, and control over the process.

In practice, this means:

* **Autonomy**: the system does not depend on external services or servers.  
* **Reliability**: operation continues even in the absence of a network or with limited access.  
* **Transparency**: the user knows that all computations occur on their device.  
* **Security**: NPC data and game states never leave the local machine.  
* **Predictability**: no external factors can alter the behavior of the engine.

### The Use of Third-Party Components Requiring or Potentially Requiring License Purchases Is Not Permissible

The engine must not include third-party components that require or may require the purchase of licenses. All elements of the system must be free from hidden restrictions, paid dependencies, and mandatory subscriptions.
