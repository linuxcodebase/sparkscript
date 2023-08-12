# SparkScript

SparkScript is a modern programming language with a host of amazing features. Here are some of them to give you an overview of the language. It derives most of them from the excellent Swift language but also adds its own features on top.

---

## Hello World

```swift
print("Hello, World!")
```

---

## Implicit Main

This is one of SparkScript's most unique features. Any code *except* for functions and classes will be *automattically* put under a main function.

For example:

```swift
func myFunc(){
    print("Hello there")
}
myFunc()
```

will be automattically converted to

```swift
func myFunc(){
    print("Hello there")
}
func main(args: Array<String>){
    myFunc()
}  
```

`func main(args: Array<String>)` is the signature of the main function.

You can explicitly add a function inside the main using the `inmain` keyword:

```swift
inmain func greet(name: String){
    print("Hello, world!")
}
```

---

## Variables

`let` creates a variable that can be varied and modified.

`const` creates a variable that cannot be varied or modified in any way.

`mut` variables can me modified but not reassigned.

`var` variables can be reassigned but not modified.
You can interpolate variables using the `$variable` syntax.

For example:

```swift
let myVar = [1, 2, 3]
myVar = [1, 2, 4] //allowed
myvar[0] = 2 //allowed
```

```js
const myVar = [1, 2, 3]
myVar = [1, 2, 4] //not allowed
myvar[0] = 2 //not allowed
```

```rust
const mut myVar = [1, 2, 3]
myVar = [1, 2, 4] // not allowed
myvar[0] = 2 //allowed
```

```js
const var myVar = [1, 2, 3]
myVar = [1, 2, 4] //allowed
myvar[0] = 2 //not allowed
```

---

## Types

SparkScript is strongly typed. However, it also supports type inference.

```swift
let myVar: Array<string> = [1, 2, 4] //not allowed: TypeError
let myStr = "Hello"
myStr = 1 //not allowed: type inferred as String
```

All the types are:

| **Type** | **Purpose** |
| --- | --- |
| Int | Integer |
| String (or Array<Char>) | String(array of characters) |
| Char | Character |
| Bool | boolean |
| Array<Type> | An array of type `Type` |
| Set<Type> | A set of type `Type` |
| Map<TKey, TValue> | A map with keys of type `TKey`  and values of type `TValue` |
| (argType) => returnType | Function |
| Void | The return type of functions that don't return anything |
| Null | Equivalent to `void` |

Type casting can be acheived with the `as` keyword.

---

## Loops

SparkScript supports three types of loops:

- `while` loops
  
- `for` loops
  
- `for ... in` loops
  

Here are the examples for these loops:

```swift
let i = 0
while i < 10{
    print(i)
    i++
}
/* 
1
2
...
*/
```

```swift
for(let i = 0, i < 10, i++){
    print(i)
}
/* 
1
2
...
*/
```

```swift
let cars: Array<String> = ["Ford", "BMW", "Honda"]
for car in cars{
    print(car)
}
/*
Ford
BMW
Honda
*/
```

---

## Functions

Functions are declared using the `func` keyword.

```swift
func myFunc(arg1: type1, arg2: type2) -> return_type{
    //body
    return something
}
let myRes = myFunc(arg1, arg2)
//...
```

If a function declaration or call has zero parameters, *parantheses are optional*. In function calls, even if there is one argument, parantheses are optional

```swift
func myFunc {
    return 1 + 2 
}
```

This is perfectly valid code.

Also

```ruby
myFunc
```

is a perfectly valid call.

Even

```ruby
doSomethingWithOneArg myArg
```

is valid.

---

## OOP

SparkScript is a multi-paradigm programming language. It also supports object-oriented-programming.

Create classes with the `class` keyword.

```swift
class Human{
    let _name 
    get _name(){name}
    set _name(name) {_name = name}
    func init(name){
        _name = name
    }
    func end(){
        print("Bye, bye")
    }
    func sayName(){
        print(_name)
    }
}
```

The `init` function is the constructor and the `end` function is the destructor.

The verbose syntax of get and set can be simplifed to:

```csharp
let _name get:set
```

Instantiate objects with the `new` keyword.

