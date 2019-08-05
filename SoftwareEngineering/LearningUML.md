UML: Unified Modelling Language

各种UML图从多视角考察一个系统，目的是和每一类stakeholder良好地沟通

### 第二章 理解面向对象
对象是一个类的实例

### 类图
``` plantuml
@startuml
class WashingMachine {
  String brandName
  String ModelName
  Int serialName
  Int capacity
  void acceptClothes()
}
object myWasher{

myWasher : name = "Dummy"
myWasher : id = 123
}
@enduml
```
### 对象图
``` plantuml

object user {
  name = "Dummy"
  id = 123
}

```