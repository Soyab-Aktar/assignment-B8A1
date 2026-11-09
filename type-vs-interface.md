# Interface and Type Alias in TypeScript

## Introduction

Typescript allows developers to define the shape of data using `type` aliases and `interface` statements. Although they appear similar especially in object properties declarations and definition, there are many differences between them that will help maintain the clarity of codebase.

## Details

Interface defines the contract of objects that can be extended using the `extends` keyword and merge declarations if there are several statements with the same name.

``` ts
interface User {
  id: number;
  name: string;
}

interface User {
  email: string; // Merged declaration adds this property.
}

interface Admin extends User {
  permissions: string[];
}
```

A `type` alias describes a value not limited to the objects. `Type` allows to define primitives, union types, intersection, tuple and function types.

``` ts
type Status = "active" | "inactive";
type Coordinates = [number, number];

type Account = {
  id: number;
  name: string;
};

type AdminAccount = Account & {
  permissions: string[];
};
```

`Interface` doesn't support reopening a type definition via declaration merging. Both `types` and `interfaces` allow to compose objects, but unions, such as `string` | `number` only possible in `type` definition. `Interface` allows to easily define publicly accessible object structures and contracts that can be extended by other developers. On the other hand, `type` is more flexible because it supports unions, intersections, tuples, primitive `types`, and other complex `type` expressions.

## Conclusion

Choose `interface` when defining object structures that may need to be extended or implemented by `classes`. Choose `type` when working with unions, intersections, or other complex `type` definitions. For ordinary object structures, both are valid choices, so maintaining consistency throughout the project is important.