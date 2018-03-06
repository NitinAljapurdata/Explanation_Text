Java 8 Functional Interfaces inside the java.util.function package.

--> java.util.function.Predicate<T>
	public interface Predicate<T>{
		public boolean test(T t);
	}
--> java.util.function.consumer<T>
	public interface Consumer<T>{
		public void accept(T t);
	}
	use this interface when you need to access an object of type T and perform some operations on it. For example, you can use it to create a method forEach, which takes a list of Integers and applies an operation on each element of that list.
	
--> java.util.function.Function<T, R>
	public interface Function<T, R>{
		public R apply(T t);
	}
	This interface when you need to define a lambda that maps information from an input object to an output
	Example: Extacting the weght of an apple or mapping a string to its length.

1. T -> R --> Function 
2. (int, int) -> int --> IntBinaryOperator
3. T -> void --> Consumer
4. () -> T --> Supplier
5. (T, U) -> R --> BiFunction
	
Use case Example of lambda Matching functional interface
A boolean
expression
(List<String> list) -> list.isEmpty() Predicate<List<String>>
Creating objects () -> new Apple(10) Supplier<Apple>
Consuming from
an object
(Apple a) ->
System.out.println(a.getWeight())
Consumer<Apple>
Select/extract
from an object
(String s) -> s.length() Function<String, Integer> or
ToIntFunction<String>
Combine two
values
(int a, int b) -> a * b IntBinaryOperator
Compare two
objects
(Apple a1, Apple a2) ->
a1.getWeight().compareTo
(a2.getWeight())
Comparator<Apple> or
BiFunction<Apple, Apple, Integer> or
ToIntBiFunction<Apple, Apple>



Type Inference:
You can simplify your code one step further.
Example: 
	Comparator<Apple> comparatorByNameReverse = (Apple apple1, Apple apple2) -> -apple1.getColor().compareTo(apple2.getColor()); --> without type inference
				Changed to 
	Comparator<Apple> comparatorByNameReverse = (apple1, apple2) -> -apple1.getColor().compareTo(apple2.getColor()); --> With Type Inference

Using local Variables:
int portNumber = 1337;
Runnable run = () -> sysout(portNumber);
		//Access Local Variables:
		final int portNumber = 1337;
		Runnable runa = () -> System.out.println(portNumber);
		//portNumber = 10;
	
Restrictions on local variables:
	Reason for why local variables to be declared as final if the local variable is used in lambda expression
	
Closure:

Method references:
Method references let you reuse existing method definitions and pass them just like lambdas.

inventory.sort((Apple a1, Apple a2)
-> a1.getWeight().compareTo(a2.getWeight()));
After (using a method reference and java.util.Comparator.comparing):
inventory.sort(compare(Apple::getWeight));

--------------------------------------------------------------------------
Lambda Method 									reference equivalent
--------------------------------------------------------------------------
(Apple a) -> a.getWeight() 						Apple::getWeight
() -> Thread.currentThread().dumpStack() 		Thread.currentThread()::dumpStack
(str, i) -> str.substring(i) 					String::substring
(String s) -> System.out.println(s) 			System.out::println


There are three main kinds of method references:
1. A method reference to a static method (for example, the method parseInt of Integer, written Integer::parseInt)
2. A method reference to an instance method of an arbitrary type (for example, the method length of a String, written String::length)
3. A method reference to an instance method of an existing object (for example, suppose you have a local variable expensiveTransaction that holds an object of type Transaction, which supports an instance method getValue; you can write expensiveTransaction::getValue)

Difference between 2 and 3 is: 
--> Second kind of method references such as String::length is that your are referring too a method to an object that will be supplied as one of the parameters of the lambda.
	(String str) -> str.toUpperCase() -->
						String::toUpperCase
--> Third Kind of method references refers to a situation you are calling a method in a lambda to an external objec that already exists.
	expensiveObject.getValue().---> expensiveObject::getValue
	
Streams:
-------
“a sequence of elements from a source that supports data processing operations.”

Sequence of elements: collection
source: where we consume data-providing source such as collection

Traversable only once
	List<STring> list = Arrays.toList("abc","efg","hihj");
	Stream<String> listStream = list.stream();
	listStream.forEach(sysout);
	listStream.forEach(sysout); --> error IllegalStateException Stream has already closed .
