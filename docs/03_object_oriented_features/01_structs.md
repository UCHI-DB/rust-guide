# Structs

[Link to Rust documentation for Struc & Impl ](https://doc.rust-lang.org/book/ch05-00-structs.html)

A ```struct```, or structure, is a data type in Rust that is composed of data items of different types, including other structures. A structure defines its data as a key-value pair.

## Declaring and Instantiating a ```struct```

To declare a structure, we use the keyword `struct` followed by the name of the structure. Then, inside the curly brackets, we define the names and types of the pieces of data. For example:

```rust
struct name_of_struct {
    field1: data_type,
    field2: data_type,
    field3: data_type
}
```

After declaring a ```struct```, we create an instance of that struct and specify concrete values for the fields and values. For example:

```rust
// declaring an employee structure
struct Employee {
    name: String,
    company: String, 
    age: u32,
    active: Boolean
}
//creating an instance of the struct
fn main() {
    let emp1 = Employee {
        name: String::from("Some Name"),
        company: String::from("Some Company"),
        age: 27,
        active: True
    };
}
```

In an instance, we define the ```key: value``` pairs, where the keys are the names of the fields and the values are the data we want to store in those fields. 

There is a common shorthand notation when initializing a struct that you can pass a variable with the same name as the member of the struct. 

```rust
let age = 27;
let active = true;
let emp1 = Employee {
        name: String::from("Some Name"),
        company: String::from("Some Company"),
        age,
        active
    };
```

To get a specified value from a struct, we can use dot notation. For example, if we wanted the employee's name, we would call
``` emp1.name ``` whenever we wanted to use this value.

To be able to modify an instance, the instance variable must be marked as mutable. A reminder on how to make your variables mutable is by adding ```mut``` in front of the variable name. If we want to modify a specific ``` key: value ``` pair, we would again use dot notation. For example, if we wanted to modify the company name of emp1, we would call:

``` 
emp1.company = String::from("Different Company");
```

after making the appropriate value mutable.
