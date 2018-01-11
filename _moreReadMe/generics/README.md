# Generics in Java

## Generic Classes

A generic class declaration looks like a non-generic class declaration, except that the class name is followed by a type parameter section.

The type parameter section of a generic class can have one or more type parameters separated by commas. These classes are known as parameterized classes or parameterized types because they accept one or more parameters.

**Syntax:**
```
public class Box<T> {
   private T t;
}
```

<ul class="list">
<li><p><b>Box</b> − Box is a generic class.</p></li>
<li><p><b>T</b> − The generic type parameter passed to generic class. It can take any Object.</p></li>
<li><p><b>t</b> − Instance of generic type T.</p></li>
</ul>

## Naming Conventions

By convention, type parameter names are named as single, uppercase letters so that a type parameter can be distinguished easily with an ordinary class or interface name. Following is the list of commonly used type parameter names −

<ul class="list">
<li><p><b>E</b> − Element (mainly used by Java Collections framework)</p></li>
<li><p><b>K</b> − Key (mainly used to represent key of a map)</p></li>
<li><p><b>V</b> − Value (mainly used to represent value of a map)</p></li>
<li><p><b>N</b> − Number (represents numbers)</p></li>
<li><p><b>T</b> − Type (represents first generic type parameter)</p></li>
<li><p><b>S, U, V, etc</b> − 2nd, 3rd, 4th Types</p></li>
</ul>

## Type Inference

Type inference represents the Java compiler's ability to look at a method invocation and its corresponding declaration to check and determine the type argument(s). The inference algorithm checks the types of the arguments and, if available, assigned type is returned. Inference algorithms tries to find a specific type which can fullfill all type parameters.

Compiler generates unchecked conversion warning in-case type inference is not used.

**Syntax:**
```
Box<Integer> integerBox = new Box<>();
```

<ul class="list">
<li><p><b>Box</b> − Box is a generic class.</p></li>
<li><p><b><></b> − The diamond operator denotes type inference.</p></li>
</ul>

Using diamond operator, compiler determines the type of the parameter. This operator is avalilable from Java SE 7 version onwards.

## Generic Methods

You can write a single generic method declaration that can be called with arguments of different types. Based on the types of the arguments passed to the generic method, the compiler handles each method call appropriately. Following are the rules to define Generic Methods −

<ul class="list">
<li><p>All generic method declarations have a type parameter section delimited by angle brackets (< and >) that precedes the method's return type ( < E > in the next example).</p></li>
<li><p>Each type parameter section contains one or more type parameters separated by commas. A type parameter, also known as a type variable, is an identifier that specifies a generic type name.</p></li>
<li><p>The type parameters can be used to declare the return type and act as placeholders for the types of the arguments passed to the generic method, which are known as actual type arguments.</p></li>
<li><p>A generic method's body is declared like that of any other method. Note that type parameters can represent only reference types, not primitive types (like int, double and char).</p></li>
</ul>

```
public static <E> void printArray( E[] inputArray ) {
      // Display array elements
      for(E element : inputArray) {
         System.out.printf("%s ", element);
      }
      System.out.println();
   }
```

## Multiple Type Parameters

A Generic class can have muliple type parameters. Following example will showcase above mentioned concept.

```
public class Box<S,T> {
   private T t;
   private S s;
}
```

## Parameterized Types

A Generic class can have parameterized types where a type parameter can be substituted with a parameterized type. 
Parameterized Types are types that take other types as parameters. Eg - Collection<String>, ArrayList<String>, etc.
  
```
public class Box<S,T> {
   ...
}
...
Box<Integer, List<String>> box = new Box<Integer, List<String>>(); //Parameterized Types
...
```

## Raw Types

A raw type is an object of a generic class or interface if its type arguments are not passed during its creation.

```
Box rawBox = new Box();
```

## Bounded Type Parameters

