Overriding:
--------------
Exceptions:

1) Parent: void m1() throws Exception
   Class : void m1()
	
	Valid
   
2) void m1() 
   void m1() throws Exception
   Invalid
   
3) void m1() throws Exception
   void m1() throws IOException
   Valid
   
4) void m1() throws IOException
   void m1() throws Exception
   In-Valid 
 
5) void m1() throws IOException
   void m1() throws FileNotFoundException, EOFException
   Valid
   
6) void m1() throws IOException
   void m1() throws EOFException, InterruptedException
   In-Valid
   
7) void m1() throws IOException
   void m1() throws ArthameticException, NullPointerException, ClassCastException
   Valid
   
   --> If child class method throws any checked exception compulsory the parent class method should throw same checked exception or its "Parent" otherwise we will get compile time error.
   
   --> There are no restrictions for unchecked exceptions Runtime Exception
   
   
   Exception --> checked
		InterruptedException
		IOException
			FileNotFoundException
			EOFException
   Runtime Exception--> Unchecked exception
		NullPointerException
		ClassCastException
		ArthameticException
		Error
		VirtualMachineError
		OutOfMemoryError
		
		Overriden method --> parent
		Overring method  --> child
		
Overriding with respect to static methods:
-->Class level method we cannot modify object level method

Static methods are class level method 
instance methods are object level methods	
--> We cannot override a class level method with object level.
--> We cannot override a static method as non-static method otherwise we get compile time error.
Exception: Case 1
class P{
public static void m1(){}
}
class C extends P{
public void m1(){}
}
m1 in c cannot override m1() in p; overriden method is static 

Exception: Case 2:
--> Simillarly we cannot a non-static method as static

class P{
pulbi void m1(){}
}
class C extends P{
public static void m1(){}
}
compile time error m1() in C cannot override m1() in p overriding method is static.

Case 3: If both parent and child class methods are static then we won't get any compile time error. It seems overriding concept applicable for static method but it is not overriding but it is method hiding  
class P{
public static void m1(){}
}
class static C extends P{
public static void m1(){}
}

method resolution JVM based on runtime object
Method Hiding:
All rules of method hiding are exactly same as overriding except the following differences

Method Hiding:
--> Both parent and child class methods should be static 
--> In method hiding Compiler is responsible for method resolution based on reference type.
--> It is also know as compile time polymorphism or early binding
Overriding:
--> Both parent and child class methods should be non-static
--> JVM is always responsible for method resolution based on runtime object.
--> It is also know as runtime polymorphism or dynamic polymorphism or late binding.

Varargs:
We can overrovide with another varargs method only if we are trying to override normal method it will become overloading but not overriding

Overriding w.r.t variables:
--> Overriding concept applicable only for methods but not for variables. Variable resolution is always takes care by reference types.
--> Same for instance or static variable .. value is always same.

class P{
	int x = 888;
}
class C extends P{
	int x = 999;
}

P p = new P();
sop(p.x) 888

C c= new C();
sop(c.x); 999 

P p= new C();
p.x 888

 P - nonstatic P-static     P-non-static P-static
 c - nonstatic C-non-static C-static     C-static
 888  same for all
 999
 888
 Variable resolution always takes care by compiler based on reference type irrespective of weather the variable is static or non static .
 
 Differences between overloading and overridings
 
 https://www.youtube.com/watch?v=SrveBABPMFc&t=5884s
 
 
 https://www.maketecheasier.com/email-notification-user-login/
http://cs-fundamentals.com/java-programming/method-overloading-in-java.php
http://docs.oracle.com/javase/specs/jvms/se7/jvms7.pdf
think java (how to think like a computer scientist) pdf

Third rule in java:
------------------
interface I{
	default boolean equals( Object obj ){--> 
	
	}
}

Example:
Interface I{
default void show(){
	sysout("I");
}
}
Interface J{
default void show(){
	sysout("J");
}
}
class A implements I, J{
	show(){
	}
	//Now 
}
--> Here are implementing both interfaces which contains same methods then class A must override the common method 
--> Now when we try to class a.show() the Class A's show method is called instead I or J .. since class is given higher priority than interfaces 
--> We cannot provide same method name for default
	Example:
		default boolean equals(Object obj){
		}
	--> Here equals method is already provided by Object class so not allowed.

Difference between C c = new C() and P p = new C():
-------------------------------------------------------
--> 1) If we know exact runtime type of object then go for:
		C c = new C();
	2) 	By using child reference we can call both parent an dchild class methods.
	3) We can use child reference to hold only for that particular child class object only.
--> 1) If we don't know exact runtime type of object then we should use this approach. 
		P p = new C();
	2) By using parent reference we can call only methods available in parent class and child specific methods we cannot call.
	3) We can use parent reference to hold any child class object.
		Example: 

Java Method Overloading and Widening:
------------------------------------
For an example:
--> If you have two overloaded method signatures as aMethod(short x) and aMethod(long x) and you make a call by passing a fixed value (literal) 10 to method aMethod as aMethod(10), aMethod(long x) will be called because Java by default treats integer literals int and JVM does not find aMethod(int x) and the next wider signature is aMethod(long x); therefore, JVM picks aMethod(long x).

--> If we use primitive and wrapper classes then primitive type given higher priority since 

Widening beats boxing because autoboxing feature was added to Java in J2SE 5.0 release. So, Java 5's designers decided that pre-existing code should not break and it should function the way it used to. Since widening capability already existed; therefore, an overloaded method gives preference to widening over boxing.

