# js原型链

标签（空格分隔）： 未分类

---

原型对象
----

    function Person () {
        this.name = 'John';
    }
    var person = new Person ();
    Person.prototype.say = function () {
        console.log('Hello,' + this.name);
    };
    person.say();//Hello,John

Person原型对象定义了公共的方法————say，虽然定义方法的操作是在构造实例以后出现，但由于是原型方法————在调用之前已经声明。因此之后的每一个实例都将拥有该方法。

原型对象的作用：为每个实例对象存储共享的方法和属性，原型对象只是一个普通的对象，所有的实例共享同一个原型对象，原型对象只有一个，所以：

    person.say = new person().say

在js中，对象调用一个方法的时候，首先会在自身的方法里寻找，若没有找到，则会去原型链上一层一层往上找，这里的原型链就是实例对象的
`__proto__`属性

详解：

    function Person(){
        this.name = 'John';
    }
    var person = new Person();
    Person.prototype = {
        say : function() {
            console.log('Hello,' + this.name);    
        }
    };
    Person.say();//Person.say() is not a function
    
这种创建方法是在添加原型方法之前构造实例对象，这样操作会造成一个问题：
当var Person = new Person();的时候，person.prototype指向了一个空对象：Person {}。而对于实例Person而言，其内部有一个原型链指针proto，该指针指向了Person.prototype指向的对象：{},然后重置了Person的原型对象，使其指向了另外一个对象：Object {say : function}。
这时Person.proto的指向还是没有变：{},没有say()方法，所以报错。

修改：
交换构造对象和重置原型对象的顺序。

    function Person(){
        this.name = 'John';
    }
    Person.prottype = {
        say : function() {
            console.log('Hello,' + this.name);
        }
    };
    var Person = new Person();
    Person.say();
    
原型对象的结构：

    function.prototype = {
        construct : function,
        __proto__ :　parent prototype,
        some prototype properties...
    }
    
小结：
    函数的原型对象construct默认指向函数本身，原型对象除了有原型属性外，还有一个原型链指针`__proto__`，该指针指向上一级的原型对象，上一层的原型对象结构也是如此，这样就能利用`__proto__`实现类似继承的功能，一直指向Object的原型对象上，而原型对象用`Object.prototype.__proto__ = null`表示原型链的最顶端。这就是javascript的原型链继承，也是所有的javascript对象都具有Object的基本方法的原因。