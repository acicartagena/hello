---
layout: post
title:  Hello Kotlin, from a Swift Developer
description: Notes from Head First Kotlin
date:   2021-12-10 10:12:35 +1000
image:  '/images/posts/learning-kotlin.png'
tags:   [kotlin]
---
# Kotlin

This is more of a reference style notes similar to [learnxiny.com](https://learnxinyminutes.com). The formatting is not nice since I wrote this in Notion and copied it here as well. It's cool to see the similarities between Swift and Kotlin.

## Class

### Constructor / Init

A constructor runs when you instantiate an object. It’s used to define properties and initialize them

```kotlin
// 1. properties in constructor is initialised first
class Dog(val name_param: String, var weight_param: Int, val breed_param: String) {
 // properties in main body
    val name = name_param
    val weight = weight_param
    val breed = breed_param

    lateinit var temperament: String

    // extra code need to run, more complex property initializer
    init {
        // 2. this init code runs after constructor
    }

    // 3. created after 2.
    var activities = arrayOf("walks") 

    init {
        // 3. can have another init to run after 3
    }
}
```

Defining **properties in the main body:**

- flexibility
- no need initialize with a parameter value
  
initialize properties before you use them
**lateinit → lazy** (can't initialize from constructor)

- needs to be **var**
- can't use: Byte, Short, Int, Long, Double, Float, Char, or Boolean

**empty constructor** - compiler writes one for you

```kotlin
class Duck() { }
var duck = Duck()
```

### Properties

custom getter/setters

```kotlin
val weightInKgs = Double
 get() = weight/2.2 //gettter - no parameter function

 // setter - runs each time you try to set the value
 set(value) {
  if (value>0) field = value // if value<0 value won't be set
 }

/* ---------------------------------------------------------------------- */

var myProperty: String
// compiler secretly adds the ff:
var myProperty: String
    get() = field
    set(value) {
        field = value
  }
// data hiding - always calls getter & setter when using dot operator
```

**field**  

- property's backing field
- reference to underlying value of property
- use in getter & setter methods
  - stop getting stuck in an endless loop

### Inheritance

Don't use inheritance if the **IS-A** test fails (just so you can reuse code)

**open**

- prefix explicitly tell compiler class can be used as a *superclass*
- prefix on properties that can be overriden

```kotlin
open class Animal(type: String) {
 open val image = ""
 val food = ""
 
 open fun makeNoise() { ... }
 // final stops override
 final fun sleep() { ... }
}

class Hippo(type: String): Animal(type) {
 override val image = "hippo.jpg"
 override fun makeNoise() { ... }
}
```

- subclass must call superclass primary constructor in header
- override **val** in superclass with **var** in subclass
- override a property's type with its superclass

### Abstract classes

- prevents class from being instantiated
- can contain abstract & non-abstract properties and functions
- make properties abstract so they  need to be overriden
- abstract properties & functions → common protocol (polymorphism)
- **first** **concrete** class below abstract superclass must implement all abstract properties & functions

### Interface

- protocol for common behaviour
- benefit from polymorphism without inheritance
- can add concrete functions to interfaces (provide a function body)
- **properties** can't store state
  - don't have backing fields
- class can inherit from a single direct superclass, but can have multiple interfaces
- **override** interface methods & properties in concrete class

### When to use which

- **class** - new class doesn’t pass the IS-A test for any other type.
- **subclass** - make a more specific version of a class and need to override or add new behaviors.
- **abstract class** - template for a group of subclasses. Guarantee that nobody can make objects of that type.
- **interface** - define common behavior, or a role that other classes can play, regardless of where these classes are in the inheritance tree.

### Any

- mother of all classes
- ensures every class inherits the same behaviour
  - equals(any: Any): Boolean
  - hashCode(): Int
  - toString(): String
- can use polymorphism with any object

### data class

- swift **struct**
- object equality based on values of each object's properties
  - equal object has same hashCode
  - toString value of each property
- ===
  - reference to the same object
- best practice use **val** properties
  - can use var but not recommended
- can't be *abstract* or *open*
- only include properties in primary constructor
  - compiler generated equality & copy

```kotlin
data class Recipe(val title: String,
                    val mainIngredient: String,
                    val difficulty: String = "Easy") { //default parameter values

//secondary constructor
 constructor(is_my_specialty: Boolean): this("Aglio Olio", "Prawn") {
  //code runs when secondary constructor is called
 }
}

// pass values in declaration
val r = Recipe("Spaghetti", "Beef")
// named arguments
val r2 = Recipe(title = "Spaghetti", 
                mainIngredient = "Beef",
                difficulty = "Medium")
```

### Enum classes

- create a set of values that represent the *only* valid values for a variable
- each value defined by the enum class is an instance of that class
- each value defined in an enum class can override the properties and functions it inherits from the class definition
  
```kotlin
// instrument is a property each BandMember has
enum class BandMember(val instrument: String) {
 JERRY("lead guitar") {
  override fun sings() = "plaintively"
 },
 BOBBY("rhythm guitar") {
  override fun sings() = "hoarsely"
 },
 PHIL("base");

 open fun sings() = "occasionally"
}

var selectedBandMember = BandMember.JERRY
println(selectedBandMember.instrument)
println(selectedBandMember.sings())
```

### Sealed class

- restrict your class hierarchy to a specific set of subtypes
- **sealed**
- similar to swift enum with associated value
- sealed class lets you create multiple instances of each subtype
  
```kotlin
sealed class MessageType
class MessageSuccess(var msg: String): MessageType()
class MessageFailure(var msg: String, var e: Exception): MessageType()

fun main(args: Array<String>) {
    val messageSuccess = MessageSuccess("Yay!")
    val messageSuccess2 = MessageSuccess("It worked!")
    val messageFailure = MessageFailure("Boo!", Exception("Gone wrong."))
    var myMessage: MessageType = messageFailure
}
```

### Nested and inner class

- **Nested**
  - class that’s defined inside another class
  - can’t access a nested class from an instance of the outer class without first creating a property of that type inside the outer class
    - val nested = Outer().Nested() //won't compile
  - class doesn’t have access to an instance of the outer class
- **inner**
  - access properties & functions defined by its outer class
  - an access an inner class by creating an instance of the outer class, and then using this to create an instance of the inner class
  
```kotlin
class Outer {
    val x = "x in outer class"
    val myInner = Inner()

    class Nested {
        val y = "y in the nested class"
        fun myFun() = "this is nested function"
        //fun getX() = "value of x is $x" //this line won't compile
    }

    inner class Inner {
        val y = "y in the nested class"
        fun myFun() = "this is nested function"
        fun getX() = "value of x is $x"
    }
}

val nested = Outer.Nested()
val inner = Outer().Inner()
```

### Singleton

- **object**
  - only a single instance of a given type can be created
  - Add an object declaration to a class to create a single instance of that type which belongs to the class
- **companion**
  - A companion object is like a class object, except that you can omit the object’s name
  - Any functions you add to a companion object are shared by all class instances
  
```kotlin
object DuckManager {
    fun herdDucks() { }
}
DuckManager.herdDucks()

class Duck {
    object DuckFactory { 
        fun create(): Duck = Duck()
     }
 
    companion object {
        fun create(): Duck = Duck()
     }
}

val duckFromFactory = Duck.DuckFactory.create()
val duckCompanion = Duck.create()
val duckCompanion2 = Duck.Companion.create()
```

### Object expression

- **object**
- similar to Swift tuple
- anonymous object with no predefined type

```kotlin
val startingPoint = object {
    val x = 0
    val y = 0
}
println("starting point is ${startingPoint.x}, ${startingPoint.y}")
```

**is**

- check for types

```kotlin
val animal: Animal = Wolf()
if (animal is Wolf) {
 animal.doWolfThings()
}
```

### as

- explicit cast
- both hold reference to same object (but knowledge of what it is might be different)

```kotlin
var wolf = r as Wolf
wolf.doWolfThings()
```

## when

- Swift Switch statement

```kotlin
when (x) {
 0 -> println("x is 0")
 1,2 -> println("x is 1,2")
 else -> {
  println("x is others")
 }
}
```

## Nullability

- similar to swift
- **?.** (safe call operator)
  - can be chained
- **?.let**
  - similar to **if let** (swift)
  - allows you to run code for a value that’s not null
  - use {} (curly braces) for the body
- **?:** (Elvis operator)
  - if value is not null return value, else return value on the right
- **!!** (not-null assertion operator)
  - throws NullPointerException

```kotlin
var w: Wolf? = Wolf()

// safe call operator
w?.doWolfThings()

// if let equivalent
w?.let {
 println(it.hunger)
}

// elvis
w?.hunger ?: -1
```

## Try Catch Finally

```kotlin
try {
 turnOvenOn()
 x.bake()
} catch (e: BakingException) {
 println("baking experiment failed")
} finally {
 turnOvenOff()
}
```

## Exception

- Every exception is of type: **Exception**
- **throw** use to throw an exception
  - type **Nothing**

```kotlin
val h = w?.hunger ?: throw AnimalException()
```

## Collections

### Array

- can't change size
- val numbers = arrayOf(1,2,3)
- can be updated

### List

- When sequence matters
- Iterable
- (Might be similar to array swift?)
- Allows duplicate values
  
```kotlin
val shopping = listOf("Tea", "Eggs", "Milk")

// iterate
for (item in shopping) println(item)

// check existence
if (shopping.contains("Milk")) {
    println(shopping.indexOf("Milk"))
}

val updateableList = mutableListOf("Tea")

updateableList.add("Bread")

if (updateableList.contains("Bread")) {
   updateableList.remove("Bread")
}

val toAdd = listOf("Cookies", "Sugar")
updateableList.addAll(toAdd)

val toRemove = listOf("Milk", "Sugar")
updateableList.removeAll(toRemove)
```

### Set

- When uniqueness matters
- Iterable
- Steps for determining uniqueness
    1. Gets the object's **hash code** and uses that to compare with other objects in the set
        1. hash code as "bucket"
        2. matching hash codes go to step 2
    2. **===** operator to compare the new value against any objects it contains with the same hash code (bucket)
    3. **== operator** to compare the new value against any objects it contains with matching hash codes
- Same value
  - same object
  - equal to a value it already contains

```kotlin
val friendSet = setOf("Jim", "Sue", "Sue", "Nick", "Nick")

val mFriendSet = mutableSetOf("Jim", "Sue")
mFriendSet.add("Nick")
mFriendSet.remove("Nick")
```

### Map

- Key value pair
- NOT iterable!
- Similar to dictionary in swift
  
```kotlin
val ri = Recipe("Chicken soup")
val r2 = Recipe("Thai Curry")
val recipeMap: Map<String, Recipe> = mapOf("recipe1" to r1, "recipe2" to r2)

recipeMap.containsKey("recipe1")
recipeMap.containsValue(r1)

if (recipeMap.containsKey("recipe1") {
 val recipeMap.getValue("recipe1")
}

for ((key, value) in recipeMap) {
     println("Key is $key, value is $value")
}

val mRecipeMap = mutableMapOf("recipe1" to r1, "recipe2" to r2)

val r4 = Recipe("Jambalaya")
val r5 = Recipe("Sausage Rolls")
val recipesToAdd = mapOf("Recipe4" to r4, "Recipe5" to r5)

mRecipeMap.putAll(recipesToAdd)

mRecipeMap.values
mRecipeMap.keys
```

## Generics

- similar definition in swift?
  - val x: MutableList< **String**>
- Compiler can infer generic type

```kotlin
interface MutableList<E> : List<E>, MutableCollection<E> { }

abstract class Pet(var name: String)
class Cat(name: String): Pet(name)
class Dog(name: String): Pet(name)
class Fish(name: String): Pet(name)

class Contest<T: Pet> { }

fun <T: Pet> listPet...

// to call function, specify type
val catList = listPet<Cat>(Cat("Zazzles"))

// can define multiple generic types
class MyMap<K, V> { }
```

- A Retailer<Pet> variable will only accept a Retailer<Pet> object
  - val petRetailer: Retailer<Pet> = CatRetailer() //this wont' compile

### **out** (covariant)

- generic subtype object in a place of a generic supertype
- generic type is **covariant**
  - can use a subtype in place of a supertype.
- can’t use if the class has function parameters or var properties of that generic type.
- used for collections
  
```kotlin
interface Retailer<T> {
 fun sell(): T
}
// val petRetailer: Retailer<Pet> = CatRetailer() //this wont' compile

interface Retailer<out T> { .. } 
val petRetailer: Retailer<Pet> = CatRetailer()
```

### in (contravariant)

- lets you use a generic supertype in place of a subtype
- can use a supertype in place of a subtype. This is the opposite of covariance.
- can't use if class functions use it as a return type, or if that type is used by any properties, irrespective of whether they’re defined using val or var
  
```kotlin
class Vet<in T: Pet> {
 fun treat(t: T) {
 }
}

val catContest = Contest<Cat>(Vet<Pet>())

// can be defined locally
class Vet<T: Pet> {
 fun treat(t: T) {
 }
}
class Contest<T: Pet>(var vet: Vet<in T>) { }
```

### invariant

- generic type has no in or out prefix
- can only accept references of that specific ty

## Lambdas

- type of object that holds a block of code
  - **(parameters) -> return_type**
- { x: Int, y: Int → x + y }
- **→**
  - separate parameters from the body
- **invoke**
  - call lambda
- **it**
  - lambda with 1 parameter that the compiler can infer
- **Unit**
  - similar to return **Void** (in swift)
  - lambda has no return value
    - () → Unit

```kotlin
val addInts = { x: Int, y: Int -> x + y }

val result = addInts.invoke(6, 7)
val result2 = addInts(6, 7)

val greeting: () -> String = { "Hello!" }

val addFive: (Int) -> Int = { it + 5 }
```

- **Higher order function**
  - uses a lambda as a parameter or return value
  - can move the lambda outside ()
    - similar to swift
  - function can return a lambda

## typealias

- provide different name for an existing type
  - typealias DoubleConversion = (Double) → Double
  - typealias DuckArray = Array<Duck>

## higher order functions

- **filter**
- **minBy**
- **maxBy**
  - If you call minBy or maxBy on a collection that contains no items, the function will return a null value.
- **map**
  - returns a **List** and not **Map**
- **forEach**
  - similar to for loop
  - arrays, Lists, Sets, and on a Map’s entries, keys and values properties.
    - Not Map
  - has no return value
- **groupBy**
  - group your items in a collection according to some criteria
  - doesn't work on Map
  - returns a **Map** with a **List** as the value
    - Map<String, List<Grocery>>
- **fold**
  - similar to **reduce**
  - specify an initial value, and perform some operation on it for each item in a collection
  - doesn't work on Map
  - default left to right
    - use **foldRight**
- **reduce**
  - similar to **fold** but no need to specify initial value
  - default left to right
    - use **reduceRight**
- can chain higher order functions

## Coroutines

- write code that runs asynchronously
- coroutine
  - like a lightweight thread
  - run on a shared pool of threads
  - same thread can run many coroutines
- launching is like starting a separate thread of execution, or **thread**
- run on a shared pool of threads by default, and the same thread can run many coroutines
- **GlobalScope.launch**
  - separate coroutine in the background by enclosing the code
  - kotlinx.coroutines library

    ```kotlin
    fun main() {
     GlobalScope.launch { playBeats("x-x-x-") }
     playBeats("x----x----")
    }
    ```

- **runBlocking**
  - code to run in the same thread but in separate coroutines
  - blocks the current thread until the code that’s passed to it finishes running
  - blocks the current thread
- **launch**
  - launch a new coroutine
  - launch a coroutine that runs in the same thread
  - use the same scope as runBlocking

```kotlin
fun main() {
 runBlocking {
  launch { playBeats("x-x-x-") }
  playBeats("x----x----")
 }
}
```

- **delay**
  - pauses the current coroutine
  - allows other code to run
  - similar to Thread.sleep
- **suspend**
  - call a suspendable function (such as delay) from another function, that function must be marked with suspend

    ```kotlin
    suspend fun playBeats(beats: String) { 
     delay(..)
    }
    ```

## Test

### JUnit

- Each test is held in a function, prefixed with the annotation **@Test**
- assertEquals
- use back ticks for function names
  - wrap function names in back-ticks (**`**)
  - fun `should be able to add 3`()

### KotlinTest

- **String Specification**—or **StringSpec**
- use rows to test your code against entire sets of data

```kotlin
"should be able to add 3 and 4 and it musn't go wrong" {
 val totaller = Totaller()
 totaller.add(3) should be 7
}
```

## Package and import

- Package
  - organize your code
  - prevents name conflicts
  - Each source file can only have one package declaration
- **import**
  - can refer to the class without typing the fully qualified name each time

## Visibility Modifiers

- **public**
  - visible everywhere
  - default behaviour
- **private**
  - visible to code inside its source file
- **internal**
  - visible inside the same module, but invisible elsewhere
  - module - set of Kotlin files that are compiled together
- **protected**
  - applied to properties, functions & other members
  - Makes the member visible inside the class, and any of its subclasses.

## Extensions

- add new functions and properties to an existing type without you having to create a whole new subtype.
  
```kotlin
// add function to Double
fun Double.toDollar(): String {
 return "$$this"
}

let dbl = 42.25
println(dbl.toDollar())

// add property to String
val String.halfLength
 get() = length/2.0

val test = "This is a test"
println(test.halfLength)
```
