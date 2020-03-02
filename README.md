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

Sometimes, business rules are written in a cryptic if statement.

- Domain expert can't verify nor read it because it's too technical
- Developers / analysts will struggle to understand the concept behind the rule.

We can extract the if to a dedicated, well-named class responsible for validating the business rule.

Therefore the code is readable by everyone and the domain is clearly expressed.

## Chapter 2: Communication and the Use of Language

### Ubiquitous language

#### Different languages

A project faces serious problems when its language is fractured

Domain experts and developers are using a different language.
Therefore, day-to-day discussions is disconnected from the terminology embedded in the code.
Even developers have different language in speech and writing.

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
which will eventually require a refactor of class, methods and modules refactor,
in order to conform with the new model.
A change in the language is a change to the model.

Confusion, awkwardness or inadequate terms to convey domain understanding should
be fixed by domain experts.
Developers on the other hand should watch for ambiguity and inconsistency.

### Modeling out Loud

Play with the model as you talk about the system.

Describe scenarios out loud using the elements and interactions of the model,
combining concepts in ways allowed by the model.
Find easier ways to say what you need to say and take those new ideas back down the diagrams and code.

#### Example: Vague and technical

If we give to *Routing Service* an origin, destination and arrival time, it can look up the stops
the cargo will have to make and stick them in the database.

#### Example: More complete but verbose

The origin, destination and so on.. it all feeds into the Routing Service and we get back an Itinerary 
that has everything we need in it.

#### Example: concise

A Routing Service finds an Itinerary that satisfies a Route Specification. 

### One Team, One Language

Technical people often feel the need to **shield** domain experts from the domain model.

- Too abstract for them
- They don't understand objects
- We have to collect requirements in their terminology

**If sophisticated domain experts don't understand the model, there is something wrong with the model.**

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