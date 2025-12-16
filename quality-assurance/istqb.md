# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Chapter 1 - Fundamentals of testing](#chapter-1---fundamentals-of-testing)
    - [Why is testing necessary?](#why-is-testing-necessary)
    - [What is testing? Testing principles.](#what-is-testing-testing-principles)
    - [Fundamental test process.](#fundamental-test-process)
    - [The psychology of testing.](#the-psychology-of-testing)
    - [SAMPLE EXAM QUESTIONS](#sample-exam-questions)
  - [Chapter 2 - Testing throughout the software life cycle](#chapter-2---testing-throughout-the-software-life-cycle)
    - [Software development models](#software-development-models)
    - [Test levels](#test-levels)
    - [Test types: the targets of testing](#test-types-the-targets-of-testing)
    - [Maintenance testing](#maintenance-testing)
    - [SAMPLE EXAM QUESTIONS](#sample-exam-questions-1)
  - [Chapter 3 - Static techniques](#chapter-3---static-techniques)
    - [Reviews and the test process](#reviews-and-the-test-process)
    - [Review process](#review-process)
    - [Static analysis by tools](#static-analysis-by-tools)
    - [SAMPLE EXAM QUESTIONS](#sample-exam-questions-2)
  - [Chapter 4 - Test design techniques](#chapter-4---test-design-techniques)
    - [Identifying test conditions and designing test cases](#identifying-test-conditions-and-designing-test-cases)
    - [Categories of test design techniques](#categories-of-test-design-techniques)
    - [Specification-based or black-box techniques](#specification-based-or-black-box-techniques)
    - [Structure-based or white-box techniques](#structure-based-or-white-box-techniques)
    - [Experience-based techniques](#experience-based-techniques)
    - [Choosing a test technique](#choosing-a-test-technique)
    - [SAMPLE EXAM QUESTIONS](#sample-exam-questions-3)
  - [Chapter 5 - Test management](#chapter-5---test-management)
    - [Test organization](#test-organization)
    - [Test plans, estimates, and strategies](#test-plans-estimates-and-strategies)
    - [Test progress monitoring and control](#test-progress-monitoring-and-control)
    - [Configuration management](#configuration-management)
    - [Risk and testing](#risk-and-testing)
    - [Incident management](#incident-management)
    - [SAMPLE EXAM QUESTIONS](#sample-exam-questions-4)
  - [Chapter 6 - Tool support for testing](#chapter-6---tool-support-for-testing)
    - [Types of test tool](#types-of-test-tool)
    - [Effective use of tools: Potential benefits and risks](#effective-use-of-tools-potential-benefits-and-risks)
    - [Introducing a tool into an organization](#introducing-a-tool-into-an-organization)
    - [SAMPLE EXAM QUESTIONS](#sample-exam-questions-5)
  - [References](#references)

---

## Chapter 1 - Fundamentals of testing 

### Why is testing necessary?  

From Section 1.1, you should now be able to explain why testing is necessary  
and support that explanation with examples and evidence. You should be able  
to give examples of negative consequences of a software defect or bug for  
people, companies, and the environment. You should be able to contrast a  
defect with its symptoms. You should be able to discuss the ways in which  
testing fits into and supports higher quality. You should know the glossary terms  
**bug**, **defect**, **error**, **failure**, **fault**, **mistake**, **quality**, **risk**, **software**,  
**testing** and **exhaustive testing**.  

> **defect** - An imperfection or deficiency in a work product where it does not meet its requirements or  
specifications or impairs its intended use.

> **error** - A human action that results in a defect.

> **failure** - An event in which a component or system does not meet its requirements within specified limits.

> **quality** - The degree to which a work product satisfies stated and implied requirements.

> **risk** - A factor that could result in future negative consequences. 

> **testing** - The process within the software development lifecycle that evaluates the quality of a component  
or system and related work products.

> **exhaustive testing** - A test approach in which the test suite comprises all combinations of input values and  
preconditions.

### What is testing? Testing principles.

From Section 1.2, you should now know what testing is. You should be able  
to remember the common objectives of testing. You should be able to describe  
how testing can find defects, provide confidence and information and prevent  
defects. You should be able to explain the fundamental principles of testing,  
summarized in Section 1.3. You should know the glossary terms **code**, **debugging**,  
**development of software**, **requirement**, **review**, **test basis**,  
**test case**, **testing** and **test objective**.  

> **debugging** - The process of finding, analyzing and removing the causes of failures in a component or system.

> **requirement** - A provision that contains criteria to be fulfilled.

> **review** - A type of static testing in which the quality of a work product or process is evaluated by individuals.

> **test basis** - The body of knowledge used as the basis for test analysis and test design.

> **test case** - A set of preconditions, inputs, actions (where applicable), expected results and postconditions,  
developed based on test conditions.

> **testing** - The process within the software development lifecycle that evaluates the quality of a component or system and related work products.

> **test objective** - The purpose for testing.

### Fundamental test process.

From Section 1.4, you should now recognize the fundamental test process, as  
well as being aware of some other related ways to model the test process. You  
should be able to recall the main testing activities related to test planning and  
control, analysis and design, implementation and execution, evaluating exit criteria and reporting, and test closure.   
You should know the glossary terms **confirmation testing**, **exit criteria**, **incident**, **regression testing**,   
**test basis**, **test condition**, **test coverage**, **test data**, **test execution**, **test log**, **test plan**,  
**test strategy**, **test summary report** and **testware**.

> **confirmation testing** - A type of change-related testing performed after fixing a defect to confirm that a  
failure caused by that defect does not reoccur.

> **exit criteria** - The set of conditions for officially completing a defined task.

> **regression testing** - A type of change-related testing to detect whether defects have been introduced  
or uncovered in unchanged areas of the software.

> **test basis** - The body of knowledge used as the basis for test analysis and test design.

> **test condition** - A testable aspect of a component or system identified as a basis for testing.

> **coverage** - The degree to which specified coverage items are exercised by a test suite, expressed  
as a percentage.

> **test data** - Data needed for test execution.

> **test execution** - The activity that runs a test on a component or system producing actual results.

> **test log** - A chronological record of relevant details about the execution of tests.

> **test plan** - Documentation describing the test objectives to be achieved and the means and the schedule  
for achieving them, organized to coordinate testing activities.

> **test strategy** - A description of how to perform testing to reach test objectives under given circumstances.

> **test completion report** -A type of test report produced at completion milestones that provides an evaluation of  
the corresponding test items against exit criteria.

> **testware** - Work products produced during the test process for use in planning, designing, executing, evaluating  
and reporting on testing.

### The psychology of testing.

Finally, from Section 1.5, you now should be able to explain the psychology  
of testing and how people influence testing success. You should recall the  
importance of clear objectives, the right mix of self-testing and independent  
testing and courteous, respectful communication between testers and others on  
the project team, especially about defects. You should be able to explain and  
contrast the mindsets of testers and programmers and why these differences can  
lead to conflicts. You should know the glossary term **independence**  

> **independence of testing** - Separation of responsibilities, which encourages the accomplishment of  
objective testing.

### SAMPLE EXAM QUESTIONS

1) A company recently purchased a commercial off-the-shelf application to automate  
their bill-paying process. They now plan to run an acceptance test against the package prior to  
putting it into production. Which of the following is their most likely reason for testing?  

1. To build confidence in the application.
1. To detect bugs in the application.
1. To gather evidence for a lawsuit.
1. To train the users
    <details><summary>Answer:</summary>1</details></br>

2) According to the ISTQB Glossary, the word **bug** is synonymous with which of the following words?

1. Incident
1. Defect
1. Mistake
1. Error
    <details><summary>Answer:</summary>2</details></br>

3) According to the ISTQB Glossary, a **risk** relates to which of the following?

1. Negative feedback to the tester.
1. Negative consequences that will occur.
1. Negative consequences that could occur.
1. Negative consequences for the test object.
    <details><summary>Answer:</summary>3</details></br>

4) Ensuring that test design starts during the requirements definition phase is important to enable which  
of the following test objectives?

1. Preventing defects in the system.
1. Finding defects through dynamic testing.
1. Gaining confidence in the system.
1. Finishing the project on time.
    <details><summary>Answer:</summary>1</details></br>

5) A test team consistently finds between 90% and 95% of the defects present in  
the system under test. While the test manager understands that this is a good defect-detection  
percentage for her test team and industry, senior management and executives remain disappointed  
in the test group, saying that the test team misses too many bugs. Given that the users are generally  
happy with the system and that the failures which have occurred have generally been low impact,  
which of the following testing principles is most likely to help the test manager explain to these  
managers and executives why some defects are likely to be missed?  

1. Exhaustive testing is impossible
1. Defect clustering
1. Pesticide paradox
1. Absence-of-errors fallacy
    <details><summary>Answer:</summary>1</details></br>

6) According to the ISTQB Glossary, regression testing is required for what purpose?

1. To verify the success of corrective actions.
1. To prevent a task from being incorrectly considered completed.
1. To ensure that defects have not been introducedby a modification.
1. To motivate better unit testing by the programmers.
    <details><summary>Answer:</summary>3</details></br>

7) Which of the following is most important to promote and maintain good relationships between   
testers and developers?

1. Understanding what managers value about testing.
1. Explaining test results in a neutral fashion.
1. Identifying potential customer work-arounds for bugs.
1. Promoting better quality software whenever possible.
    <details><summary>Answer:</summary>2</details></br>

8) Which of the statements below is the best assessment of how the test principles apply   
across the test life cycle?

1. Test principles only affect the preparation for testing.
1. Test principles only affect test execution activities.
1. Test principles affect the early test activities such as review.
1. Test principles affect activities throughout the test life cycle.
    <details><summary>Answer:</summary>4</details></br>

## Chapter 2 - Testing throughout the software life cycle

### Software development models

From Section 2.1, you should now understand the relationship
between development and testing within a development life cycle,
including the test activities and test (work) products. You should
know that the development model to use should fit, or must be
adapted to fit, the project and product characteristics. You should
be able to recall the reasons for different levels of testing and
characteristics of good testing in any life cycle model. You should
know the glossary terms (**commercial**) **off-the-shelf software**
(**COTS**), **incremental development model**, **test level**, **validation**,
**verification** and **V-model**.

> **commercial off-the-shelf** - A type of product developed in an identical format for a large number  
of customers in the general market. 

> **incremental development model** - A type of software development lifecycle model in which the component  
or system is developed through a series of increments.

> **test level** - A specific instantiation of a test process.

> **validation** - Confirmation by examination that a work product matches a stakeholder's needs.

> **verification** - The process of confirming that a work product fulfills its specification.

> **V-model** - A sequential software development lifecycle model describing a one-for-one relationship between major  
phases of software development from business requirements specification to delivery, and corresponding test levels  
from acceptance testing to component testing.

### Test levels

From Section 2.2, you should know the typical levels of testing. You should be able to compare the different levels   
of testing with respect to their major objectives, typical objects of testing, typical targets of testing (e.g.   
functional or structural) and related work products. You should also know which persons perform the testing   
activities at the various test levels, the types of defects found and failures to be identified. You should know the  
glossary terms **alpha testing**, **beta testing**, **component testing**, **driver**, **functional requirements**,   
**integration**, **integration testing**, **non-functional testing**, **operational testing**, **regulation acceptance  testing** (**compliance testing**),  
**robustness testing**, **stub**, **system testing**, **test-driven development**, **test environment** and **user acceptance testing**.

> **alpha testing** - A type of acceptance testing performed in the developer's test environment by roles outside the  
 development organization.

> **beta testing** - A type of acceptance testing performed at an external site to the developer's test environment by  
roles outside the development organization.

> **component testing** - A test level that focuses on individual hardware or software components.

> **driver** - A component or tool that temporarily replaces another component and controls or calls a test item in   
isolation.

> **integration testing** - A test level that focuses on interactions between components or systems.

> **non-functional testing** - Testing performed to evaluate that a component or system complies with non-functional requirements.

> **compliance testing** - Testing to determine the compliance of the component or system.

> **stub** - A type of test double providing predefined responses.

> **system testing** - A test level that focuses on verifying that a system as a whole meets specified requirements.

> **test-driven development** - A software development technique in which the test cases are developed, automated  
and then the software is developed incrementally to pass those test cases.

> **test environment** - An environment containing hardware, instrumentation, simulators, software tools, and other  
support elements needed to perform a test.

> **user acceptance testing** - A type of acceptance testing performed to determine if intended users accept the system.

### Test types: the targets of testing

From Section 2.3, you should know the four major types of test (functional, non-functional, structural and change-related) and should be able to provide some concrete examples for each of these. You should understand that functional and structural tests occur at any test level and be able to explain how they are applied
in the various test levels. You should be able to identify and describe non-functional test types based on non-functional requirements and product quality characteristics. Finally you should be able to explain the purpose of confirmation testing (retesting) and regression testing in the context of change-related testing. You should know the glossary terms **black-box testing**, **code coverage**, **confirmation testing** (**re-testing**), **functional testing**, **interoperability testing**, **load testing**, **maintainability testing**, **performance testing**, **portability testing**, **regression testing**, **reliability testing**, **security testing**, **specification-based testing**, **stress testing**, **structural testing**, **test suite**, **usability testing** and **white-box testing**.

> **black-box testing** - Testing based on an analysis of the specification of the component or system.

> **coverage** - The degree to which specified coverage items are exercised by a test suite, expressed as a percentage.

> **confirmation testing** - A type of change-related testing performed after fixing a defect to confirm that a failure caused by that defect does not reoccur.

> **functional testing** - Testing performed to evaluate if a component or system satisfies functional requirements.

> **interoperability** - The degree to which two or more components or systems can exchange information and use the information that has been exchanged.

> **load testing** - A type of performance testing conducted to evaluate the behavior of a component or system under  
varying loads, usually between anticipated conditions of low, typical, and peak usage.

> **maintainability** - The degree to which a component or system can be modified by the intended maintainers.

> **performance testing** - A test type to determine the performance efficiency of a component or system 

> **portability** - The degree to which a component or system can be transferred from one hardware, software or other operational or usage environment to another.

> **regression testing** -  A type of change-related testing to detect whether defects have been introduced or  
uncovered in unchanged areas of the software.

> **reliability** - The degree to which a component or system performs specified functions under specified   
conditions for a specified period of time.

> **security testing** - A test type to determine the security of a component or system.

> **stress testing** - A type of performance testing conducted to evaluate a system or component at or beyond the limits of its anticipated or specified workloads, or with reduced availability of resources such as access to memory or servers.

> **test suite** - A set of test scripts or test procedures to be executed in a specific test run.

> **usability testing** - Testing to evaluate the degree to which the system can be used by specified users with  
effectiveness, efficiency and satisfaction in a specified context of use.

> **white-box testing** - Testing based on an analysis of the internal structure of the component or system.

### Maintenance testing

From Section 2.4, you should be able to compare maintenancetesting to testing of new applications.   
You should be able to identify triggers and reasons for maintenance testing, such as modifications, migration  
and retirement. Finally you should be able to describe the role of regression testing and impact analysis within  
maintenance testing. You should know the glossary terms **impact analysis** and **maintenance testing**.

> **impact analysis** - The identification of all work products affected by a change, including an estimate of  
the resources needed to accomplish the change

> **maintenance testing** - Testing the changes to an operational system or the impact of a changed environment  
to an operational system.

### SAMPLE EXAM QUESTIONS

1) What are good practices for testing within the development life cycle?
    
1. Early test analysis and design.
1. Different test levels are defined with specific objectives.
1. Testers will start to get involved as soon as coding is done.
1. A and B above.
    <details><summary>Answer:</summary>4</details></br>

2) Which option best describes objectives for test levels with a life cycle model?

1. Objectives should be generic for any test level.
1. Objectives are the same for each test level.
1. The objectives of a test level don't need to be defined in advance.
1. Each level has objectives specific to that level.
    <details><summary>Answer:</summary>4</details></br>

3) Which of the following is a test type?

1. Component testing
1. Functional testing
1. System testing
1. Acceptance testing
    <details><summary>Answer:</summary>2</details></br>

4) Which of the following is a non-functional quality characteristic?

1. Feasibility
1. Usability
1. Maintenance
1. Regression
    <details><summary>Answer:</summary>2</details></br>

5) Which of these is a functional test?

1. Measuring response time on an on-line booking system.
1. Checking the effect of high volumes of traffic in a call-center system.
1. Checking the on-line bookings screen information and the database contents against the   
information on the letter to the customers.
1. Checking how easy the system is to use.
    <details><summary>Answer:</summary>3</details></br>

6) Which of the following is a true statement regarding the process of fixing emergency changes?

1. There is no time to test the change before it goes live, so only the best developers should  
do this work and should not involve testers as they slow down the process.
1. Just run the retest of the defect actually fixed.
1. Always run a full regression test of the whole system in case other parts of the system have  
been adversely affected.
1. Retest the changed area and then use risk assessment to decide on a reasonable subset of the  
whole regression test to run in case other parts of the system have been adversely affected.
    <details><summary>Answer:</summary>4</details></br>

7) A regression test:

1. Is only run once.
1. Will always be automated.
1. Will check unchanged areas of the software to see if they have been affected.
1. Will check changed areas of the software to see if they have been affected.
    <details><summary>Answer:</summary>3</details></br>

8) Non-functional testing includes:

1. Testing to see where the system does not function correctly.
1. Testing the quality attributes of the system including reliability and usability.
1. Gaining user approval for the system.
1. Testing a system feature using only the software required for that function.
    <details><summary>Answer:</summary>2</details></br>

9) Beta testing is:

1. Performed by customers at their own site.
1. Performed by customers at the software developer's site.
1. Performed by an independent test team.
1. Useful to test software developed for a specific customer or user.
    <details><summary>Answer:</summary>1</details></br>

## Chapter 3 - Static techniques

### Reviews and the test process

From Section 3.1, you should be able to explain the importance and advantages of static testing. You should know  
the difference between static testing and dynamic testing, and also understand the concept of reviews. You should  
be able to recognize the software work products that can be examined by static testing. You should know the glossary  
terms **static testing**, **dynamic testing** and **reviews**.

> **static testing** - Testing that does not involve the execution of a test item.

> **dynamic testing** - Testing that involves the execution of the test item.


### Review process

From Section 3.2, you should understand the difference between formal and informal reviews. You should be able to  
recall the main phases of a typical formal review. The main roles within reviews and their responsibilities should  
be clear to you. You should know the differences between the various types of formal review: technical review,  
walkthrough and inspection. Finally you should be able to explain the factors for successful performance of reviews.  
You should know the glossary terms **entry criteria**, **exit criteria**, **formal review**, **informal review**,  
**inspection**, **moderator**, **reviewer**, **scribe**, **technical review** and **walkthrough**.

> **entry criteria** - The set of conditions for officially starting a defined task.

> **exit criteria** - The set of conditions for officially completing a defined task.

> **formal review** - A review that follows a defined process with a formally documented output.

> **informal review** - A type of review that does not follow a defined process and has no formally documented output.

> **inspection** - A type of formal review that uses defined team roles and measurement to identify defects in a work  
product, and improve the review process and the software development process.

> **moderator** - The person responsible for running review meetings. (2) The person who performs a usability  
test session.

> **reviewer** - A participant in a review who identifies defects in the work product.

> **scribe** - A person who records information at a review meeting.

> **technical review** - A formal review by technical experts that examine the quality of a work product and identify  
discrepancies from specifications and standards.

> **walkthrough** - A type of review in which an author leads members of the review through a work product and the  
members ask questions and make comments about possible issues.

### Static analysis by tools 

From Section 3.3, you should understand the objective of static analysis and be able to compare it to static and  
dynamic testing. You should be able to describe the main features of static analysis and recall typical defects that  
can be found using static analysis. Finally, you should be able to recall the benefits of using static analysis. You  
should now the glossary terms **compiler**, **cyclomatic complexity**, **control flow**, **data flow** and  
**static analysis**.

> **cyclomatic complexity** - The maximum number of linear, independent paths through a program.

> **control flow analysis** - A type of static analysis based on a representation of unique paths for executing  
a component or system.

> **data flow analysis** - A type of static analysis based on the lifecycle of variables.

> **static analysis** - The process of evaluating a component or system without executing it, based on its form,  
structure, content, or documentation.

### SAMPLE EXAM QUESTIONS

1) Which of the following artifacts can be examined by using review techniques?

1. Software code
1. Requirements specification
1. Test designs
1. All of the above
    <details><summary>Answer:</summary>4</details></br>

2) Which statement about the function of a static analysis tool is true?

1. Gives quality information about the code without executing it.
1. Checks expected results against actual results.
1. Can detect memory leaks.
1. Gives information about what code has and has not been exercised. 
    <details><summary>Answer:</summary>1</details></br>

3) Which is not a type of review?

1. Walkthrough
1. Inspection
1. Informal review
1. Management approval
    <details><summary>Answer:</summary>4</details></br>

4) What statement about reviews is true?

1. Inspections are led by a trained moderator, whereas technical reviews are not necessarily.
1. Technical reviews are led by a trained leader, inspections are not.
1. In a walkthrough, the author does not attend.
1. Participants for a walkthrough always need to be thoroughly trained. 
    <details><summary>Answer:</summary>1</details></br>

5) What is the main difference between a walkthrough and an inspection?

1. An inspection is led by the authors, whilst a walk through is led by a trained moderator.
1. An inspection has a trained leader, whilst a walk through has no leader.
1. Authors are not present during inspections, whilst they are during walkthroughs.
1. A walkthrough is led by the author, whilst an inspection is led by a trained moderator. 
    <details><summary>Answer:</summary>4</details></br>

6) Which of the following characteristics and types of review processes belong together?

1. Led by the author
2. Undocumented
3. No management participation
4. Led by a trained moderator or leader
5. Uses entry and exit criteria

- (s) Inspection
- (t) Technical review
- (u) Informal review
- (v) Walkthrough

1. s = 4, t = 3, u = 2 and 5, v = 1
1. s = 4 and 5, t = 3, u = 2, v = 1
1. s = 1 and 5, t = 3, u = 2, v = 4
1. s = 5, t = 4, u = 3, v = 1 and 2 
    <details><summary>Answer:</summary>2</details></br>

7) What statement about static analysis is true?

1. With static analysis, defects can be found that are difficult to find with dynamic testing.
1. Compiling is not a form of static analysis.
1. When properly performed, static analysis makes functional testing redundant.
1. Static analysis finds all faults. 
    <details><summary>Answer:</summary>1</details></br>

8) Which of the following statements about early test design are true and which are false?

1. Defects found during early test design are more expensive to fix.
2. Early test design can find defects.
3. Early test design can cause changes to the requirements.
4. Early test design takes more effort.

1. 1 and 3 are true. 2 and 4 are false.
1. 2 is true. 1, 3 and 4 are false.
1. 2 and 3 are true. 1 and 4 are false.
1. 2, 3 and 4 are true. 1 is false. 
    <details><summary>Answer:</summary>3</details></br>

9) Static code analysis typically identifies all but one of the following problems. Which is it?

1. Unreachable code
1. Undeclared variables
1. Faults in the requirements
1. Too few comments 
    <details><summary>Answer:</summary>3</details></br>


## Chapter 4 - Test design techniques

### Identifying test conditions and designing test cases

From Section 4.1, you should now be able to differentiate between a test condition, a test case and a test procedure,  
and know that they are documented in a test design specification, a test case specification and a test procedure  
specification respectively. You should be able to write test cases that include expected results and that show clear  
traceability to the test basis (e.g. requirements). You should be able to translate test cases into a test procedure  
specification at the appropriate level of detail for testers and you should be able to write a test execution schedule  
for a given set of test cases that takes into account priorities as well as technical and logical dependencies. You  
should know the glossary terms **test case**, **test case specification**, **test condition**, **test data**,  
**test procedure specification**, **test script** and **traceability**.

> **test case** - A set of preconditions, inputs, actions (where applicable), expected results and postconditions,  
developed based on test conditions.

> **test specification** -The complete documentation of the test design, test cases, and test scripts for a specific  
test item.

> **test condition** - A testable aspect of a component or system identified as a basis for testing.

> **test data** - Data needed for test execution.

> **test procedure** - A sequence of test cases in execution order and any associated actions that may be required to  
set up the initial preconditions and any wrap-up activities after execution.

> **test script** - A sequence of instructions for the execution of a test.

> **traceability** - The ability to establish explicit relationships between related work products or items within  
work products.

### Categories of test design techniques 

From Section 4.2 (categories of test design techniques), you should be able to give reasons why both specification-based (black-box) and structure-based (white-box) approaches are useful, and list the common techniques   
for each of these approaches. You should be able to explain the characteristics and differences between  
specification-based, structure-based and experience-based techniques. You should know the glossary terms  
**black-box test design techniques**, **experience-based test design techniques**,  
**specification-based test design techniques**, **structure-based test design techniques** and   
**white-box test design techniques**.

> **black-box test technique** - A test technique based on the specification of a component or system.

> **experience-based test technique** - A test technique based on the tester's experience, knowledge and intuition.

> **white-box test technique** - A test technique based on the internal structure of a component or system.

### Specification-based or black-box techniques

From Section 4.3, you should be able to write test cases from given software models using equivalence partitioning,  
boundary value analysis, decision tables and state transition diagrams. You should understand the main purpose of each  
of these four techniques, what level and type of testing could use each technique and how coverage can be measured for  
each of them. You should also understand the concept and benefits of use case testing. You should know the glossary  
terms **boundary value analysis**, **decision table testing**, **equivalence partitioning**,   
**state transition testing** and **use case testing**.

> **boundary value analysis** - A black-box test technique in which test cases are designed based on boundary values.

> **decision table testing** - A black-box test technique in which test cases are designed to exercise the   
combinations of conditions and the resulting actions shown in a decision table.

> **equivalence partitioning** - A black-box test technique in which test conditions are equivalence partitions  
exercised by one representative member of each partition.

> **state transition testing** - A black-box test technique in which test cases are designed to exercise elements of  
a state transition model.

> **use case testing** - A black-box test technique in which test cases are designed to exercise use case behaviors.

### Structure-based or white-box techniques

From Section 4.4, you should be able to describe the concept and importance of code coverage. You should be able to  
explain the concepts of statement and decision coverage and understand that these concepts can also be used at test  
levels other than component testing (such as business procedures at system test level). You should be able to write  
test cases from given control flows using statement testing and decision testing, and you should be able to assess  
statement and decision coverage for completeness. You should know the glossary terms **code coverage**,  
**decision coverage**, **statement coverage**, **structural testing**, **structure-based testing**  
and **white-box testing**.

> **decision coverage** - The coverage of decision outcomes.

> **statement coverage** - The coverage of executable statements.

> **white-box testing** - Testing based on an analysis of the internal structure of the component or system.

> **white-box test technique** - A test technique based on the internal structure of a component or system.

### Experience-based techniques

From Section 4.5, you should be able to remember the reasons for writing test cases based on intuition, experience and  
knowledge about common defects and you should be able to compare experience-based techniques with specification-based  
techniques. You should know the glossary terms **error guessing** and **exploratory testing**.

> **error guessing** - A test technique in which tests are derived on the basis of the tester's knowledge of past  
failures, or general knowledge of failure modes.

> **exploratory testing** - An approach to testing in which the testers dynamically design and execute tests based on  
their knowledge, exploration of the test item and the results of previous tests.

### Choosing a test technique

From Section 4.6, you should be able to list the factors that influence the selection of the appropriate test design  
technique for a particular type of problem, such as the type of system, risk, customer requirements, models for use  
case modeling, requirements models or testing knowledge. 


### SAMPLE EXAM QUESTIONS

1) In which document described in IEEE 829 would you find instructions for the steps to be
taken for a test including set-up, logging, environment and measurement?

1. Test plan
1. Test design specification
1. Test case specification
1. Test procedure specification
    <details><summary>Answer:</summary>D</details></br>

2) With a highly experienced tester with a good business background, which approach to defining test  
procedures would be effective and most efficient for a project under severe time pressure?

1. A high-level outline of the test conditions and general steps to take.
1. Every step in the test spelled out in detail.
1. A high-level outline of the test conditions with the steps to take discussed in detail with another experienced tester.
1. Detailed documentation of all test cases and careful records of each step taken in the testing
    <details><summary>Answer:</summary>A</details></br>


3) Put the test cases that implement the following test conditions into the best order for the test execution   
schedule, for a test that is checking modifications of customers on a database.

1. Print modified customer record.
2. Change customer address: house number and street name.
3. Capture and print the on-screen error message.
4. Change customer address: postal code.
5. Confirm existing customer is on the database by opening that record.
6. Close the customer record and close the database.
7. Try to add a new customer with no details at all.

- 5,4,2,1,3,7,6
- 4,2,5,1,6,7,3
- 5,4,2,1,7,3,6
- 5,1,2,3,4,7,6
    <details><summary>Answer:</summary>C</details></br>

4) Why are both specification-based and structure-based testing techniques useful?

1. They find different types of defect.
1. Using more techniques is always better.
1. Both find the same types of defect.
1. Because specifications tend to be unstructured.
    <details><summary>Answer:</summary>A</details></br>

5) What is a key characteristic of structure-based testing techniques?

a. They are mainly used to assess the structure of a specification.
b. They are used both to measure coverage and to design tests to increase coverage.
c. They are based on the skills and experience of the tester.
d. They use a formal or informal model of the software or component.
    <details><summary>Answer:</summary>B</details></br>

6) Which of the following would be an example of decision-table testing for a financial application  
applied at the system-test level?

1. A table containing rules for combinations of inputs to two fields on a screen.
1. A table containing rules for interfaces between components.
1. A table containing rules for mortgage applications.
1. A table containing rules for chess.
    <details><summary>Answer:</summary>C</details></br>

7) Which of the following could be a coverage measure for state transition testing?

- (V) All states have been reached.
- (W) The response time for each transaction is adequate.
- (X) Every transition has been exercised.
- (Y) All boundaries have been exercised.
- (Z) Specific sequences of transitions have been exercised.

1. X, Y and Z
1. V, X, Y and Z
1. W, X and Y
1. V, X and Z
    <details><summary>Answer:</summary>D</details></br>

8) Postal rates for 'light letters' are 25p up to l0g, 35p up to 50g plus an extra l0p for each  
additional 25g up to l00g. Which test inputs (in grams) would be selected using equivalence partitioning?

1. 8, 42, 82, 102
1. 4, 15, 65, 92, 159
1. 10, 50, 75, 100
1. 5, 20, 40, 60, 80
    <details><summary>Answer:</summary>B</details></br>

9) Which of the following could be used to assess the coverage achieved for   
specification-based (black-box) test techniques?

- (V) Decision outcomes exercised
- (W) Partitions exercised
- (X) Boundaries exercised
- (Y) State transitions exercised
- (Z) Statements exercised

1. V, W, Y or Z
1. W, X or Y
1. V, X or Z
1. W, X, Y or Z
    <details><summary>Answer:</summary>B</details></br>

10) Which of the following structurebased test design technique would be  
most likely to be applied to?

- (1) Boundaries between mortgage interest rate bands.
- (2) An invalid transition between two different arrears statuses.
- (3) The business process flow for mortgage approval.
- (4) Control flow of the program to calculate repayments.

1. 2, 3 and 4
1. 2 and 4
1. 3 and 4
1. 1, 2 and 3
    <details><summary>Answer:</summary>C</details></br>

11) Use case testing is useful for which of the following?

- (P) Designing acceptance tests with users or customers.
- (Q) Making sure that the mainstream business processes are tested.
- (R) Finding defects in the interaction between components.
- (S) Identifying the maximum and minimum values for every input field. 
- (T) Identifying thepercentage of statements exercised by a sets of tests.

1. P, Q and R
1. Q, S and T
1. P, Q and S
1. R, S and T
    <details><summary>Answer:</summary>A</details></br>

12) Which of the following statements about the relationship between statement coverage  
and decision coverage is correct?

