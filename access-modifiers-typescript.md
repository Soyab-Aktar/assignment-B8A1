# Access modifiers for TypeScript OOP

## Introduction

TypeScript has access modifiers that specify how class members can
be accessed. They allow defining the public interface of classes,
enclosing their implementation, and creating more maintainable object-
oriented programs. TypeScript has `public`, `private`, and `protected`;
the related property modifier `readonly` can prevent its later reassigning.

## Detailed explanation

The `public` access modifier makes class members accessible from
anywhere in the program. It is the default visibility modifier and does
not need to be declared explicitly.

```ts
class User {
  public name: string;

  constructor(name: string) {
    this.name = name;
  }
}

const user = new User("Asha");
console.log(user.name); // Allowed
```

The `protected` access modifier allows class members to be accessed within the class where they are declared and its subclasses (child classes). However, these members cannot be accessed directly through an instance of the class from outside.

```ts
class Employee {
  protected department: string = "Engineering";

  public showDepartment(): void {
    console.log(this.department); // Allowed
  }
}

class Manager extends Employee {
  public displayDepartment(): void {
    console.log(this.department); // Allowed (inherited)
  }
}

const employee = new Employee();
employee.showDepartment(); // Allowed

// employee.department; // Error: protected member

const manager = new Manager();
manager.displayDepartment(); // Allowed
// manager.department; // Error: protected member
```

The `private` access modifier makes class members visible only inside
the declaring class itself. The `protected` access modifier is similar
to `private`, allowing accessing the property inside a class and any
of its subclasses. Ordinary instances cannot access `protected`
members.

```ts
class Employee {
  private salary = 30000;
  protected department = "Engineering";

  public getSalary(): number {
    return this.salary;
  }
}

class Manager extends Employee {
  public describe(): string {
    return this.department; // Allowed
    // return this.salary;  // Error: private member
  }
}
```

The `readonly` modifier allows initializing the property when it is
declared or initialized in the constructor, but prevents later
reassignment.

``` ts
class Product {
  constructor(
    public readonly id: number,
    public name: string
  ) {}
}

const product = new Product(101, "Keyboard");
product.name = "Mouse"; // Allowed
// product.id = 102;     // Error: readonly
```


## Conclusion

Use `public` for intended external operations, `private` for class
internals, `protected` for members shared with subclasses, and
`readonly` for values that should not be reassigned after
initialization. Thoughtful access control creates safer, clearer class
designs.
