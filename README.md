# Domain driven design - part 1

## Chapter 1: Crunching knowledge

### Effective Modeling

- Binding model and implementation
- Cultivating a language based on the model
  - Anyone can take and understand the model and being unambiguously understood
  - "Domain sentences" must be consistent with the structure of the model
- Developing a knowledge-rich model
  - The model is not a data-schema
  - Object contains behaviour
- Distilling the model
  - Concepts should be dropped if not useful nor central
  - An unneeded concept tied to an important should lead to a model refactor without the unneeded one
- Brainstorming and experimenting
  - Many models should be produced and tested
  - Eventually, the team will be able to quickly detect the validity / awkwardness of a model

### Crunching Knowledge

#### Problem

Two visions of the software model, one from the domain expert, the other from the developer.

The developer's one is naive and not deeply connected to the domain.
The expert's one is complex and hard to understand by the developers.

The domain and the software are not isomorphic and therefore, solving domain problems
can be hard to do because of the model.
The model is not evolving with the domain and eventually, even though the software is useful,
it won't provide tremendous value and will struggle to solve new problems of the domain.

#### Reasons

In waterfall, analysts are a wall between developers and domain experts.
Knowledge is only going one way and is not shared across the team.
The domain won't be refined because of the lack of feedback 
(no early versions, no knowledge sharing, etc.).  

In iterative cycles, even though feedback and refactoring will definitely help,
if developers are not interested in the domain, powerful features won't arise by themselves
from the domain.
The developers are just asking what do, implementing the feature, presenting it and moving on
to the next one.

### Knowledge-rich Design

Implementation should reflect and express the model.
If the model changes, the implementation should be refactored.

#### Example: Extract a Hidden Concept.

Sometimes, business rules are written in a cryptic `if` statement.

- Domain expert can't verify nor read it because it's too technical
- Developers / analysts will struggle to understand the concept behind the rule.

We can extract the `if` to a dedicated, well-named class responsible for validating the business rule.
Hence the code will be readable by everyone and the domain clearly expressed.

## Chapter 2: Communication and the Use of Language

### Ubiquitous language

#### Different languages

A project faces serious problems when its language is fractured.

Domain experts and developers are using a different language.
Therefore, day-to-day discussions is disconnected from the terminology embedded in the code.
Even developers use different languages, one when talking to the team and an other when writing code.

Translation blunts communication and makes knowledge crunching anemic.
Team members are constantly translating concepts to their own language.
This leads to information loss and unreliable software that doesn't fit together.
Also, the effort required by the translation prevents the interplay of knowledge and ideas
that would have lead to deep model insights.

None of these dialects can be a common language because none serves all needs.

#### Inject the ubiquitous language

Use the model as the backbone of a language.
The team should extensively use the model, whether for speech or writing.

Difficulties in formulating sentencing should lead to new model alternatives,
which will eventually require a class, method or module refactor,
in order to conform with the new model.
A change in the language is a change to the model.

Confusion, awkwardness or inadequate terms to convey domain understanding should
be fixed by domain experts.
Developers on the other hand should watch for ambiguity and inconsistency.

### Modeling out Loud

> Play with the model as you talk about the system.  
> Describe scenarios out loud using the elements and interactions of the model,
> combining concepts in ways allowed by the model.
> Find easier ways to say what you need to say and take those new ideas back down the diagrams and code.

#### Examples

- If we give to **Routing Service** an origin, destination and arrival time, it can look up the stops
the cargo will have to make and stick them in the database. (*vague and technical*)

- The origin, destination and so on.. it all feeds into the **Routing Service** and we get back an **Itinerary** 
that has everything we need in it. (*more complete but verbose*)

- A **Routing Service** finds an **Itinerary** that satisfies a **Route Specification**. (*concise*) 

### One Team, One Language

Technical people often feel the need to *shield* domain experts from the domain model.

- Too abstract for them
- They don't understand objects
- We have to collect requirements in their terminology

*If sophisticated domain experts don't understand the model, there is something wrong with the model.*

