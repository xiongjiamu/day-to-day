### 前言  
日常js面试题积累汇总。实时更新！

### 1.JavaScript的基本数据类型  

<details><summary><b></b></summary>
<p>

#### 答案:   
`Number`、`String`、`Boolean`、`Null`、`Undefined`、`Symbel`（ES6新增）  
Object是JavaScript中所有对象的父对象  
数据封装类对象：`Object`、`Array`、`Boolean`、`Number`、和`String`  
其他对象：`Function`、`Arguments`、`Math`、`Date`、`RegExp`、`Error`  
</p>
</details>  

***

### 2.JavaScript的引用类型  

<details><summary><b></b></summary>
<p>

#### 答案:   
* `Object ` 
* `Function`  
* `Array`  
</p>
</details>  

***

### 3.Javascript基本数据类型和引用类型的特点  

<details><summary><b></b></summary>
<p>

#### 答案:   
1.基本数据类型：值不可变；数据存放在栈区。  
2.引用数据类型：值是可变的；同时保存在栈内存和堆内存。
</p>
</details>  

***

### 4.检验JavaScript的数据类型的方法有哪些，以及使用它们的缺点  

<details><summary><b></b></summary>
<p>

#### 答案:   
* 1.`typeof`：不能判断null和区分Array/Date/RegExp  
* 2.`instanceof`：无法检测null和undefined；未必准确（是否处于处于原型链上的方法不准确）；无法判断字面量方式创建的基本数据类型；    
* 3.`constructor`：无法检测null和undefined；未必准确
* 4.`Object.prototype.toString.call()`：无；全能方法；  
</p>
</details>  

***

### 5.JavaScript基本数据类型和非基本数据类型的区别  

<details><summary><b></b></summary>
<p>

#### 答案:   
* 1.目前JS中有6种基本数据类型：`Undefined`、`Null`、`Boolean`、`Number`、`String`和`Symbel`（ES6新增）。还有一种复杂数据类型----`Object`,`Object`本质上是由一组无序的名值对组成的，`Object`、`Fuction`、`Array`则属于引用类型。  
* 2.基本数据类型是不可变的，而非基本数据类型是可变的。 
* 3.基本数据类型是不可变的，因为一旦它们创建就无法更改。但是非基本数据类型可更改，意味着一旦创建对象，就可以更改它。  
* 4.将基本数据类型与其值进行比较，这意味着如果两个值具有相同的数据类型，并具有相同的值，那么它们是严格相等的。  
* 5.非基本数据类型不与值进行比较。例如，如果两个对象具有相同的属性和值，则它们严格不相等。 
</p>
</details>  

***  

### 6.instanceof操作符  

<details><summary><b></b></summary>
<p>

#### 答案:   
判断对象属于某一个类，回去查找对象的constructor的prototype
</p>
</details>  

***  

### 7.new操作符的作用  

<details><summary><b></b></summary>
<p>

#### 答案:   
* 新生了一个对象  
* 链接到原型  
* 绑定this  
* 返回对象  

```javascript
function newCreate(){
  // 创建一个空白对象
  let obj = new Object();
  // 获得构造函数
  let Con = [].shift.call(arguments);
  // 链接到原型
  obj.__proto__ = Con.prototype; 
  // 绑定this,执行构造函数
  let result = Con.apply(obj,arguments);
  // 确保new出来的是个对象
  return typeof result === 'object' ? result : obj;
}
```
</p>
</details>  

***  

### 8.作用域和作用域链  

<details><summary><b></b></summary>
<p>

#### 答案:   
[静态作用域与动态作用域](https://github.com/yihan12/day-to-day/blob/master/202101/%E8%AF%8D%E6%B3%95%E4%BD%9C%E7%94%A8%E5%9F%9F%E5%92%8C%E5%8A%A8%E6%80%81%E4%BD%9C%E7%94%A8%E5%9F%9F.md)  
#### 1.作用域  

* 种类：JS中有三种作用域，全局作用域，函数作用域，ES6新推出的块级作用域。  
* 概念：一个变量的可访问规则，在函数创建的时候就已经创建好作用域，整个JS文件执行有一个最外层的全局作用域（window）。  
* 使用：本作用域内部的所有变量都可以在本作用域内部访问，外部无法访问。内部可访问上级作用域变量，本作用域内部所使用的var声明的变量会有一个作用域提升的过程，let、const声明的变量没有变量提升。  

#### 2.作用域链  

* 一个变量的访问规则的链式操作  
* 可以把它理解成包含自身变量对象和上级变量对象的列表，可以通过[[Scope]]属性查找上级变量  
* 当访问一个变量时，现在本作用域内查找，如果没有，就回去上一级作用域查找，直到全局作用域window下面，都没有返回undefined  
</p>
</details>  

***  

### 9.闭包  

<details><summary><b></b></summary>
<p>

#### 答案:   
1.特点：  

* 内层作用域可以访问外层作用域的变量  
* 闭包就是可以读取其他函数内部变量的函数  
* 函数A返回一个函数B，并且函数B中使用了函数A的变量，函数B就称为闭包  
* 闭包函数引用的变量是存储在堆上的，所以说，当闭包函数弹出调用栈后，闭包返回的函数依然能够调用到闭包函数的变量  

2.优点  

* 使用闭包能够形成独立的空间，延长变量的生命周期，保存中间状态值  
* 可以封装一些私有变量，外部无法直接访问（例如用户登录状态计数器）创建立即执行函数（闭包）实现js模块化封装  
* 解决var声明的循环语句变量无法长久保存的问题  

3.缺点  

* 滥用闭包会导致内存泄漏，因为闭包中引用的包裹函数的变量都永远不会被释放，所以我们应该在必要的时候，及时释放这个闭包函数，将不再使用的闭包引用变量设置为null  
* 由于函数闭包的变量都保存在内存中，会导致内存消耗大  
</p>
</details>  