1. 100% decision coverage is achieved if statement coverage is greater than 90%.
1. 100% statement coverage is achieved if decision coverage is greater than 90%.
1. 100% decision coverage always means 100% statement coverage.
1. 100% statement coverage always means 100% decision coverage.
    <details><summary>Answer:</summary>C</details></br>

13) If you are flying with an economy ticket, there is a possibility that you may get upgraded to business class,  
especially if you hold a gold card in the airline's frequent flier program. If you don't hold a gold card, there is  
a possibility that you will get 'bumped' off the flight if it is full and you check in late. This is shown in figure.  
Note that each box (i.e. statement) has been numbered. Three tests have been run:  

- (Test 1) : Gold card holder who gets upgraded to business class
- (Test 2) : Non-gold card holder who stays in economy
- (Test 3) : A person who is bumped from the flight

<p align="center">
    <img src="images/istqb-q13.png" width="35%"> 
</p>

What is the statement coverage of these three tests?

1. 60%
1. 70%
1. 80%
1. 90%
    <details><summary>Answer:</summary>C</details></br>

14) Why are error guessing and exploratory testing good to do?

1. They can find defects missed by specification-based and structure-based techniques.
1. They don't require any training to be as effective as formal techniques.
1. They can be used most effectively when there are good specifications.
1. They will ensure that all of the code or system is tested.
    <details><summary>Answer:</summary>A</details></br>