So keep in mind that you can consume a stream only once!

Short-Circuiting:
Despite the fact that many dishes have more than 300 calories, only the first three are selected! This is because of the limit operation and a technique called short-circuiting

Loop Fusion:
filter and map are two separate operations, they were merged into
the same pass (we call this technique loop fusion).

Intermediate Operations:
--> filter --> Predicate
--> map -->Function
--> limit
--> distinct
--> sorted
--> skip

Terminal Operations:
--> collect
--> forEach
--> count

1) stream Stream<Dish>
2) filter isVegetarian Stream<Dish>
3) map List<String>
3) collect(toList()) List<String>

Optionals:
https://www.javacodegeeks.com/2017/07/java-8-optionals.html

--> Lambda expressions:
	Lambda expressions let you pass around a piece of code in a concise way(easy, readable).
		Example: Runnable runnable = new Runnable() {
					@Override
					public void run() {
					System.out.println("Hi");
				}
				
				Now: 
				Runnable runnable = () -> System.out.println("Hi");
				Thread thread = new Thread(runnable);
				thread.start();
				
				
--> Method references:
	They let you select an existing method defined in a class and pass it around.
	
		Example: 
			List<String> strs = Arrays.asList("C", "a", "A", "b");
			Collections.sort(strs, new Comparator<String>() {
				@Override
				public int compare(String s1, String s2) {
				return s1.compareToIgnoreCase(s2);
   			}
			});
			
			Now:
			Collections.sort(strs, String::compareToIgnoreCase);
--> Enhanced Interfaces
	 Introduces two enhancements:
		--> Default Methods
				--> For enhancements use it
		--> Static methods
				--> For util API's
			
Complitable future
https://www.youtube.com/watch?v=OYpTn0nWKR4&t=1011s

----------------------------------------------------------------------------------------------------
Java8 - Features:
-------------------
--> Lambda Expressions
--> Functional Interfaces --> to invoke or to call lamdba experssion we should go for functional interfaces
--> Default methods in Interface
--> Static methods in Interface
--> Predefined Functional Interfaces
	--> Predicate
	--> Function
	--> Consumer
--> Method reference and Constructor reference by Double colon (::) operator
--> Streams API
	 --> to perform bulk operation is easily to write readable concise code.
--> Date and Time API ( Joda API ) 
	 --> Introduced by joda.org
	 
Java 
1.0
	 1.1
1.2 --> Collection ..Major version
	 1.3
	 1.4
1.5 --> Major Version
	 1.6
	 1.7
1.8 --> Major Version

--> To simplify programming
--> To get the benefits of functional programming.. so that we enable the functional programming language in the form of lambda expressions
	We can send behaviour as argument
--> To get benefits of multi-core processing or to enable parallel processing 
--> To use API's very easily and effectively

LISP

What is Lambda Expression:
---------------------------
Lambda Expression is an anonymous function:
--> Not having any Name
--> Not having modifiers
--> Not having any return type 

Type Inference:
compiler can guess the type of context automatically 

@Functional Interface:
-----------------------
Unexpected @FunctionInterface annotation.. multiple non-overriding abstract methods found in Interface Interf1
interface Interf{
	public void m1();
	default public void m2(){}
	static void m3(){}
}
Valid

interface Interf{
	public void m1();
	public void m2(){}
}
In-Valid

interface Interf{
	
}
In-valid
	
@Functional Interface W.R.T Inheritance:
-----------------------------------------
Case 1:
If an interface extends Functional Interface and child interface does not contain any abstract method, then child interface is always Functional Interface.

@FunctionInterface
interface P{
	public void m1();
}
interface C extends P{
	
}
Compilation: Valid

Case 2:
In the child interface we can define exactly same parent interface abstract method.
@FunctionInterface
interface P{
	public void m1();
}
@FunctionInterface
interface C extends P{
	public void m1();
}
Compilation: Valid

Case 3:
In the child inteeface we cannot define any new abstract methods otherwise we will get compile time error.
@FunctionInterface
interface P{
	public void m1();
}
@FunctionInterface
interface C extends P{
	public void m2();
}
Compilation: Not-Valid
One from Parent and one from Child

CE: unexpecte @FunctionInterface annotation multiple non-overriding abstract methods found in interface "C".

Case 4:

@FunctionInterface
interface p{
	public void m1();
}
interface C extends p{
	public void m2();
}

Compilation: Valid --> since Interface "C" is not annotated with @FunctionInterface.

--> It should contain exactly one abstract method 
--> It can contain any number of default and static methods 
--> FunctionInterface acts as a "type" for Lambda Expressions
	Interf1 f1 = () -> sysout("hello");
	here the type of lambda experssion is functional interface Interf1
--> FunctionInterface can be used to invoke Lambda expression
	f1.m1();
--> For lambda expressions concept FunctionInterface concept came

We can replace Anonymous inner class with lambda experssion in only one particular cases that is the anonymous inner class that contains only one abstract method.
that is only in the case of functional interfaces anonymous inner classes can be replaced with lambda experssion

Anonymous Inner class != Lambda Expression

Case (Anonymous Inner class):

--> Inside Anonymous inner class is it possible to declare instance variable yes we can declare
--> Inside Anonymous inner class "this" always refers to current inner class (object) instance variable only.

Case (Lambda Expression)
--> Inside lambda experssion is it possible to declare "instance" variable or not	
	--> Not possible
			--> the variable which is declared inside the lambda experssion is always acts as "local" variable only 
	Example:	
	Class Test{
		int x = 888;
		public void m1(){
			Interf f1 = () -> { int x=999; sysout(this.x );}
		}
		psvm (){
			Test t =  new Test();
			t.m1(); --> 888
		}
		Here "x" is local variable but not instance variable
		
--> Inside Lambda expression "this" always refers outer class variables only 
------------------------------------------------------------------------------------------------------------
Anonymous InnerClas                             |                          Lambda Expressions
------------------------------------------------------------------------------------------------------------
-->It is a class without name								It is a function without name
--> It can extend concrete and     							It cannot extend abstract and concrete methods 
abstract classes
--> AI class Can implement as								LaExp can implement interface which contain only one abstract methods with any number of default and static methods
interface which contain any number 
of abstract methods 
-->AI we can declare instance variables    					Here we cannot declare instance variables whatever declared can be considered as local variables
--> Can be instantiated										we cannot instantiate
--> this always refers to current   						this always refers to outer class object
anonymous inner class object but 
not outer class object
--> A seperate .class is generated    						no seperate class is generated
for inner class 

--> memory will be allocated on demand whenever.       will reside in premanent memory of JVM(method area)


--> From Lambda Expression we can access unclosing class variable and enclosing method variable
	--> The local variable (but not the class level variable) which are referenced from lambda expression are final or effectively declared as final 
	Example:
		class Test{
			int x = 10;
			public void m2(){
				int y = 999;
			  Infer1 i = () ->{
				sysout(x);
				sysout(y);
				y = 888; --> compile time error
									local variables referenced from a lambda expression must be final 
			  }
			  
Advantages of Lambda Expression:
----------------------------------
--> We can enable functional programming in java

We can assign a procedure to a variable 
	Exmaple: 	
			String s = "durga";
			Intref i = () -> sysout("hello");
			directly as an argument --> early we can pass as variable or object 
--> We can reduce length of the object readability will be improved
--> We can resolve complexity of Anonymous Inner classes until some extent.
--> We can pass procedures/functions as argument instead of sending object
--> Easier to use updated API's and libraries
--> Enable support for Parallel processing

Default methods inside Interface:
----------------------------------		

Default methods with respect to Inheritance:
---------------------------------------------

interface Left{
	default void m1();
}
interface Right{
	default void m1();
}
class Test implements Right, Left{
}
Compiltation: Fails 
class Test inherits Unrelated defaults for Left and Right
failed because of ambiguity 

Solution: --> Provide implementation in class Test 
class Test implements Right, Left{
	public void m1(){
		sysout("my Test m1");
		}
}
Solution: --> i dont want to provide new implemtation want to use implementation provided by Left or Right 
class Test implements Right, Left{
	public void m1(){
		Left.super.m1();
	}
}
InterfaceName.super.m1(); --> want to use a particular method
--> Provide complete new implmentation or use the existing implmented methods

-------------------------------------------------------------------------------------------------------------
Interface with default method			                                               Abstract Class
-------------------------------------------------------------------------------------------------------------
Interface with default method:
	--> Inside interface every variable is always is public static final but we cannot declare instance variables
Abstract Class	:
	--> Inside abstract class we can declare instance variables, which are required to the child class

Interface with default method:
	--> Interface never talks about state of object.
Abstract Class:
	--> Abstract class can talk about state of object.

Interface with default method:
	--> Inside interface we cannot declare constructor
Abstract Class:
	--> Inside abstract class, we can declare constructor

Interface with default method:
	--> we cannot declare instance and static blocks
Abstract Class:
	--> we cann declare instance and satatic blocks

Interface with default method:
	--> Functional interface with default method can refer Lamda Expression
Abstract Class:
	--> Abstract class cannot refer Lambda Expression

Interface with default method:
	--> Inside interface we cannot override Object class methods
Abstract Class:
	--> Inside Abstract class we can override object class methods..
	
    Interface with default methods != Abstract classes

-------------------------------------------------------------------------------------------------------------

Static methods inside Interface:
----------------------------------
-->Inside interface we can take static method from java1.8
--> To define general utility methods.
--> Interface static methods by default are not available to the implementation class.	
	--> That's why in the implementation class We cannot call static method directly, by implementation object reference or by using implmentation class name.
	Possible using only Interface name only.
	Example:
		interface inref{
			public static void m1(){sysout("Hello")}
	    }
		class Test implements intref{
		psvm(){
			Test t = new Test();
			t.m1(); --> error
			Test.m1(); --> error
			intref.m1() --> valid
		  }
		}
		
Interface static methods wrt Overriding:
-----------------------------------------
--> Overriding concept is not applicable for Interface static methods. 
--> If you want same method signature you can do so but it is not a overriding since the static method is not available to the implemented class  

interface Interef{
	psvm(){
		sysout("Interface main method");
	}
}

Comparable
Runnable
ActionListener
Callable

Predefined Functional Interfaces: Introduced in java8 version
Predicate
Function
Consumer
Supplier

Package: Java.util.function

Predicate: (Interface) Predicate Joining:
------------------	
--> Java 1.8
--> """"A boolean valued function"""" 
--> test method 
	interface Predicate<T>{
		public boolean test(T t);
	}
--> Predicate Has 3 Default methods and 1 static method:
	Default Method:
		--> and
		--> or
		--> negate
	Static Method:
		--> isEqual
	

Function:
----------
--> It can return any   Type
Package: java.util.Function 
--> interface Function<T, R>{
	R apply(T t); --> after performing functionality return type "R"
}
T --> Input parameter
R --> Return Type
Example: 
	Find length of a given string
	Function<String, Integer> findStringLength = s -> s.length();
--> Function have 2 default methods and 1 static method
	Default Method:
		--> compose
		--> andThen
	Static Method:
		--> identity
	Example: 	
		Function<Integer, Integer> times2 = e -> e * 2;
		Function<Integer, Integer> squared = e -> e * e; 
	
		times2.compose(squared).apply(4); // Returns 32
				--> squared -- 4 --> 16
				--> times2  -- 16*2 --> 32
		times2.andThen(squared).apply(4); // Returns 64 
				--> times2  -- 4*2  --> 8				--> squared -- 8*8 --> 64
		Link: http://www.deadcoderising.com/2015-09-07-java-8-functional-composition-using-compose-and-andthen/
		
Consumer:(accept, consume items and perform process)
---------
--> Java8
--> Package: java.util.function
interface Consumer<T>{ --> T Input Type
	void accept(T t);
}
--> It consumes value and performs operation and will not return any value.
--> Consumer has 1 default method
	Default:
		--> andThen
				--> Here andThen is executed last 
			Example:
				Consumer<Integer> multiply = i -> System.out.println(i * 2);
				Consumer<Integer> add2 = i -> System.out.println(i + 2);
				
				multiply.andThen(add2).andThen(multiply).accept(10);
				Output: 	20 12 20

Supplier:(always going to provide or return some value)
---------				
interface Supplier<R> { --> R Return Type
	R get();
}        

-------------------------------------------------------------------
Method Reference and Constructor Reference by Double Colon Operator:
--------------------------------------------------------------------

Method Reference by Double Colon Operator:
------------------------------------------
Code reusability
If you want to use method reference compulsory both methods should have arguments types
--> """Only argument types mustbe match"""
--> method name, return type, modifier not at all important
	---Static Method---
		ClassName::MethodName
	Example:
		interface Interef{
			public void m1();
		}
		Class Test{
			public static void m2(){
				sysout("m2");
			}
			psvm(){
				Interef i = Test::m2;
				i.m1();
			}
		}
	  Interef interface m1 method internally refers Test class static method m1	
		
	*****MethodReference is alternative syntax to lambda Expression***
	
--> the target method (Here m2) can be:
	--> Static Method or
	--> Instance Method
  Only one condition that argument types must be same
  
    --- Instance Method ---
		ObjectRef::MethodName
		Example:
			Test t = new Test();
				 t::m2(); 

Thread:
--------
Runnable have only one method run:
	public void run();
	
	Runnable r = new MyRunnable(); --> 1
				 Lambda Expression --> 2
				 Method Reference  --> 3
		use any way 
	Thread t = new Thread();
	t.start();
	
	Runnable interface run method internally refers Test class m1 method
	Runnable r = Test::m1;
	
Constructor Reference by Double Colon Operator:
-----------------------------------------------
--> Arguments type must match
Class Sample{
	Sample(){
		sysout("Sample constructor ");
	}
}
interface Intref{
	public Sample get();
}
By Lambda Expression:
	Class Test{
		psvm(){
			Intref i = () -> { Sample r = new Sample();
								return r;
							}
			i.get();
			}
		}
By Constructor Reference:
	Class Test{
		psvm(){
			Intref i = Sample::new;
			Sample s = i.get();
			}
		}

---------		
Streams:
---------
Difference between IO and Streams:
Streams related to Collection objects --> Process the objects from the collection
Group of objects as a single entity
java.io.Streams meant for representing data wrt to file io operation

Difference between Collections and Streams:
--> If we want to represent a group of object as a single entity we go for Collection
--> If we want to process objects from the collection then we can go for Streams concept

Stream s = c.stream();
			c -> Any Collection Object
			stream() --> this methid present in Collection interface as default method 
	Stream --> is a interface present in Java.util.Stream package
	
	1) Configuration
		--> Filter Mechanism
				If we want to filter elements from the collection based on some boolean condition, then we should go for filtering
			    We can configure Filter by using filter method of Stream interface.
				public Stream filter(Predicate<T> t)
					Predicate<T> t --> can be boolean valued function or Lambda Expression
		--> Map Mechanism
				If we want to create a seperate new objec for every object present in the Collection based on some function then we should go for mapping mechanism.
				Can implement mapping by using map() method of Stream interface.
				public Stream map(Function<T, R> t)
				Stream s1 = c.stream().map(i -> i * i);
	2) Processing
		1) Processing by collect() method:
			This method collects elemets from the stream and added to the specified Collection
			
		2)	Count() --> long
 		3) Processing by sorted() method: 
			--> Wd can use sorted() method to sort elemets inside stream.
			--> We can sort either based on default natural sorting order or have on our own Customized Sorting order Specified by comparator Object
				sorted() --> for default natural sorting order
				sorted(Comparator t) --> For customized sorting order.
		 4) Min() and Max() --> here the list should be sorted for both Min and Max
		 5) forEach() --> It won't return anything 
			--> this method won;t return anything
			--> this method can take Lambda Expression as argument and apply that Lambda expression for each element present in Stream
		  6) toArray()	
			 --> We can use toArray() method to copy elements present in the stream into specified array