When using the same language, developers and domain experts can informally test the model
by walking through scenarios, using the model objects step-by-step.
Almost every discussion is an opportunity for developers and user experts to play with model together,
deepening each other's understanding and refining concepts as they go.

The domain experts can use the language of the model in writing use case,
and can work even moore directly with the model by specifying acceptance tests. (BDD)

Multiplicity of languages is often necessary but the linguistic division should *never* 
be between the domain experts and the developers. 
Technical jargon / advanced business terms are **extensions** of the language and one shouldn't replace the other.

![languages-extensions](https://comment-it.co.uk/wp-content/uploads/2018/01/ubiquitous-language.png)

### Documents and Diagrams

UML diagrams are useful when discussing software design.
However people tend to add too many details in their diagrams, making them
very hard to read and stay focused on the central concept.

When this is the case, UML is used to precisely model the domain, constraining the team to the UML syntax.
Details like constraints, assertions or even comments are added around objects and overwhelm the reader with
unneeded information.

UML is *not* a programming language and should only be used as a mean of communication and explanation, facilitating
brainstorming.
Diagrams should be small, simple and focused, they represent the skeleton of ideas.

**The vital detail about the design is captured in the code**.
Diagrams and documents can guide people and natural language discussion can fill nuances of meaning.
**The model is not a the diagram**, the diagram help in explaining the model. 

### Written Design Documents

#### Documents should complement Code and Speech

XP tends to remove any written documents and mostly rely on code.
Written documents have no impact on behaviour and can easily lie and become outdated.
On the other hand, spoken communication is ephemeral and can't really create confusion.

The limit of this is that code can overwhelm the reader with a lot of details.
Although the behaviour is unambiguous, that doesn't mean that it's obvious.
Then we end up with the same problem as with a detailed UML diagram, it's hard to clearly express / understand the intent.

Extra documents should aim to illuminate meaning and focus attention on core elements.
It clarifies design intents but *shouldn't try to do what the code already does well*.

#### Documents should work for a living and stay current 

Design documents should explain core concepts of the model, help in navigating the detail of the code and give
insight into the model's intended style of use.

The document must be involved in project activities.
That is, the document should be written using the *current* language the team uses (spoken and written languages).
If the terms explained in the document aren't synced, then the document is incorrect.
Maybe it's too big or complicated, or not focused enough.
People are either not reading it or not finding it compelling.
*If it has no impact on the ubiquitous language, then something is wrong*.

An outdated document should either be archived or updated.
But if the document is not playing an important role, effort might be wasted while trying to keep it up to date. 

Thanks to the ubiquitous language, specifications can be more concise and less ambiguous.
Scenarios can directly use the model and clearly express the intent,
without having to convey the business knowledge that lies behind the model.
By keeping minimal documents, they are complementing code and conversation and can easily stay connected to the project.
  
### Executable Bedrock

Relying mostly on the executable code and tests can be risky.
Even though the behaviour is inescapable, the communication is not guaranteed to be accurate.

The main reason for that is naming. Method or variable names can be misleading, ambiguous or outdated.
It requires a lot of disciple to not only write a code that doesn't just **do** the right thing but also
**says** the right thing.

To communicate effectively, the code must be based on the same language used
to write the requirements, that is the same language that the developers speak
with each other and with domain experts.

### Explanatory Models

Models can be valuable as education aids to teach about the domain.
The model that drives the design is only one view of the domain, 
but it may aid learning to have other views, for educational purpose only, 
to communicate general knowledge of the domain.

The models are free to use whatever style they want, like visual metaphor for example.
They don't (and maybe shouldn't) be object models, like strict UML, in order to avoid
a false impression of correspondence with the softwaxre design.

Example: Instead of using a UML object diagram, you could hand-draw the workflow 
and add some comments using natural language.
  
## Chapter 3: Binding Model and Implementation

### Model Driven Design

Projects without any domain model will the domain is very simple, as they will have the advantages of 
knowledge crunching and communication (because the code is the only source of truth).
However, a complex domain will swamp them.