15) How do experience-based techniques differ from specification-based techniques?

1. They depend on the tester's understanding of the way the system is structured rather than on a
documented record of what the system should do.
1. They depend on having older testers rather than younger testers.
1. They depend on a documented record of what the system should do rather than on an individual's personal view.
1. They depend on an individual's personal view rather than on a documented record of what the system should do.
    <details><summary>Answer:</summary>D</details></br>

16) When choosing which technique to use in a given situation, which factors should be taken into account?

- (U) previous experience of types of defects found in this or similar systems
- (V) the existing knowledge of the testers
- (W) regulatory standards that apply
- (X) the type of test execution tool that will be used
- (Y) the documentation available
- (Z) previous experience in the development language

1. V, W, Y and Z
1. U, V, W and Y
1. U, X and Y
1. V, W and Y
    <details><summary>Answer:</summary>B</details></br>

17) Given the state diagram in Figure, which test case is the minimum series of valid transitions to cover every state?

<p align="center">
    <img src="images/istqb-q17.png" width="35%"> 
</p>

1. SS-S1-S2-S4-S1-S3-ES
2. SS-S1-S2-S3-S4-ES
3. SS-S1-S2-S4-S1-S3-S4-S1-S3-ES
4. SS-S1-S4-S2-S1-S3-ES
    <details><summary>Answer:</summary>A</details></br>

