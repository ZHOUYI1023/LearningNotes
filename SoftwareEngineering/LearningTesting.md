#Verification & Validation
[Website](https://www.softwaretestingclass.com/difference-between-verification-and-validation/)
Verification|Validation
-----|-----
Are we building the system right?| Are we building the right system?
==within a development phase== |==at the end of the development process== 
The objective of Verification is to make sure that the product being ==develop is as per the requirements and design specifications.==|The objective of Validation is to make sure that the product ==actually meet up the user’s requirements==, and check whether the specifications were correct in the first place.
Following activities are involved in Verification: Reviews, Meetings and Inspections.|Following activities are involved in Validation: Testing like black box testing, white box testing, gray box testing etc.
Verification is carried out by ==QA team== to check whether implementation software is as per specification document or not.|Validation is carried out by ==testing team.==
Following items are evaluated during Verification: Plans, Requirement Specifications, Design Specifications, Code, Test Cases etc.|Following item is evaluated during Validation: Actual product or Software under test.
---
# Monitoring Cyclomatic Complexity
[Website](https://www.ibm.com/developerworks/java/library/j-cq03316/?S_TACT=105AGX52&S_CMP=cn-a-j)

## Behavior-driven development
* BDD isn't anything new or revolutionary. It's just an evolutionary offshoot of TDD in which the word "test" is replaced by the word "should. 
* With BDD, you don't have to think about tests, you can just pay attention to the requirements of your application and ensure that the application behavior does what it should to meet those requirements.

## Be aware of the tight couple
* keeping an eye on maintainability
* In a loosely coupled system, components are interrelated using abstractions instead of implementations.
* This abstraction of implementation details is key to flexibility: it enables you to swap out the implementation type completely without affecting the GUI. 

## Don't be fooled by the coverage report
* High coverage percentages alone do not ensure the quality of your code. Highly covered code isn't necessarily free of defects, although it's certainly less likely to contain them.
* The trick to test coverage measurement is to use the coverage report to expose code that hasn't been tested, such as to estimate the time needed for a project, continuously monitor code quality, and facilitate QA collaboration.

## Monitoring cyclomatic complexity
* 软件源码某部分的圈复杂度就是这部分代码中线性无关路径的数量
* Cyclomatic complexity precisely measures path complexity
* methods having a cyclomatic complexity (or CC) greater than 10 have a higher risk of defects
* Because CC represents the paths through a method, this is an excellent number for determining how many test cases will be required to reach 100 percent coverage of a method.
* When faced with a report indicating high cyclomatic complexity values, the first course of action is to verify the existence of any corresponding tests. If there are any tests, how many are there?
* If there aren't any associated test cases, you obviously need to test the method. The most effective way to reduce cyclomatic complexity is to pull out portions of code and place them into new methods. This pushes the complexity into smaller, more manageable (and therefore more testable) methods. Of course, you should then test those smaller methods. 
*  If a method's CC value keeps growing, you have a couple of response options:
    * Ensure a healthy amount of related tests are present to reduce risk.
    * Evaluate the possibility of refactoring the method to reduce any long-term maintenance issues. 
* Because cyclomatic complexity is such a good indicator of code complexity, there is a strong relationship between test-driven development and low CC values. When tests are written often (note, I'm not implying first), developers have the tendency to write uncomplicated code because complicated code is hard to test.

## Test Categorization
### Unit Test
* A unit test verifies an object or multiple objects in isolation
### Component Test
* component tests deal with multiple layers of an architecture, they often deal with databases, file systems, network elements
### System Test
* System tests verify a software application end-to-end. 
* System tests are very similar to functional tests. The difference is that they don't emulate a user, they mimic one. 

### Acceptance Test
* Acceptance tests are similar to functional tests, the difference being that, ideally, customers or end users write them. Just like functional tests, acceptance tests test as an end user would. 