Many complex projects have some domain models, but they become quickly irrelevant and misleading
as they don't maintain a tight connection with the code.
These domain model are often called *analysis* model.

> If the design, or some central part of it, does not map to the domain model,
> that model is of little value, and the correctness of the software is suspsect.
> At the same time, complex mappings between models and design functions are difficult to understand and, 
> in practice, impossible to maintain as the design changes.  
> A deadly divide opens between analysis and design so that insight gained in each of 
> those activities does not feed into the other.

Model Driven Design discards the dichotomy of analysis model and design to search out
a single model that serves both purposes.
The binding between model and design shouldn't come at the cost of weakened design nor analysis.

That means, a model should be discarded if:
- It is not practical for implementation
- It doesn't faithfully express the key concepts of the domain

The modeling and design process then becomes a single iterative loop.
It will require more effort, but eventually, the produces model will be **relevant**.

> Design a portion of the software system to reflect the domain model in a very literal way,
> so that mapping is obvious.  
> Revisit the model and modify it to be implemented more naturally in software, 
> even as you seek to make it reflect deeper insight into the domain.  
> Demand a single model that serves booth purposes well, in addition to
> supporting a robust ubiquitous language.
> 
> Draw from the model the terminology used in the design and the basic assignment of
> responsibilities. 
> The code becomes an expression of the model, so a change to the code may be a change to the model.
> Its effect must ripple through the rest of the project's activities accordingly. 
> To tie the implementation slavishly to a model usually requires software
> development tools and languages that support a modeling paradigm, such as OOP.

### Hands-on Modelers

#### Manufacturing

Manufacturing is a popular metaphor in software development.
- Highly skilled engineers design
- Less skilled laborers assemble the products

Most of the projects tend to over-separate responsibilities, such as design / modeling and programming.
Managers think that modelers (ex: architects) should only to work on the design,
and that programming would be a waste of their skills.
In practice, this leads to the loss of the model in the implementation.

Developers lack support from modelers and the model is only used as a mere data structure.  
Instead of closely work with modelers and define the correct abstractions, the developers
are going to create their own and focus only on trying to make the software work.

Modelers on the other hand may produce models that are hard to implement.
Developers will then be forced to find a workaround, because they can't question the model made by
the architect in the ivory tower. 

> If the people who write the code do not feel responsible for the model, or don't understand
> how to make the model work for an application, then the model has nothing to do with the software.
> If developers don't realize that changing code changes the model, then their refactoring
> will weaken the model rather than strengthen it.
>      
> Meanwhile, when a modeler is separated from the implementation process, he or she never acquires,
> or quickly loses, a feel for the constraints of the implementation.
> The basic constraint of MDD - that the model supports an effective implementation and abstract
> key domain knowledge - is half-gone, and the resulting models will be impractical.
>
> Finally, the knowledge and skills of experienced designers won;t be transferred to other developers 
> if the division of labor prevents the kind of collaboration that conveys the subtleties of coding a MDD

The need for hands-on modelers does not mean that team members cannot have specialized roles.
The problem arises from separating two tasks that are coupled, that is modeling and implementation.
The effectiveness of an overall design is very sensitive to the quality and consistency of 
fined-grained design and implementation decisions.
A portion of the code is an expression of the model; changing that code changes the model.

> Any technical person contributing to the model must spend some time touching the code,
> whatever primary role he or she plays on the project.
> Anyone responsible for changing code must learn to express a model through the code.  
> Every developer must be involved in some level of discussion about the model and have
> contact with domain experts.  
> Those who contribute in different ways must consciously engage those who touch the code 
> in a dynamic exchange of model ideas through the ubiquitous language.

## Conclusion

Domain driven design puts a model to work to solve problems for an application.
Through knowledge crunching, a team distills a torrent of chaotic information into a practical model.  
A Model driven design intimately connects the model and the implementation.
The ubiquitous language is the channel for all that information to flow between 
developers, domain experts and the software.

The result is software that provides rich functionality based on a fundamental understanding of the core domain.
As mentioned, success with Model driven design is sensitive too detailed design decisions.
