If you like green, here is another version: https://aclaudel.github.io/ddd-book-summary/

# I - Putting the domain model to work 

## The utility of a Model in DDD

- *The model and the heart of the design shape each other.*
  The intimate link between the model and the implementation makes the model relevant.
  This binding will also help during maintenance and continuous development, because the code
  can be interpreted based on understanding the model
  
- *The model is the backbone of a language used by all team members*.
  Because of the binding between model and implementation, developers can talk about the program,
  with domain experts, without any translation.
  Because the language is based on the model, our natural linguistic abilities
  can be turned to refining the model itself.
  
- *The model is distilled knowledge*
  A model captures how we choose to think about the domain as we select terms, break down concepts,
  and relate them.
  The shared language allows effective collaboration between developers and domain experts.

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

Difficulties in formulating sentences should lead to new model alternatives,
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

Projects that have no domain model at all, but just write code to fulfill one function after another,
gain few of the advantages of knowledge crunching and communication.
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


# III - Refactoring Toward Deeper Insight (first run)

## Chapter 11: Applying Analysis Patterns

nothing interesting.

## Chapter 12: Relating Design Patterns to the Model

Even tought most of the patterns from the book *Design Patterns* are technical, 
some of them can be applied to a broader context of domain modeling and design.

Here is the definition from *Design Patterns*: 
> The design patterns in this book are descriptions of communicating objects and classes
> that are customized to solve a general design problem in a particular context.

When using a technical pattern in the domain layer, we have to add an additional motivation,
an other layer of meaning.  
For example, if the pattern *Strategy* corresponds to an actual business strategy (ex: policies),
the pattern becomes more than just a useful implementation technique.

## Chapter 13: Refactoring Toward Deeper Insight

There are three things you have to focus on:
- Live in the domain
- Keep looking at things a different way
- Maintain an unbroken dialog with domain experts

The classic refactoring scenario is two developers, looking at the code and changing it on the fly.
This practice should happen all the time, but it isn't the whole story.

### Initiation

Refactoring can begin in many ways, it may be a response to a problem in the code (complexity or awkwardness).
But instead of just immediately refactoring the code, developers sense that the root of the problem is in the domain model.
Perhaps a concept is missing, maybe some relationship is wrong.

This means that the refactoring could occur, even if the code is clean and tidy,
just because the language seems disconnected from the domain experts
or new requirements are not fitting in naturally.
It might result from learning, as a developer who has gained deeper understanding
of the domain and see an opportunity to improve the model.

### Exploration Teams

The next step is to seek refinement that will make the model communicate clearly and naturally.
This might require only some modest change and take few hours.
However sometimes, finding a new model may require more time and involve more people.

In that case, it's a good idea to pick a couple of developers with strong problem solving skills
or who know the model well.
Be sure to include a domain expert, find a coffee shop and brainstorm for around an hour.
Sketch some UML diagrams, walk through scenarios, the goal is to find an understandable and useful model.

After that, you can either go back and code some prototypes, or have some sleep to think about it
and go throught the same exercise again.

There are few keys to keep this productive:
- *Self-determination*. A small team, assembled on the fly to explore a design problem only for a few days.
  No need for long-term, elaborate organizational structures.
- *Scope and sleep*. Two or three short meetings spaced out over a few days.
  If you get stuck, you may be taking too much at once.
- *Execising the ubiquitous language*. Involving other team members creates an opportunity
  to exercise and refine the ubiquitous language.
  The end result is a refinement of that language which the developer will take back and formalize in code.

### A design for Developers

Software isn't just for users, it's also for developers.
Developers change the code again and again while refactoring, which should lead to a supple design.
A supple design communicates its intent.

It makes easy to anticipate the effect of running code and therefore easy to anticipate
consequences of changing it.
It helps limit mental overload, by reducing dependencies and side effects.
It is based on a deep model of the domain that is fine-grained only where most critical to the users.

This makes for *flexibility* where change is mot common and *simplicity* elsewhere.

### Timing

*If you wait until you can make a complete justification for a change, you've waited too long.*  
Continuous refactoring has come to be considered as best practice, but most teams are still cautious about it.

It's easy to see the risk of changing code and the cost of developer time to make the change.
It's harder to see the risk of keeping an awkward design and the cost of working around it.
Developers are often asked to justify their decision to refactor, but it's not always simple.

Refactoring toward deeper inshight needs to become part of the ongoing exploration of the domain,
the education of the developers and the meeting of the minds of developers and domaine experts.
Refactor when:
- The design does not express the current understanding of the domain.
- Important concepts are implicit in the design (and you see a way of making them explicit)
- You seee an opportunity to make some important part of the design suppler.

This aggressive attitude does not justify any change at any time.  
Don't refactor a day before relase, don't try to demonstrate your technical skills
nor try to push a model that domain experts struggle to understand.

Don't be absolute, but push beyond the comfort zone in the direction of favoring refactoring.

### Crisis as Opportunity

Punctuated equilibrium (Charles Darwin):
*Long periods of gradual change or stability are interrupted by relatively short bursts of rapid change.
Then things settle down into a new equilibrium.*

Classic refactoring sound steady, refactoring toward deeper insight usually isn't.
A period of steady refinement of a model can suddendly bring you to an insight that shakes up everything.

Such a situation ofthen does not look like an opportunity: it seems more like a crisis.
Suddenly, there is some obious inadequacy with the model. 
There is a gaping hole in what it can be express, or some critical area where it is opaque.
Maybe it makes statements that are just wrong.

This means the team has reached a new level of understanding.
From their now-elevated viewpoint, the old model looks poor.
From that viewpoint, they can conceive a far better one.

Refactoring toward deeper insight is a continuing process.
Implicit concepts are recognized and made explicit.
Parts of the design are made suppler, perhaps taking on a declarative style.

# IV - Strategic Design (first run)

This part of the book presents principles that enable the modeling process to scale up to very complicated domains.

The goal of the most ambitious enterprise system is a tightly integrated system spanning the entire business.
Yet the entire business model for almost any such organization is too large and complex to manage or even
understand as a single unit.
The system must be broken down into smaller parts, in both concept and implementation.
The challenge is to accomplish this modularity *without losing the benefits of integration*.

A monolithic, all-encompassing domain model will be unwieldy and loaded with subtle duplications and contradictions.
A set of small, distinct subsystems glued together with ad-hoc interfaces will lack the power
to solve enterprise-wide problems and allows consistency problems to arise at every integration point.  
The pitfalls of both extremes can be avoided with a systematic, evolving design strategy.

Strategic design must guide design decisions to reduce the interdependence of parts and improve clarity
without losing critical interoperability and synergy.
They must focus the model to capture the conceptual core of the system, the *vision* of the system.
*And they must do all this without bogging the projct down*.

To help accomplish these goals, there are three themes: context, distillation and large-scale structure.

*Context*. A successful model has to be logically coonsistent throughout, without contradictory or overlapping definitions.
Unifiying integrated subsystems and distinct applications with various origins and domain views can be tricky.  
By explictitely definings **Bounded Context** withing which a moodel applies and then,
when necessary, defining its relationship with other contexts,
the modeler can avoid bastardizing the model.