```typescript
const person1: Human = new Human("person1")
//or
const person2: Human = new Human(name = "person2")
```

Use inheritance with the `extends` keyword. Function overrides can be achieved using `override`.

Propeties can be made `public`, `private` or `internal`. `internal` is like `protected` in many other languages. Methods are `public` by default and variables are `private` by default.

Interfaces can be declared using `protocol`. They are like abstract classes.

Here is an example showing all these features:

```swift
protocol Animal{
    func say(thing: String) -> Void
}
class Human extends Animal{
    let internal _name: String
    func init(name){
        _name = name
    }
    override func say(thing: String) -> Void{
        print(thing)
    }
}
class Dog extends Animal{
    override func say(thing: String) -> Void{
        print("Bark, bark")
    }
}

let dog = new Dog()
let person = new Human("Person1")
person.say("Hello there") //Hello there
dog.say("") //Bark, bark
```
Generics are created using `<T>` eg:
```swift
class GenericTest<T>{
    let public x: T;
    //...
}
```
---

## Functional Programming

Along with OOP, SparkScript also supports functional programming.

Functions are first-class objects, so they can be assigned to variables and treated just like any other variable. The type of a function is `(argType) => returnType` .

Lambdas can be created using `func { ... }`

```swift
let doSomething: (Void) => Void = func {
    print("Doing...")
}
doSomething //Doing...
```

---

## Operators and Conditionals

Operators are:

**Arithmetic**: `+`, `-`, `*`, `/` , `%`

**Boolean**: `and`, `or`, `xor`, `bitand`, `bitor`, `not`

**Comparison**: `==`, `not ==`, `<=`, `>=`, `<`, `>`

...

All other operators are the same as in JavaScript.

`if` statements are created using

```swift
if(condition){
    //...
}
else if(condtion){
    //...
}
else{
    //...
}
```

`switch` statements are written as:

```swift
switch(expression){
    case 1{
        //...
    }
    case 2{
        //...
    }
    default{
       //...
    }    
}
```

---

## Modules and importing

SparkScript has an excellent module system. It allows for four types of exports and imports:

- targeted exports
  
- targeted imports
  
- global exports
  
- global imports
  

Targeted exports export code *to* specific files. For example

```swift
func hello(){
    //...
}
export hello to hello.sp
```

```swift
//hello.sp
import hello
```

will then import all exports *to* hello.sp

Targeted imports / Global exports are the way most programming languages use imports / exports. You can use global exports with global imports. This means that global imports *any* code that is exported, globally or to a specific file. Of course, if the export is targeted, it will only be available in that file. You can also use targeted exports with targeted imports, though that just makes the syntax more verbose.

*Note*: If two files are exporting a function `fun` globally, then `import fun` will raise a ValueError. You need to use targeted imports in this case.

---

## Asynchronous Programming

SparkScript supports threads using the `launch` block. Here is an example

```swift
func main(){
    launch{
        printOne()
    }
    printTwo()
}
func printOne(){
    print(1)
}
func printTwo(){
    print(2)
}
```

```
2
1
```

(The 1 and 2 will be outputted randomly.)

All threads are suspended when the program inside them stops.

You can pause the execution of a program using `await`:

```swift
func main(){
    await printOne()
    printTwo()
}
async func printOne(){
    print(1)
}
func printTwo(){
    print(2)
}
```

In this case, the 1 will always be outputted before the 2.

You can use `await` inside a thread, which blocks the program *inside that specific thread* . The main function will still continue.

---

## Arrays

SparkScript has a built in `Array` type for creating arrays.

You can loop over an array with `for ... in` . Arrays are declared using the `[]` syntax. Most of the functions on `Array`s are similar to those in other languages, such as `arr.push`, `arr.pop`, etc.

---

## Sets

SparkScript supports creating sets using the `Set` type.

```swift
let mySet: Set<String> = {0, 1, 1}
print(mySet) //{0, 1}
```

---

## Maps

Maps in SparkScript are created using the `Map` type.

```swift
let myMap: Map<String, Int> = {"A": 1, "B": 2}
myMap.get("A") //1
myMap.set("B", 3)
myMap.get("B") //3
myMap.set("C", 4) //No error!
```

---