There may be times when you'll want to restrict the kinds of types that are allowed to be passed to a type parameter. For example, a method that operates on numbers might only want to accept instances of Number or its subclasses. This is what bounded type parameters are for.

To declare a bounded type parameter, list the type parameter's name, followed by the extends keyword, followed by its upper bound.

**Single Bound:**
```
public static <T extends Comparable<T>> T maximum(T x, T y, T z)
```

**Multiple Bounds:**
```
public static <T extends Number & Comparable<T>> T maximum(T x, T y, T z)
```
<ul class="list">
<li><p><b>maximum</b> − maximum is a generic method.</p></li>
<li><p><b>T</b> − The generic type parameter passed to generic method. It can take any Object.</p></li>
</ul>

The T is a type parameter passed to the generic class Box and should be subtype of Number class and must implments Comparable interface. In case a class is passed as bound, it should be passed first before interface otherwise compile time error will occur.

**Calling eg.:**
```
maximum( 6.6, 8.8, 7.7 )
```

## Collections Framework Examples

Java has provided generic support in Collections Framework Interfaces like List, Set, Map, etc.

### List

```
List<T> list = new ArrayList<T>();
```
<ul class="list">
<li><p><b>list</b> − object of List interface.</p></li>
<li><p><b>T</b> − The generic type parameter passed during List declaration.</p></li>
</ul>
The T is a type parameter passed to the generic interface List and its implemenation class ArrayList.

### Set

```
Set<T> set = new HashSet<T>();
```
<ul class="list">
<li><p><b>set</b> − object of Set Interface.</p></li>
<li><p><b>T</b> − The generic type parameter passed during Set declaration.</p></li>
</ul>
The T is a type parameter passed to the generic interface Set and its implemenation class HashSet.

### Map
```
Map<T> set = new HashMap<T>();
```
<ul class="list">
<li><p><b>set</b> − object of Map Interface.</p></li>
<li><p><b>T</b> − The generic type parameter passed during Map declaration.</p></li>
</ul>
The T is a type parameter passed to the generic interface Map and its implemenation class HashMap.

## Generics Wild Cards

The question mark (?), represents the wildcard, stands for unknown type in generics. 

### Upper Bounded Wildcards

There may be times when you'll want to restrict the kinds of types that are allowed to be passed to a type parameter. For example, a method that operates on numbers might only want to accept instances of Number or its subclasses.

To declare a upper bounded Wildcard parameter, list the ?, followed by the extends keyword, followed by its upper bound.
```
public static double sum(List<? extends Number> numberlist) {
      ...
   }
```

### Unbounded Wildcards

There may be times when any object can be used when a method can be implemented using functionality provided in the Object class or When the code is independent of the type parameter.

To declare a Unbounded Wildcard parameter, list the ? only.
```
public static void printAll(List<?> list) {
    ...
   }
```

### Lower Bounded Wildcards

There may be times when you'll want to restrict the kinds of types that are allowed to be passed to a type parameter. For example, a method that operates on numbers might only want to accept instances of Integer or its superclasses like Number.

To declare a lower bounded Wildcard parameter, list the ?, followed by the super keyword, followed by its lower bound.
```
public static void addCat(List<? super Cat> catList) {
      ...
   }
...
//You can add list of Cat or Animal (super class of the Cat class)
addCat(animalList);
addCat(catList);
```

## Restrictions on Generics

**No Primitive Types** - Using generics, primitive types can not be passed as type parameters.
```
Box<int> intBox = new Box<int>() //Error
```   
NOTE : Use Wrappers like Integar instead.

**No Instance** - A type parameter cannot be used to instantiate its object inside a method.
```
public static <T> void add(Box<T> box) //Error
```   
NOTE : To achieve such functionality, reflection can be used.

**No Static field** - Using generics, type parameters are not allowed to be static. As static variable is shared among object so compiler can not determine which type to used.
```
class Box<T> {   
   private static T t; //Error
}
```   