Stream of() method:
			 --> We can also apply stream for group of values and for arrays
			 1) For group of values
				 Stream<Integer> s = Stream.of()
				 
Summary Stream:
----------------
1) Purpose
To process the elements present in the collection 
2) Stram --> java.util.Stream
		Stream s = c.stream();
			stream() method present in Collection interface so stream method available in every collection class
3) filter(Predicate<T> t)
4) map(Function<T, R> f)
5) collect
6) count
7) sorted 	
	sorted(Comparator c)
8) Min(Comparator) and Max(Comparator)
9) toArray
10) forEach
Streams concept is not only applicable for Collections but also applicable for some group of values or arrays
Stream.of() --> Stream interface

1) Lambda Expression
2) Functional Interface
3) Static methods inside interfaces
4) Default methods inside interface
5) default predefined builtin FunctionInterface
	Predicate<T> boolean valued function "test"
6) Function<T, R> "apply"
7) Cunsumer<T> "accept"
8) Suppler<R> "get" 
9) Method Reference and Constructor reference by using double colon operator 
	Instance method ObjRef::methodNAme
	Static method className::methodNAme
10) Streams
11) Date and Time (API) Joda-Time API
Date, Calendar, TimeStamp until 1.7 these classes are that much convenience to use wrt performance and convenience
	--> To handle date and time values effectively
	LocalDate date = LocalDate.now() represent current date
	LocalDate is a class
		--> getDayOfMonth()
		--> getMonthValue()
		--> getYear()
	
	LocalTime time = LocalTime.now() --> to get current time
	java.time package
		--> getHour()
		--> getSecond()
		--> getNano()
		--> getMinute()
	LocalDateTime