## Chapter 5 - Test management


### Test organization

From Section 5.1, you should now be able to explain the basic ideas of test organization. You should know why  
independent testing is important, but also be able to analyze the potential benefits and problems associated with  
independent test teams. You should recognize the types of people and skills needed in a test team and recall the   
tasks that a tester and a test leader will carry out. You should know the glossary terms **tester**, **test leader**  
and **test manager**.

> **tester** - A person who performs testing.

> **test leader** - On large projects, the person who reports to the test manager and is responsible for project  
management of a particular test level or a particular set of testing activities.

> **test manager** - The person responsible for project management of testing activities, resources, and evaluation  
of a test object.

### Test plans, estimates, and strategies

From Section 5.2, you should now understand the fundamentals of test planning and estimation. You should know the  
reasons for writing test plans and be able to explain how test plans relate to projects, test levels or phases, test  
targets and test execution. You should know which parts of the test process require special attention in test  
planning. You should be able to explain the justification behind various entry and exit criteria that might relate to  
projects, test levels or phases and test targets. You should be able to distinguish the purpose and content of test  
plans from that of test design specifications, test cases and test procedures, and know the IEEE 829 outline for a   
test plan. You should know the factors that affect the effort involved in testing, including especially test  
strategies  (approaches) and how they affect testing. You should be able to explain how metrics, expertise and  
negotiation are used for estimating. You should know the glossary terms **entry criteria**, **exit criteria**,  
**exploratory testing**, **test approach**, **test level**, **test plan**, **test procedure** and **test strategy**.

