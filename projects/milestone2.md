## CYBR 8480 Project Milestone 2: Prototype development
**Assigned: Tuesday 4/4/17**

### Due Date
Monday April 17th (4/17/17) at 11:59PM, Presentation and Demo 4/18/17.

### Overview
This project milestone tasks you with building a prototype application that addresses your top User stories. This means you will be creating features to support and realize your user stories. The milestone also tasks you with generating relevant documentation associated with design and implementation of your app. Towards this goal, you will be required to submit the following by the due date:

- [Component-based Architectural Diagram](#architectural-diagram) - How do the components in your product work together?
- [User story realization](#user-story-realization) - Document and describe what was done.
  - Identify tasks achieved in this product increment (an agile term for the things you produce)
  - Bind tasks, code artifacts, and documentation together
- [Presentation](#presentation) - Demo and discuss your milestone 2 work with Dr. Hale and the class
  - Focus on achieving primary user story

**All materials will be submitted on GitHub, be sure to slack message me with your GitHub Repo link.**

### Architectural Diagram
An architecture diagram clearly identifies the various components and connectors that comprise a product. For this part of Milestone 2, you should create a diagram that shows how the components in your product are composed together. This means you should identify which components fit into your design, how you plan to connect them together, and how other (third party, etc) components fit into the design. Think about questions such as "What layers exist in my application?, Are components cleanly separated from one another and are they appropriately coupled and cohesive?, How is data passed between components or external resources (e.g. are APIs being used appropriately)?"

#### Submission materials
You should create your diagram using an architectural tool such as Lucidchart, MS Visio, or similar tools. You should include the diagram in your README.md file, in your Github repo, as an image and/or link to Lucidchart.

It should contain the following:

1. Components, represented as a box or a small picture. Each component must have a label that names it. Each component should identify input and output interfaces. On a separate note (in markdown), you should briefly list and explain what each component does.
1. Connectors, represented as arrows with appropriately labeled data sent over the connectors.
1. Other grouping concepts, as necessary. In some cases, components may have sub components, systems might be part of a larger system of systems, or there could be other needs for identifying clusters of concepts. Use these where necessary.

**Follow UML or UML-like conventions to build your diagram**
For more information on component diagrams, see:
* [http://www.uml-diagrams.org/component-diagrams-reference.html](http://www.uml-diagrams.org/component-diagrams-reference.html)
* [http://agilemodeling.com/artifacts/componentDiagram.htm](http://agilemodeling.com/artifacts/componentDiagram.htm)

### Grading criteria
Your architecture diagram will be graded as follows:

| | Meets expectations (9-10) | Some Issues (6-8) | Does not meet expectations (0-5)|
|---|---|---|---|
|Appropriate Components| Identifies relevant components in your product design | some components are tangential to user stories | components are not relevant to user stories |
|Component descriptions| Each component is described in accompanying text (in markdown). | Some descriptions are missing. | Components are not described in text.|
|Component labels| Each component is labeled and the labels are relevant. | Some components are not labeled, or are labeled poorly. | Many components are not labeled, or labeled poorly.|
|Coverage| Diagram contains a reasonable number of components for your user stories and product | Some obvious components are missing from the diagram | Many components are missing from the diagram|
|Usage of interfaces| Components clearly identify the input and output interfaces that make available | Some interfaces between components are undefined or unidentified | Many missing interfaces.|
|Appropriate grouping and clustering| Concepts are grouped according to function or how they appear in the product. | There are some issues of grouping and clustering concepts.|  There are multiple issues with clustering and grouping concepts.|
|Clear and understandable| The diagram clearly and unambiguously conveys the structure of the application or product. | The diagram leaves some concerns open for interpretation.| The diagram is not clear or understandable.|

### User story realization
Once you've created a component diagram, begin drilling into actually realizing (i.e. completing) your user stories. This means actually start coding and working to develop the features to support the stories. As you do this, keep basic documentation to connect your work to the ideas that created it. Make sure to update your component diagram if anything changes.

#### Submission materials
You should prepare a prototype application/product that demonstrates the three selected user stories. The prototype should include an IoT component and a mobile app. The app may be hybrid or native. The IoT component should use Bluetooth or another wireless protocol (such as RFID or Wi-Fi) to communicate. All code should be properly documented - with non-trivial code (such as methods and algorithms) briefly explained in-line using appropriate comments. Update your component descriptions associated with the architecture diagram with appropriate references in the code (where applicable). The last element of submission materials include a demo-ready compiled app that can demonstrate some basic functionality.

#### Grading Criteria
Your will be graded as follows:

| | Meets expectations (33-40) | Some Issues (25-32) | Does not meet expectations (0-24)|
|---|---|---|---|
|Effort and progress| It is clear that the team has made non-trivial effort and progress towards user story realization.| There is some evidence of effort and progress, but more could have been done in the time. | Little effort or progress was made towards user story realization.|
|Documentation| Code artifacts and tasks are documented well. Documentation is clear and illustrative. | Some code is documented, but large portions are not. | Little or no documentation.|
|Prototype Demo| The product is successfully demoed for Dr. Hale and the class. The team addresses and handles questions well. | The demo partially works, but there are some significant issues. | Many significant issues or non-functional prototype.|

### Presentation
You will be expected to present your Milestone 2 achievements to the class following the deadline. It is important that you use this time to both inform your classmates of your activities and to get feedback. You will be expected to Demo your prototype product.

#### Submission Materials
Submit your slides to Dr. Hale by 11:59pm on the day of the presentation. Submit them by posting and pinning them in your team slack channel.

#### Grading Criteria
You will be graded by a rubric TBA.

#### License
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">CYBER4580 and related works</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://faculty.ist.unomaha.edu/mlhale" property="cc:attributionName" rel="cc:attributionURL">Matt Hale</a> are licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