Example:
public static void main (String[] args)
  {
    int l = 5;
    aMethod(l);
  }
 
  static void aMethod (Integer x)
  {
    System.out.println("int version: " + x);
  }
 
  static void aMethod (long x)
  {
    System.out.println("long version: " + x);
  }
  
Internal rule for resolving the method call : 
	****In Overloading exact match is going to get highest priority****
In overloading method resolution,
	--> Compiler is always going to check exact matched method.
		--> If exact matched method is there then it will execute 
		--> If exact matched method is not there then compliler wont raise compile time error immediately. Compiler promote's this 'Char' to next level and check is there any metched method or not. 
			i,e. 
				char--> int 
		--> If yes it will execute  or get chance to execute.
		--> If method not matched after promoting next level then compiler again promo to next level 
			i,e. 
				char--> int --> long
			
		--> this process continues untill all possible promotions still method not matched then we will get compile time error	
			char --> int --> long --> float --> double (Here byte and short not promoted because of the range which does not fit either in short or byte)
			byte --> short --> int --> long --> float --> double
				
			10.5--> by default "double" type
			
Example Case 1:
	public void m1(int i)
		sysout(int arg)
	public void m1(float i)
		sysout(float arg)
	
	
	t.m1(10); int arg
	t.m1(10.f); float arg
	t.m1('a'); int arg --> char promoted to next level that is "int"
	t.m1(10l); float arg --> long promoted to next level that is "float"
	t.m1(10.5); double --> here we get cannot find symbol error since there is no next level promoting for duble and no method with m1(argument type double )
  
Example case 2:
	m1(String str){
		sysout("String version")
	}
	m1(Object obj){
		sysout("Object obj")
	}
   
    t.m1(new Object()); --> Object version 	  
  
	If the work is going to complete in child level then no need to go for parent level
		Object(Parent) --> String( Child )
		null is valid for String arg and Object arg 
			Example: collector --> poen 
			
		Child is getting higher priority than parent. So, here String arg is called.
Note: While resolving overloaded methods compiler will always gives the precedence for child type argument when compared with parent type argument
		
Here both String and StringBuffer both are in the same level for object that is 
 *  Object --> String
 *  Object --> StringBuffer
 *  So it gives error saying ambiguity	
Example Case 3:
Show(String str){
 System.out.println("String");
}
public void Show(StringBuffer str){
 System.out.println("StringBuffer");
}		
		
Example Case 4:

public void m1(int i, float j){
	System.out.println("int float");
}
	
public void m1(float j, int i){
	System.out.println("float int");
}

In general var-arg method will get least priorty that is if no other method matched then only var arg method will get chance it is exactly same as default case inside a switch  

In overloading object compiler is respo to perform method resolution based on reference type.		
	
Overriding:
-----------	
In overriding method resolution is always based on runtime object. dymanic, late, runtime polymorphism
	
	P p = new P();
	p.marry(); -> Parent marry
	c c = new C();
	c.marry(); ->child marry 
	P p = new C()
	p.marry --> child marry method
	
	In overriding you have to decide compiler and runtiime role
	
		compiler--> systactically here we are calling marry method which is of type P type and marry method is present in P class
		runtime--> runtime object is parent or child
		if it is child object if it is overriding marry method then based on runtime object child class marry mehtod will be executed .
	
	method name, arg name, return types, modifier, throws, access modifier
Rules for overriding:
	Method signature:
	--> Method signature same .. method name and method parameters
	Return Types:
	--> In overriding return types must be same --> but this rule is applicable untill 1.4 version only.. from 1.5 version onwards covariant return types allowed that is the child class method retun type need not be same with parent class method return type
	--> Its child type also allowed
	
		--> Covariant Return Type:
				Example:
					class p{
						public Object m1(){
							return null;
						}
					}
					 class C extends P{
						public String m1(){
							return null;
						}
					 }
		Parent --> Object as return type
		Child --> we can take Object or Object|String|StringBuffer...
		
		Child method return type should be equal to parent method return type or its sub type
		
		***IMP***:
			Covariant concept is only applicable for Object types but not for primitive type
				Parent --> double primitive
				Child  --> int primitive
						---------ERROR-------
					m1(double)-->parent
					m1(int) --> child error		
		Modifiers:
		-->	Parent class private methods not available to the child and overriding concept not applicable for private methods
			But we can exactly define the method in child class it is valid but not overriding
		--> Final: We cannot override parent class final methods in child classes. If we are trying override we will get compile time error
			cannot override method declared final
		--> abstract: parent class abstract mehtod we should override in child class to provide implementation
			abstract class P{
				public abstract void m1(){}
			}
			class C extends P{
				public void m1(){}
			}
			
			Parent--> abstract class
			child --> non abstract class
		Now reverse
			Parent--> non abstract class
			child --> abstract class
			We can override non abstract method as abstract 
			public P{
				public void m1(){}
			}
			abstract class C extends P{
				abstract void m1();
			}
			The main advantage:
			Of this approach is we can stop the availability of parent class method implementation in the next level child classes 
			
			
			If we don't want super class implementation to child and child class do not know how to override or provide logic for the method then declare the child class method as abstract.
			 
			Parent method :   final		non-final	abstract(non-abstract)	synchronized 		native 		strictfp		
			
			
			Child mehtod  :   non-final  final       non abstract(abstract)	non-synchronized	non-native	non-strictfp
			
			Valid		  :	   no        yes          yes                      yes               yes            yes		 
		
		Scope:
			We cannot reduce the scope from private to child... compiler error acting to assign weaker access privilages 