> **entry criteria** - The set of conditions for officially starting a defined task.

> **exit criteria** - The set of conditions for officially completing a defined task.

> **exploratory testing** - An approach to testing in which the testers dynamically design and execute tests based  
on their knowledge, exploration of the test item and the results of previous tests.

> **test approach** - test approach The manner of implementing testing tasks.  

> **test level** - A specific instantiation of a test process.

> **test plan** - Documentation describing the test objectives to be achieved and the means and the schedule  
for achieving them, organized to coordinate testing activities.

> **test procedure** - A sequence of test cases in execution order and any associated actions that may be required  
to set up the initial preconditions and any wrap-up activities after execution.

> **test strategy** - A description of how to perform testing to reach test objectives under given circumstances.

### Test progress monitoring and control

From Section 5.3, you should be able to explain the essentials of test progress monitoring and control. You should  
know the common metrics that are captured, logged and used for monitoring, as well as ways to present these metrics.  
You should be able to analyze, interpret and explain test metrics that can be useful for reporting test status and for  
making decisions about how to control test progress. You should be able to explain a typical test status report and   
know the IEEE 829 test summary report and test log. You should know the glossary terms **defect density**,   
**failure rate**, **test control**, **test coverage**, **test monitoring** and **test report**.

> **defect density** - The number of defects per unit size of a work product.

