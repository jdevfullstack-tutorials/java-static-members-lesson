# Java Static Members of a Class

*`updated 21 April 2022`*

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fxdvrx1%2Fjava-static-members-lesson&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=PAGE+VIEWS&edge_flat=false)](https://hits.seeyoufarm.com)

At first, I was just ignoring the importance of a variable or a method being static.
And my understanding at first was quite obscure but then I realized how important
they are in computer programming.

A static member, whether a method or a variable, can exist on its own the moment
you run a program. So, you can access them prior to any object creation. That is
the very reason why the main method is static. It should exist prior to any
object because it is the entry point of any running program in Java.

Another important lesson here: once you created an object from a class that contains
static variable, that object will not create a copy of its own static variable,
it will always refer to the original static variable. This is very powerful in
programming. For instance, you want to keep track of a certain variable whether 
its value is changing that will be used by several objects that depend on its status. 
It is, in essence, a global variable.

`SampleStatic.java`

```
class SampleStatic {
   //a static block
   //this is needed to initialize or load things
   //take note, this static block is loaded only ONCE 
   //the moment you run the code,
   //for demonstration purposes, we just display a 
   //default message here,
   static {
      System.out.println("A static member is called, " +
                         "this is a default message, " +
                         "independent of any object.");  
   }
   
   //a static variable,
   //it is considered as global variable
   //when this is changed in an object,
   //the value will be reflected on all
   //objects created from this class
   static Integer staticVar = 5;
   
   //a static method, independent of any object
   //and can be called before any object exists
   //just like the main method
   static void staticMeth() {
      System.out.println("static `staticVar` is " +
                         staticVar);
   }      
}
```

And in main: `MainMethod.java`

```
class MainMethod {
   public static void main(String[] args) {
      //a call to the static method of `SampleStatic` class
      SampleStatic.staticMeth();   
      
      //create an instance of `SampleStatic`
      //to demonstrate 
      //the behavior of static members
      SampleStatic sample1 = new SampleStatic();
      //this will change the original
      //value of the static variable
      //`staticVar` and will be shared
      //by all objects
      System.out.println("`staticVar` is changed by sample1 object so: ");
      sample1.staticVar = 10;
      SampleStatic.staticMeth();
      
      //another object that will share
      //the same static variable
      SampleStatic sample2 = new SampleStatic();
      System.out.println("`sample2` object shares " +
                         "the same variable: `staticVar` = " +
                         sample2.staticVar);
      
   }
}
```

the result is:

```
> run MainMethod
A static member is called, this is a default message, independent of any object.
static `staticVar` is 5
`staticVar` is changed by sample1 object so: 
static `staticVar` is 10
`sample2` object shares the same variable: `staticVar` = 10
```

## static block
As demonstrated above, if you need to initialize things, do it in
the static block. The moment you run the code, it is loaded ONCE.

## static method
The static method has restrictions compared to a regular method.
> It can only call directly other static methods.

> It can only call directly static variables.

> It cannot refer to *this* and *super* because it does not depend
on any object creation. 

## static variable
As was mentioned, it is essentially a global variable. If ever it is changed
directly or maybe through an object, all objects and direct calls to it
manifest that change.
