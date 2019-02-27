# CYBR 8480 Project Milestone 1: Project Ideation and Requirement Analysis
**Assigned: Wednesday 2/27/19**

## Due Date
March 13 (3/13/19) at 11:59PM, Discuss idea with Dr. Hale during class 3/14/19.

## Points
180 Project points (15% of overall grade), 10 Participation Points

## Overview
This project milestone tasks you with developing and expressing a project idea, identifying its requirements, and then analyzing them to determine needed resources and a project management plan for the rest of the semester. Towards this goal, you will be required to submit the following by the due date:

* [Executive Project Summary](#executive-project-summary) - What are you doing and why?
  - Goals and Objectives
  - Merit of the Project
* [Application requirements](#application-requirements) - What does your app/product do?
  - User stories
  - Misuser stories
* [Design](#design) - How is the app going to be designed?
  - Draw an architecture diagram of your proposed app
  - Identify significant design challenges
* [Security Analysis](#security-analysis) - What could go wrong and where might it affect your application?
* [Discussion](#discussion) - Talk to Dr. Hale about your idea

**All materials will be submitted on GitHub, be sure to slack message me with your GitHub Repo link.**

## Executive Project Summary
An executive summary should be evocative. It should capture a reader and make them want to be a part of your idea. In this milestone you will write an executive summary that defines the goals and objectives of your project in language that is easily readable and mental-image evoking. I (or anyone else) should be able to read your executive summary and instantly know a) what you are doing and b) why it is important. Executive summaries should be exciting and interesting. It is the first (and likely the only) chance for you to engage your reader and, in a real world setting, would determine if your product gets funded. An executive summary does not need technical detail to describe interesting functionality. You should mention your product by name without using phrases such as "the team", "the class", "the instructor", "project 2" etc.

### Submission materials
You should submit a summary document (in markdown format) on your GitHub project repo. Call the file README.md and place it in the top-level directory of your GitHub project.

It should contain the following:

1. A problem statement identifying the problem your product addresses.
1. Project goals and objectives in a numbered or bulleted list that you will undertake to address the identified problem.
1. The merit of accomplishing the project goals and objectives in terms of how it helps end users, society, or particular industries/sectors.

You can make use of the following markdown syntax to embed your executive summary in your README.md file:

```markdown
# Project Repo Name

## Executive Summary
Problem statement text goes here

## Project Goals
* Bulleted list item 1
* Bulleted list item 2
* etc
```

### Grading criteria
Your summaries will be graded as follows following:

| | Meets expectations (9-10) | Some Issues (6-8) | Does not meet expectations (0-5)|
|---|---|---|---|
| Problem statement | Clearly identifies the context of the problem addressed by your project. Answers the question - Why is this of interest? | Problem context not clearly identified, leaves reader wondering what the product is for. | Problem context unclear or not identified. |
| Project goals | Project goals are clear, concise, and in a bulleted list. Efforts are clearly tied to addressing the identified problem. Goals are stated at a high level and are free of technical jargon or unnecessary detail. | Goals are not as clear, 'in the weeds,' or not directly applicable to the problem. | No goals are identified or there are severe clarity issues. |
| Project Merit | The benefits for pursing the project are clear and tied to addressing the identified problem(s). End user, societal, and industrial benefits are stated - if relevant.| Benefits and merits of the proposed work are muddled or not tied to the problem statement. | Merits are difficult to identify or missing entirely. |
| Length | Summary is of reasonable length (no longer than 1 page, not too short)| Summary is slightly too short or too long | Summary is extremely short or long. |
| Grammar, spelling, syntax | Summary is evocative and free of grammar, spelling, or syntax issues. | Summary contains a few syntax, grammar, or spelling issues. | Summary is difficult to read due to glaring grammar, syntax, or spelling issues|
| Use of markdown | Summary should render as the project homepage on your GitHub repo. It should following markdown conventions. | Doesn't perfectly follow markdown syntax or isn't rendered on the repo home page correctly. | Doesn't use markdown or isn't displayed in the repo.|

## Application requirements
Requirements are extremely important for conducting a successful project. Collecting requirements about an application means understanding what your end user is going to do with the product. To understand requirements we often define user stories and use cases to encapsulate and represent behavior.

### Submission materials
#### User stories
For milestone 1, you should define the 3 most important user stories for your product. Pay careful attention to structure the user stories as we discussed in CYBR8470. Specifically, submit your user stories using the following template. Include them directly on, or as a link from, your GitHub repo README.md file.

As a **user/role**, I want to **goal** so I can **rationale**.

For each user story, also define acceptance criteria.
Your acceptance criteria should define the set of things required to understand when you are done with the user story.

You can make use of the following markdown syntax to embed your user stories in your README.md file:

```markdown
## User stories
As a **user/role**, I want to **goal** so I can **rationale**.
**Acceptance Criteria:**
* Insert criteria 1 here
* Insert criteria 2 here
* etc
```

#### Misuser stories
Also think about and define 2 misuser stories. Misuser stories are nothing more than user stories, except for users seeking to abuse your app. Use the same format as above, except replace user with misuser and use the ```goal``` to define the misuse goal. I.e.

As a **misuser**, I want to **misuse goal** so I can **bad rationale**.

e.g.

As a **Fitbit misuser**, I want to **exploit the Fitbit companion app** so I can **steal user Fitness and GPS data**.

Under each misuser story, identify at least one way you will counter this misuse in your application design.

You can make use of the following markdown syntax to embed your misuser stories in your README.md file:

```markdown
## Misuser stories
As a **misuser/misuser-role**, I want to **misuse goal** so I can **bad rationale**.
**Mitigations:**
* Mitigation technique 1 to be used goes here
* Mitigation technique 2 to be used goes here
* etc
```

### Grading Criteria
User stories and use cases will be graded as follows.

#### User stories
| Each user story (x3) | Meets expectations (4-5) | Some Issues (2-3) | Does not meet expectations (0-1)|
|---|---|---|---|
| Stated correctly | The user story identifies a user role, goal, and rationale that dictates a user behavior in the product to be created. | A role, goal, or rationale is missing. | Many issues with role, goal, or rationale identification |
| Acceptance Criteria | The user story has a reasonable, well thought out, set of acceptance criteria that dictate when the story is satisfied. | Some criteria are ill defined or ambiguous. Not enough criteria defined. | Many ill-defined or missing criteria.|

#### Misuser stories
| Each misuser story (x2) | Meets expectations (4-5) | Some Issues (2-3) | Does not meet expectations (0-1)|
|---|---|---|---|
| Stated correctly | The misuser story identifies a user type, goal, and rationale that dictates a potential misuser behavior in the product to be created. | A role, goal, or rationale is missing. | Many issues with role, goal, or rationale identification |
| Mitigation | The user story has a reasonable, well thought out, mitigation plan that dictates how the story will be thwarted. | Mitigation is ill defined or ambiguous. | Mitigation is extremely ill-defined, poorly thought out, and/or unrealistic.|


## Design
Once you have a set of requirements, the next step is to think about how you want to create an application that meets those demands. This is design. In Milestone 1 you will come up with a design that meets your project requirements. Your design should be kept to the component/service level. A design is only as effective as it is communicable. If your design is overcomplicated or difficult to describe, then it means that you may have a poor design. What I want to see for Milestone 1 is that you have a clear picture in mind for how you will make an app to meet your requirements.

**Remember that you only have roughly 1.5-2 months to work on your product, so keep scope in mind**

### Submission materials
You should **draw a picture of your overall application**. You may use any architecture style you wish, but I would recommend c4, read more at [https://c4model.com/](https://c4model.com/). The picture should identify the core components of your design and how they are connected. At a high level, there are three types of components you may need: `web services`, `mobile app(s)`, and `hardware devices` (e.g. IoT hardware). Web services are tools that (typically) deliver data to apps and maintain state across user sessions. They often also allow you to integrate your apps and devices with other apps, devices, and services. Mobile apps are what we have mainly focused on so far in this course. Hardware devices are sensors and actuators that sense or impact the world around them. Connections between components may exist over known protocols (bluetooth, http, etc) or may be internal to an app (e.g. function -> function in Android).

Your design should identify these high level components, but should also drill down to identify what each of these high level components will do - for instance, your hardware device might need to read temperature, your mobile app may need to be able to login to a webservice, pull down the temperature data from Omaha, and then compare it to the temperature measured by your hardware device and create a graph of temperature over time. This might require several subcomponents. **Your design should list them out, writing 1-2 sentences to describe each one**.

**TL;DR**
1) A picture that identifies components and their connections
2) a list of components with 1-2 sentences defining each one

You can make use of the following markdown syntax to embed your design in your README.md file:

```markdown
## High Level Design
![Tooltip for visually disabled](./path-to-image-file.imgextension)

## Component List
### Component 1 Name here
Component description here

#### Sub-component 1.1 name here
Sub component description here

#### Sub-component 1.2 name here
Sub component description here

### Component 2 Name here
Component 2 description here

#### Sub-component 2.1 name here
Sub component description here

#### Sub-component 2.2 name here
Sub component description here
```

### Grading Criteria
Your design will be evaluated as follows:

| | Meets expectations (9-10) | Some Issues (6-8) | Does not meet expectations (0-5)|
|---|---|---|---|
| Overviews big picture of components | Clear effective graphical depiction (picture) of your high level design. | Missing high level components in design. | No or poor high level picture. |
| Component / Sub-component list | Each major component in your app is listed with 1-2 sentences describing its functionality. | Some components are not described or descriptions are unclear. | Many missing or poor component descriptions. |
| Design quality | Design is clear, rational, and justifiable. | There are issues in the design that would limit or prevent product success. | Design is seriously deficient or unrealistic. |
| Design complexity | Design is effective and not overly complex to meet the requirements. | Design is overcomplicated in areas. | Design is seriously limited by many over-complications. |

## Security Analysis
As you know, there are many problems that can arise in the design and implementation of an app. You should analyze your design, while considering your misuse cases, to identify problem points where security challenges might exist.

### Submission materials
Using your high level architecture diagram and component list, identify potential problem areas and how they might be mitigated. Draw arrows, circle areas, or use other callout methods to show how the security problems you identify connect to your systems architecture.

You can make use of the following markdown syntax to embed your security analysis information in your README.md file:

```markdown
## Security analysis
Text describing high level diagram with red or other callouts identifying problem points or attacks.
![Tooltip for visually disabled](./path-to-image-file.imgextension)

| Component name | Category of vulnerability | Issue Description | Mitigation |
|----------------|---------------------------|-------------------|------------|
| Component 1 name | Privilege Escalation | This component exposes an interface to integrated webviews that might allow malicious javascript to read and modify protected data on the component that it shouldn't have access it. | Sandboxing techniques should encapsulate access permissions and capabilities for webviews individually to prevent privilege escalation.|
```

### Grading Criteria
Your security analysis will be graded as follows:

| | Meets expectations (9-10) | Some Issues (6-8) | Does not meet expectations (0-5)|
|---|---|---|---|
| Category and description| Category and description are appropriate and understandable. High level diagram is marked up in away that makes it easy to see where attacks target. | Some descriptions are unclear or missing. | Most or all descriptions are missing or unclear. |
| Coverage and relevance | Identified problems are relevant to the project and cover most the important potential problem areas. | Some coverage or relevance is missing. | Many potential problem areas are not considered |
| Mitigation Quality | Proposed mitigations are reasonable and appropriate | Some mitigations may not be feasible. | Many missing or non-sensical mitigations. |

### Discussion
The last element of your grade for Milestone 1, is just talking to Dr. Hale about your idea and getting some feedback. Come prepared to discuss the technology needed, the overall idea, and your initial thoughts for how you will go about achieving it.

### Submission materials
No extra materials for the discussion, come prepared with your other submission materials ready though for discussion.

#### License
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">CYBER4580 and related works</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://faculty.ist.unomaha.edu/mlhale" property="cc:attributionName" rel="cc:attributionURL">Matt Hale</a> are licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