> **failure rate** - The ratio of the number of failures of a given category to a given unit of measure.

> **test control** - The activity that develops and applies corrective actions to get a test project on track when  
it deviates from what was planned.

> **test coverage** - The degree to which specified coverage items are exercised by a test suite, expressed  
as a percentage.

> **test monitoring** -The activity that checks the status of testing activities, identifies any variances from   
planned or expected, and reports status to stakeholders.

> **test report** - Documentation summarizing testing and results.

### Configuration management

From Section 5.4, you should now understand the basics of configuration management that relate to testing. You should be
able to summarize how good configuration management helps us do our testing work better. You should know the glossary terms **configuration management** and **version control**.

> **configuration management** -  A discipline applying technical and administrative direction and surveillance to  
identify and document the functional and physical characteristics of a configuration item, control changes to those  
characteristics, record and report change processing and implementation status, and verify that it complies with  
specified requirements.

### Risk and testing

From Section 5.5, you should now be able to explain how risk and testing relate. You should know that a risk is a  
potential undesirable or negative outcome and that most of the risks we are interested in relate to the achievement of  
project objectives. You should know about likelihood and impact as factors that determine the importance of a risk.  
You should be able to compare and contrast risks to the product (and its quality) and risks to the project itself  
and know typical risks to the product and project. You should be able to describe how to use risk analysis and risk  
management for testing and test planning. You should know the glossary terms **product risk**, **project risk**,  
**risk** and **risk-based testing**.

> **product risk** - A risk that impacts the quality of a product.

> **project risk** - A risk that impacts project success.

> **risk** - A factor that could result in future negative consequences.

> **risk-based testing** - A test approach in which the management, selection, prioritization, and use of test  
activities and resources are based on corresponding risk types and risk levels.

### Incident management

