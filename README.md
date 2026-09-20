#### CS 3365 - Fall 2026

#### Class Project

#### Starting a product

# Overview
As we have addressed in class, appropriate product specification is key to the successful execution of a project. Thus, as the first deliverable for the class project, students will explore generating multiple high level requirement-specification products under different scenarios.

 

In the project we will leverage the use of AI models to simulate some parts of the requirements gathering process, to polish the documentation and contrast different versions to drive students to critique the specification, as it would happen in real life. Deliverables consist of product vision, persona definitions and user stories, associated with each product modeled.

# Objective
The main purpose of this assignment is to practice what would normally happen during a regular requirements elicitation and analysis phase, during the development of a software product.

# Detailed Requirements
During the course of the semester we will have fixed teams of 2 or 3 people, who will develop a prototype to address a specific product idea. In this first phase, we will explore multiple potential products to implement. One of the sets of documents generated during this first project phase will be selected for further class project stages starting from a general vision that will allow students to generate the next requirements layer.

 

For this, we will create documents with specific sections, one per product explored:

* Product overview and persona definitions
* 1-Pagers
* High level stories

## Product ideas
Students will need to select 2 out of the following options to generate the different product definitions. For each top level idea, students will need to generate documents by using the help of 2 completely different models (e.g. one by Anthropic and another one by Google or Open AI). Students are expected to document, in detail, how well they consider the models to have performed, which one was better, under what circumstances they did well, what prompts worked better, etc.

 

* **Personal Finance & Expense Tracker:** Interactive dashboard with dynamic spending charts, budget limits, and transaction categorization views.
* **Fitness & Workout Log App:** Mobile-first UI for logging daily workouts, tracking exercise sets, and viewing historical volume graphs.
* **Restaurant Ordering & Status Platform:** Dual-portal interface featuring a customer menu page and an admin view for tracking order status updates.
* **Recipe & Meal Planning Portal:** Searchable UI where users filter recipes by dietary tags, plan weekly meals, and auto-generate grocery lists.
 

## Product Overview 
Using 2 different models, as mentioned above, the students will generate two versions of product visions, consistent with book recommendations to write them. Students need to be confident about the final writeup generated and are advised to pay close attention and will be held responsible for the text generated (i.e. don't rely on just the model)

 

To an extent, the AI models will take on the role that a product manager will play. We can think of this as a “PM simulator”. Students should iterate on the product vision writeup and they are expected to provide early “draft versions” of each product vision as well as a detailed log of the prompts that were used to generate the visions.

## Persona definitions
Following up from the different product visions (4 in total), students will generate 4 sets of personas, derived from each vision. How many personas and the details behind them will need to be guided by the book and class discussions. Once again, students can use AI to help ideate, but they're responsible for the final written product.

## 1-Pagers / Epics
"1-pager" documents are common artifacts used in the industry to summarize the requirements for a set of features. It is common for 1-pagers to map to "Epics" (in agile terminology) that are then executed by Scrum teams. This type of document does not necessarily have a strict format. However, for the purposes of this project, students will be required to follow the template given at the end of this document.

 

Students will create multiple 1-pagers; enough to cover the requirements derived from each product vision and persona definitions. Remember, there are 4 sets of products we're dealing with. They will document any assumptions made to complement the requirements and, later, they will create the detailed stories needed to provide finer-grain requirements for later phases.

 

It is important that the level of detail is sufficient enough for Project Milestone 2.

 

# Grading considerations
This milestone is given a value of 10% of the semester grade. The compendium of documents will be turned in physically during class, on October 1, 2026.

 

Students are advised to review Chapter 3 of "Engineering Software Products" in detail, to make sure that Personas and Scenarios follow the best practices called out. 

 

Each person will assign a grade to each of the other students in the team, which they will send directly to the instructor. This will be done via email. Please use the subject "CS3365 - Project 1 Teammate Grades - [Student Name]" with each of the grades that person assigns to the other students, on a scale from 0 to 100. Grades will not be assigned to a student who has not turned in their peer evaluation. These grades will be taken into account when assigning the final number of points for this milestone.

### Rubric items
* Product vision statements
    * Detailed log of AI interactions
    * Critique of the different models generated and which was considered to be better and why
    * 4 visions addressed and well documented
* Personas
    * Sufficient level of detail
    * Adequate amount and specificity of personas
* Problem statements (1 per 1-pager)
    * Properly written scenarios
    * Sufficient coverage of the requirements
    * Appropriate complement with respect to assumptions
* Functional requirements
    * Written following class and book best practices
    * Sufficient coverage for the problem tackled
* Sizing
    * Rationale given for sizes
    * Appropriate metric assignment protocol
 

*Use the following as the template to create 1-pagers. Note that there can/should be multiple 1-pagers per product*

# [Initiative Name] 1-pager
 

## PROBLEM
*One to two paragraph description of the initiative. This should roughly match what Sommerville refers to as Scenarios in Chapter 3 of Engineering Software Products*

## ASSUMPTIONS
*Since the product vision is not complete, the team will need to define here all assumptions they had to make to complement the base requirements sketched in the vision.*

 

## FUNCTIONAL REQUIREMENTS

* *As a [persona], I want to [perform task] so that I can/in order to [description]*

    * *Possible detail A*

    * *Possible detail B*

* *As a [persona], I want to [perform task] so that I can/in order to [description]*

    * *Possible detail A*

    * *Possible detail B*

* *As a [persona], I want to [perform task] so that I can/in order to [description]*

    * *Possible detail A*

    * *Possible detail B*

## NON-FUNCTIONAL REQUIREMENTS
*E.g. SLAs, performance, security levels*

 

## REQUIREMENTS SIZING
*Select one type of metric to assess effort and provide an initial estimate for each of the stories in the functional requirements. Explain the rational to assign each size*