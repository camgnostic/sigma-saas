# United States Identification Challenge Tasks

## Description

A student opens their console and is presented with some kind of invitation/reminder to study their US states. The student engages this notice and is brought to some kind of a study interface, presenting some mix of:

1. "Identify the state" challenges, in which the student is presented with a map of the united states with state lines drawn and one state colored and asked to type the name of the state. Perhaps there is some kind of fuzzy matching for this input.
2. "Click the state" challenges, in which the student is presented with a state name and a map of the US (with state lines drawn) and asked to click on the named state.

The student's teacher can then review this student's activity. This review should include some measure of "did they do what I told them to do" (engage their US state study) and some measure of "did they do well at it"(perhaps number of questions missed).

The student's teacher MAY also have some kind of a summary of "did they do what I told them to do" and "did they do well at it" for the entire class.

Notably not mentioned here is challenge scheduling (shall the system today ask them to identify New Jersey, shall the system wait till a student is able to click on a state before asking them to produce the state name, etc.). Discuss if so inclined.

### Responses

#### Cameron

- "opens their console" -> can you elaborate?

- Would our schema as we're thinking of it be as specific as to describe the specific subsets of challenges or would it merely describe a "challenge" page with a "question" display element and an "answer" input element?

  - To this point: I guess this goes to the nature of what our language is for... I mean, is the purpose to prototype a skeleton where the first view the dev looks at after running "build" is to see (literally) "Question" and a field for "Answer"?
  - Put another way - are the specifics of how to implement the various state challenges part of the program-specific logic (the part we're trying to get to faster) or part of the infrastructure (the part we're trying to abstract away / avoid boilerplating / meta-program)?

- RESTful API = stateless.  Our SPA should be (roughly) stateless (or else we're sort of overlaying state using JS which is awful).  User stories are stateful.
  - Agree?
  - As such: should we view the semantic language as a sort of map of stateless pages that can be traversed in the order specified in the user story (but don't explicitly describe that routing)?
  - Put another way - do we sort of view the path from user story -> specification as a stripping of directionality (and even edges altogether) from the directed graph of user stories and producing a well-defined set of nodes?

```
student-page:
  notifications
  link to state to name challenge (perhaps included in notification)
  link to name to state challenge (perhaps included in notification)
teacher-page
  link to review specific student recent activity (quantity)
  link to review specific student recent activity (quality)
  summary of student recent activity (quantity)
  summary of student recent activity (quality)
```

#### Joseph

### Response to Responses

#### Cameron

#### Joseph