From Section 5.6, you should now understand incident logging and be able to use incident management on your projects.  
You should know the content of an incident report according to the IEEE 829 standard. You should be able to write a  
high-quality report based on test results and manage that report through its life cycle. You should know the glossary  
term **incident logging**.

### SAMPLE EXAM QUESTIONS

1) Why is independent testing important?

1. Independent testing is usually cheaper than testing your own work.
1. Independent testing is more effective at finding defects.
1. Independent testers should determine the processes and methodologies used.
1. Independent testers are dispassionate about whether the project succeeds or fails.
    <details><summary>Answer:</summary>2</details></br>

2) Which of the following is among the typical tasks of a test leader?

1. Develop system requirements, design specifications and usage models.
1. Handle all test automation duties.
1. Keep tests and test coverage hidden from programmers.
1. Gather and report test progress metrics.
    <details><summary>Answer:</summary>4</details></br>

3) According to the ISTQB Glossary, what do we mean when we call someone a test manager?

1. A test manager manages a collection of test leaders.
1. A test manager is the leader of a test team or teams.
1. A test manager gets paid more than a test leader.
1. A test manager reports to a test leader
    <details><summary>Answer:</summary>2</details></br>

4) What is the primary difference between the test plan, the test design specification,  
and the test procedure specification?

1. The test plan describes one or more levels of testing, the test design specification identifies the  
associated high-level test cases and a test procedure specification describes the actions for executing a test.
1. The test plan is for managers, the test design specification is for programmers and the test  
procedure specification is for testers who are automating tests.
1. The test plan is the least thorough, the test procedure specification is the most thorough and  
the test design specification is midway between the two.
1. The test plan is finished in the first third of the project, the test design specification is finished in  
the middle third of the project and the test procedure specification is finished in the last third of the project.
    <details><summary>Answer:</summary>1</details></br>

5) Which of the following factors is an influence on the test effort involved in most projects?

1. Geographical separation of tester and programmers.
1. The departure of the test manager during the project.
1. The quality of the information used to develop the tests.
1. Unexpected long-term illness by a member of the project team.
    <details><summary>Answer:</summary>3</details></br>

6) The ISTQB Foundation Syllabus establishes a fundamental test process where test planning occurs early in the  
project, while test execution occurs at the end. Which of the following elements of the test plan, while specified  
during test planning, is assessed during test execution?

1. Test tasks
1. Environmental needs
1. Exit criteria
1. Test team training
    <details><summary>Answer:</summary>3</details></br>

7) Consider the following exit criteria which might be found in a test plan:

- (I) No known customer-critical defects.
- (II) All interfaces between components tested.
- (III) 100% code coverage of all units.
- (IV) All specified requirements satisfied.
- (V) System functionality matches legacy system for all business rules.

Which of the following statements is true about whether these exit criteria belong  
in an acceptance test plan?

1. All statements belong in an acceptance test plan.
1. Only statement I belongs in an acceptance test plan.
1. Only statements I, II, and V belong in an acceptance test plan.
1. Only statements I, IV, and V belong in an acceptance test plan.
    <details><summary>Answer:</summary>4</details></br>

8) According to the ISTQB Glossary, what is a test level?

1. A group of test activities that are organized together.
1. One or more test design specification documents.
1. A test type.
1. An ISTQB certification.
    <details><summary>Answer:</summary>1</details></br>

9)  Which of the following metrics would be most useful to monitor during test execution?

1. Percentage of test cases written.
1. Number of test environments remaining to be configured.
1. Number of defects found and fixed.
1. Percentage of requirements for which a test has been written.
    <details><summary>Answer:</summary>3</details></br>

10) During test execution, the test manager describes the following situation to the project team: '90% of the test  
cases have been run. 20% of the test cases have identified defects. 127 defects have been found. 112 defects have  
been fixed and have passed confirmation testing. Of the remaining 15 defects, project management has decided that  
they do not need to be fixed prior to release.' Which of the following is the most reasonable interpretation of  
this test status report?

1. The remaining 15 defects should be confirmation tested prior to release.
1. The remaining 10% of test cases should be run prior to release.
1. The system is now ready for release with no further testing or development effort.
1. The programmers should focus their attention on fixing the remaining known defects prior to release
    <details><summary>Answer:</summary>2</details></br>

11) In a test summary report, the project's test leader makes the following statement,  
'The payment processing subsystem fails to accept payments from American Express cardholders, which is  
considered a must-work feature for this release.' This statement is likely to be found in which  
of the following sections?

1. Evaluation
1. Summary of activities
1. Variances
1. Incident description
    <details><summary>Answer:</summary>1</details></br>

12) During an early period of test execution, a defect is located, resolved and confirmed as resolved by re-testing,  
but is seen again later during subsequent test execution. Which of the following is a testing-related aspect of  
configuration management that is most likely to have broken down?

1. Traceability
1. Confirmation testing
1. Configuration control
1. Test documentation management
    <details><summary>Answer:</summary>3</details></br>

13) You are working as a tester on a project to develop a point-of-sales system for grocery stores and  
other similar retail outlets. Which of the following is a product risk for such a project?

1. The arrival of a more-reliable competing product on the market.
1. Delivery of an incomplete test release to the first cycle of system test.
1. An excessively high number of defect fixes fail during re-testing.
1. Failure to accept allowed credit cards
    <details><summary>Answer:</summary>4</details></br>

14) A product risk analysis meeting is held during the project planning period.   
Which of the following determines the level of risk?

1. Difficulty of fixing related problems in code
1. The harm that might result to the user
1. The price for which the software is sold
1. The technical staff in the meeting
    <details><summary>Answer:</summary>2</details></br>

15) You are writing a test plan using the IEEE 829 template and are currently completing  
the Risks and Contingencies section. Which of the following is most likely to be listed as a project risk?

1. Unexpected illness of a key team member
1. Excessively slow transaction-processing time
1. Data corruption under network congestion
1. Failure to handle a key use case
    <details><summary>Answer:</summary>1</details></br>

16) You and the project stakeholders develop a list of product risks and project risks during the planning stage of a project. What else should you do with those lists of risks during test planning?

1. Determine the extent of testing required for the product risks and the mitigation and contingency  
actions required for the project risks.
1. Obtain the resources needed to completely cover each product risk with tests and transfer  
responsibility for the project risks to the project manager.
1. Execute sufficient tests for the product risks, based on the likelihood and impact of each product  
risk and execute mitigation actions for all project risks.
1. No further risk management action is required at the test planning stage.
    <details><summary>Answer:</summary>1</details></br>

17) According to the ISTQB Glossary, a product risk is related to which of the following?

1. Control of the test project
1. The test object
1. A single test item
1. A potential negative outcome
    <details><summary>Answer:</summary>2</details></br>

