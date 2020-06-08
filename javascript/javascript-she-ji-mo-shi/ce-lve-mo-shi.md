# 策略模式

## 策略模式

代码中常见需要分情况选择的需求，如奖金分级，在为s级执行某操作，为a级执行某操作，为b级执行某操作。若使用if判断的话，判断次数较少的情况可接受，若判断次数多的话，不必要的比较就会增加消耗。减少比较次数是优化的重点。

首先想到的是使用函数。针对每一级都创建一个函数来操作。则将需进行的操作（假设为工资翻倍）与奖金分级的操作分离。奖金分类使用类来实现。代码如下：

奖金计算：

```text
var performanceS = function(){}
performanceS.prototype.calculate = function(salary){
    return salary*4;
}
var performanceA = function(){}
performanceA.prototype.calculate = function(salary){
    return salary*3;
}
var performanceB = function(){}
performanceB.prototype.calculate = function(salary){
    return salary*2;
}
```

奖金分类：

```text
var Bonus = function(){
    this.salary = null;
    this.strategy = null;
}
​
Bonus.prototype.setSalary = function(salary){
    this.salary = salary;
}
​
Bonus.prototype.setStrategy = function(salary){
    this.strategy = strategy;
}
​
Bonus.prototype.getBonus = function(){
    return this.strategy.calculate(this.salary);
}
​
```

