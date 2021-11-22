# public，private，protected的区别，继承方法与访问权限

## 公共public，私有private与受保护protected的修饰符

一般来说，在TypeScript里，成员都*默认为public*。

我们可以把上面的例子写成这样：

```ts
class Greeter {
    public greeting: string;
    public constructor(message: string) {
        this.greeting = message;
    }
    public greet() {
        return "Hello, " + this.greeting;
    }
}

let greeter = new Greeter("world");
```

*当成员被标记成 private时，它就不能在声明它的类的外部访问。*

```ts
class Greeter {
    private greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
}
new Greeter('abc').greeting; // 错误：'greeting'是私有的。
```

protected修饰符与private修饰符的行为很相似，但有一点不同，*protected成员在派生类中仍然可以访问。* 例如：

```ts
class Person {
    protected name: string;
    constructor(name: string) { this.name = name; }
}

class Employee extends Person {
    private department: string;

    constructor(name: string, department: string) {
        super(name)
        this.department = department;
    }

    public getElevatorPitch() {
        return `Hello, my name is ${this.name} and I work in ${this.department}.`;
    }
}

let howard = new Employee("Howard", "Sales");
console.log(howard.getElevatorPitch());
console.log(howard.name); // 错误
```