18) In an incident report, the tester makes the following statement, At this point, I expect to receive an error  
message explaining the rejection of this invalid input and asking me to enter a valid input. Instead the system   
accepts the input, displays an hourglass for between one and five seconds and finally terminates abnormally, giving   
the message, "Unexpected data type: 15. Click to continue." ' This statement is likely to be found in which of the  
following sections of an IEEE 829 standard incident report?

1. Summary
1. Impact
1. Item pass/fail criteria
1. Incident description
    <details><summary>Answer:</summary>4</details></br>

19) According to the ISTQB Glossary, what do we call a document that describes any event that occurred during  
testing which requires further investigation?

1. A bug report
1. A defect report
1. An incident report
1. A test summary report
    <details><summary>Answer:</summary>3</details></br>

20) A product risk analysis is performed during the planning stage of the test process. During the execution stage  
of the test process, the test manager directs the testers to classify each defect report by the known product risk  
it relates to (or to 'other'). Once a week, the test manager runs a report that shows the percentage of defects  
related to each known product risk and to unknown risks. What is one possible use of such a report?

1. To identify new risks to system quality.
1. To locate defect clusters in product subsystems.
1. To check risk coverage by tests.
1. To measure exploratory testing
    <details><summary>Answer:</summary>1</details></br>
    
## Chapter 6 - Tool support for testing

### Types of test tool

From Section 6.1, you should now be able to classify different types of test tools according to the test process  
activities that they support. You should also recognize the tools that may help developers in their testing   
(shown by '(D)' below). In addition to the list below, you should recognize that there are tools that support   
specific application areas and that general-purpose tools can also be used to support testing. The tools you   
should now recognize are:

Tools that support the management of testing and tests:
- test management tool;
- requirements management tool;
- incident management tool;
- configuration management tool.

Tools that support static testing:
- review process support tool;
- static analysis tool (D);
- modeling tool (D).

Tools that support test specification:
- test design tool;
- test data preparation tool.

Tools that support test execution and logging:
- test execution tool;
- test harness and unit test framework tool (D);
- test comparator;
- coverage measurement tool (D);
- security tool.

Tools that support performance and monitoring:
- dynamic analysis tool;
- performance-testing, load-testing and stress-testing tool;
- monitoring tool.

In addition to the tools already listed, you should know the glossary terms
**debugging tool**, **driver**, **probe effect** and **stub**.

> **debugging** - The process of finding, analyzing and removing the causes of failures in a component or system.

> **driver** -A component or tool that temporarily replaces another component and controls or calls a test item  
in isolation.

> **stub** - A type of test double providing predefined responses.

### Effective use of tools: Potential benefits and risks

From Section 6.2, you should be able to summarize the potential benefits and potential risks of tool support for  
testing in general. You should recognize that some tools have special considerations, including test execution tools,  
performance-testing tools, static analysis tools and test management tools. You should know the glossary terms  
**data-driven testing**, **keyword-driven testing** and **scripting language** and recognize these as associated with  
test execution tools.

> **data-driven testing** -A scripting technique that uses data files to contain the test data and expected results  
needed to execute the test scripts.

> **keyword-driven testing** - A scripting technique in which test scripts contain high-level keywords and supporting  
files that contain low-level scripts that implement those keywords.

### Introducing a tool into an organization

From Section 6.3, you should be able to state the main principles of introducing a tool into an organization   
(e.g. assessing organizational maturity, clear requirements and objective criteria, proof-of-concept, vendor  
evaluation, coaching and mentoring). You should be able to state the goals of a proof-ofconcept or piloting phase for  
tool evaluation (e.g. learn about the tool, assess fit with current practices, decide on standards, assess benefits).  
You should recognize that simply acquiring a tool is not the only factor in achieving good tool support; there are   
many other factors that are important for success (e.g. incremental roll-out, adapting processes, training and  
coaching, defining usage guidelines, learning lessons and monitoring benefits). There are no specific definitions   
for this section.

### SAMPLE EXAM QUESTIONS

1) Which tools help to support static testing?

1. Static analysis tools and test execution tools.
1. Review process support tools, static analysis tools and coverage measurement tools.
1. Dynamic analysis tools and modeling tools.
1. Review process support tools, static analysis tools and modeling tools.
    <details><summary>Answer:</summary>4</details></br>

2) Which test activities are supported by test harness or unit test framework tools?

1. Test management and control.
1. Test specification and design.
1. Test execution and logging.
1. Performance and monitoring.
    <details><summary>Answer:</summary>3</details></br>

3) What are the potential benefits from using tools in general to support testing?

1. Greater quality of code, reduction in the number of testers needed, better objectives for testing.
1. Greater repeatability of tests, reduction in repetitive work, objective assessment.
1. Greater responsiveness of users, reduction of tests run, objectives not necessary.
1. Greater quality of code, reduction in paperwork, fewer objections to the tests.
    <details><summary>Answer:</summary>2</details></br>

4) What is a potential risk in using tools to support testing?

1. Unrealistic expectations, expecting the tool to do too much.
1. Insufficient reliance on the tool, i.e. still doing manual testing when a test execution tool has been purchased.
1. The tool may find defects that aren't there.
1. The tool will repeat exactly the same thing it did the previous time.
    <details><summary>Answer:</summary>1</details></br>

5) Which of the following are advanced scripting techniques for test execution tools?

1. Data-driven and keyword-driven
1. Data-driven and capture-driven
1. Capture-driven and keyhole-driven
1. Playback-driven and keyword-driven
    <details><summary>Answer:</summary>1</details></br>

6) Which of the following would NOT be done as part of selecting a tool for an organization?

1. Assess organizational maturity, strengths and weaknesses.
1. Roll out the tool to as many users as possible within the organization.
1. Evaluate the tool features against clear requirements and objective criteria.
1. Identify internal requirements for coaching and mentoring in the use of the tool.
    <details><summary>Answer:</summary>2</details></br>

7) Which of the following is a goal for a proof-of-concept or pilot phase for tool evaluation?

1. Decide which tool to acquire.
1. Decide on the main objectives and requirements for this type of tool.
1. Evaluate the tool vendor including training, support and commercial aspects.
1. Decide on standard ways of using, managing, storing and maintaining the tool and the test assets.
    <details><summary>Answer:</summary>4</details></br>


## References
- https://github.com/jalizadeh/ISTQB-Exam-Questions
- https://glossary.istqb.org/en_US/search?term=&exact_matches_first=true
- https://www.softwaretestinggenius.com/manual-testing/quality-systems/software-testing-skill-test/
- https://www.softwaretestinggenius.com/certifications-resources/istqb-foundation-exam-sample-question-papers/