To handle both date and time then use "LocalDateTime"
12) Period to represent quantity of time 
	how many months
	how many years
13) Year
14) ZoneId class: used to represent zone
15) ZoneDateTime

How to Remove key value pairs or Entries from HashMap in Java 8:
------------------------------------------------------------------
removeIf method is used to remove values from HashMap
Link:
http://javarevisited.blogspot.in/2017/08/how-to-remove-key-value-pairs-from-hashmap-java8-example.html#axzz4qdAf8nAx

priceMap.values().removeIf( d -> d.compareTo(Double.valueOf(39.00)) > 0);
priceMap.entrySet().removeIf( e -> e.getValue().compareTo(Double.valueOf(39.00)) > 0);


Can we make Default method static in Java? (http://www.java67.com/2017/08/java-8-default-methods-faq-frequently-questions-answers.html)
--------------------------------------------
Link: http://www.java67.com/2017/08/java-8-default-methods-faq-frequently-questions-answers.html#ixzz4rmJTZtDC

No, You cannot make default method static in Java. If you declare static method and default together, the compiler will complain saying "illegal combination of modifiers: static and default".
Example: 
	interface Finder{
		static default void find(){
			sysout("HI")
		}
	}
	Error: illegal combination of modifier and static
	
Can default method override equals(), hashCode() or toString() from Object class?
----------------------------------------------------------------------------------
interface Parser{ 
	@Override default String toString()
	{ 
		return ""; 
	} 
} Compile time error : "default method toString in interface parser overrides a member of java.lang.Object"

How to Remove key value pairs or Entries from HashMap in Java 8?
----------------------------------------------------------------
Link: http://javarevisited.blogspot.in/2017/08/how-to-remove-key-value-pairs-from-hashmap-java8-example.html

Map<String, String> map = new HashMap<String, String>();
map.put("a", "b");
map.put("b", "c");
map.put("c", "d");

map.keySet().remove("a");
map.keySet().removeIf(e -> e.equals("b"));
map.entrySet().stream() .forEach(e-> System.out.println(e.getKey()+" : "+e.getValue()));



--> Lambda Expressions
--> Functional Interfaces --> to invoke or to call lamdba experssion we should go for functional interfaces
		--> Functional Interface W.R.T Inheritance
--> Default methods in Interface
		--> Default methods with respect to Inheritance
--> Static methods in Interface
		--> Interface static methods wrt Overriding
--> Predefined Functional Interfaces
	--> Predicate
	--> Function
	--> Consumer
	--> Supplier
--> Method reference and Constructor reference by Double colon (::) operator
--> Streams API
	 --> to perform bulk operation is easily to write readable concise code.
--> Date and Time API ( Joda API ) 
	 --> Introduced by joda.org
	 
Peek and Skip:
https://www.youtube.com/watch?v=oqB91V9QVK0
Skip:
IntStream.of(1,23,4,8,9)
		 .skip(2)
		 .filter(i -> i > 5)
		 .Collect(Collectors.toList());
Output: 8, 9		  

Peek:
Stream.of("One", "Two", "Three")
	  .filter(i -> !i.equals("One"))
	  .peek(i -> System.out.println(i)) --> which prints the results
	  .collect(Collections.toList());
And use peek before terminal operation... mainly used for logging	  
	  
