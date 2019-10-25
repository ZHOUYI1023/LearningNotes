# Bad C++ Software Problems
## 1. Cyclic Dependencies

## 2. Excessive Link-Time Dependencies  

## 3. Excessive Compile-Time Dependencies
This dominate the development time for large project.
## 4. The Global Name Space
for example, if you use a typedefine in global without implicitly imply the meaning of the new type, it would be hard to understand your code. To fix it, try typedef within a class. Then, when you call it, you will use class::typename, it will be much easier to find the definition of type. Besides that, it can minimize the likelihood of collision.
## 5. Logical vs Physical Design
Layering