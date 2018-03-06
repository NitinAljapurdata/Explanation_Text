https://www.youtube.com/watch?v=V2jFpFGAwcU&list=PL0e0_xCoqAFEoJ-k5z3z4BFMqlJGeUvBq&index=40

Difference Between Web Server and application Server:

Log file analyzer:
Link:
	https://dzone.com/articles/7-log-management-tools-java
Open source log analyzer :
	logstash:
		https://www.elastic.co/downloads/logstash
	Installing steps:
		https://www.elastic.co/guide/en/logstash/current/installing-logstash.html
	https://blog.terminal.com/elk-logs-analysis-part-iii/
	
	Kibana: 
		Its a UI for log analysis
			https://www.elastic.co/products/kibana
			
			Prefix
			http://support.stackify.com/hc/en-us/articles/211497443-How-to-Enable-Java-Profiling-with-Prefix

Difference Between Inheritance and Composition:
-----------------------------------------------
--> Composition allows resuse of code without extending it. Where as for inheritance we must extend the class to reuse the code or funtionality.
--> We can reuse the code even if the class is final in case of Composition. where as for inheritance we cannot extend final classes.
--> Using composition we can resuse multiple classes. Whereas for Inheritance we can extends atmost only one class we cannot multiple classes since java does not support multiple inheritance.
--> Inheritance breaks encapsulation because any change in the super class will effect the sub class, since sub class depend upon the super class behaviour.

Java Stack: Article http://www.journaldev.com/13401/java-stack
-----------
Java Stack is a legacy Collection class.
Stack extends Vector implempts RandomAccess interface.
Stack supports LIFO ( Last in First Out ).
Stack supports only 5 Operations.
1) boolean empty()
2) E peek(): looks at the object at the top of this stack.
3) E pop(E item): removes the object at the top of this stack.
4) E push(E item): pushes an item onto the top of this stack.
5) int search(Object o): returns 1 bases postion where an object is on the statck.

Fixing Unsupported major.minor version 52.0 Error in Java:
---------------------------------------
	Article:

http://javarevisited.blogspot.com/2015/05/fixing-unsupported-majorminor-version.html#ixzz4eiChMYaB

Unsupported major.minor version 52.0 comes when you are trying to run a class compiled using Java 1.8 compiler into a lower JRE version e.g. JRE 1.7 or JRE 1.6. Simplest way to fix this error is install the latest Java release i.e. Java 8 and run your program. I

If we cannot upgrade to Java 8 or compile for lower JRE version using java -target 1.6 option

Exampl: javac -target 1.4 HelloWorld.java


Read more: http://javarevisited.blogspot.com/2011/01/how-classpath-work-in-java.html#ixzz4eiIzMAh0

-->ClassNotFoundException
is an Exception and will be thrown when Java program dynamically tries to load a particular Class at Runtime and don’t find that on Java classpath due to result of Class.forName() or loadClass() method invocation.

-->NoClassDefFoundError comes when a particular class was present in Java Classpath during compile time but not available during runtime on Classpath in Java.

Difference in String pool between Java 6 and 7:
----------------------------------------------
Article:
http://javarevisited.blogspot.com/2016/07/difference-in-string-pool-between-java6-java7.html#ixzz4eoTWG2hT

The String pool is implemented using a HashMap in Java and default size of the table in Java 6 was 1009

Due to this relocation of String pool from PermGen memory space to heap space, the String.intern() method, which is used to intern a String object and store inside string pool for further reuse has now become even more useful. You can intern a large number of String than before. You are only limited by your JVM heap size as far as String pool goes.


In summary here, is the important difference in String pool in Java 6 and 7:
-->String pool is relocated to Java heap space from PermGen space.
-->The default size of String pool is increased to 60013 entries from 1009 in Java 6.
-->The -XX:StringTableSize JVM option is provided to specify the size of String pool. 

Why Should I Write Getters and Setters?
---------------------------------------
Link: https://dzone.com/articles/why-should-i-write-getters-and-setters?oid=facebook&utm_content=buffercbe8f&utm_medium=social&utm_source=facebook.com&utm_campaign=buffer
I understand, but generally, we do not write anything in getters/setters. We just return and set the field, which is same as exposing a field as public. So why are you saying all of this?

To answer this question, I say by writing getters/setters, we create a provision to add any validation method in the future, currently, there is no validation, but if anything goes wrong in the future we just add validation logic in the setter.

The main difference between making a field public vs. exposing it through getters/setters is holding control over the property. If you make a field public, it means you provide direct access to the caller. Then, the caller can do anything with your field, either knowingly or unknowingly. For example, one can set a field to a null value, and if you use that field in another method, it may blow up that method with a null pointer exception.

But, if you provide a getter/setter, you provide them indirect access while taking full control. The only way to set a value is through setter, and you get a value through a getter, so now you have exactly one entry and one exit point for your field, as getter/setters are methods, which allows blocks of code, so you can do validation checks on them! The object takes the decision whether you should set the caller value or not. The same applies to a getter method — you can take the decision to return the actual reference or clone it and return the same to the caller.

Why can other methods be “static” but a constructor cannot?
-----------------------------------------------------------
Link: http://stackoverflow.com/questions/7780406/why-can-other-methods-be-static-but-a-constructor-cannot
Simply to say, "A java constructor is always non static" because,

The purpose of the constructor is only to initialize/construct the object, and to make inheritance possible. To do these we need to use the two useful java keywords (cum non-static variables) such as this and super. We will use 'this' to initialize the object. We/Java will use super(ofcourse super()) to invoke super class constructor so that super object(or Object class) created first then the child object(hence the inheritance) If the constructor is static then we cant use that two keywords(non-static variables) inside the constructor(As we know non-static stuff cant be referenced from static context)

"So java constructors should not static".


Whats actually happening at compile time and runtime:
-----------------------------------------------------
https://coderanch.com/t/473487/java/Whats-happening-compile-time-runtime


Sort an Employee Object list first by salary and if salaries are equal, then by name:
-------------------------------------------------------------------------------------
Link: http://stackoverflow.com/questions/35969967/sort-an-employee-object-list-first-by-salary-and-if-salaries-are-equal-then-by

Comparable --> CompareTo()
Comparator --> Compare(Obj1, Obj2)

CompateTo(Object obj1){
	Employee e1 = (Employee)Obj1;
	int compareSal = Integer.compare(this.sal, e1.getSalary());
	if(compareSal == 0){
		return name.compareTo(e1.getName());
	}
	return compareSal;
}

Binary Search:
-----------------
Recursive Binary Search Algorithm in Java - Example Tutorial
Read more: http://javarevisited.blogspot.com/2017/04/recursive-binary-search-algorithm-in-java-example.html#ixzz4f5MYo0BT

Difference between State and Strategy Design Pattern in Java:
---------------------------------------------------------------
Read more: http://javarevisited.blogspot.com/2014/04/difference-between-state-and-strategy-design-pattern-java.html#ixzz4f5ONKCh6

2 solution of java.lang.OutOfMemoryError in Java:
---------------------------------------------------
http://javarevisited.blogspot.in/2011/09/javalangoutofmemoryerror-permgen-space.html:


Memory Fundamentals - part 1 of Java Memory Management:
------------------------------------------------------
Link: https://www.youtube.com/watch?v=ckYwv4_Qtmo

Very thread has it's own stack..
	Statk is LILO
	
	Objects are stored physically in Heap.
	variables that hold the objects are just reference of that object.
	Local variables are stored on the stack.
	
	Pass by value and Pass by reference
	
Immutable: 
-----------
Link: http://www.javapractices.com/topic/TopicAction.do?Id=15

A class can have mutable object as a field. There are two possible ways that this mutable object field can change:
--> the native class can change it's state.
--> it's state can be changed by callee.

https://www.youtube.com/watch?v=CdAmS9H93q4
Garbage Collection:
-------------------
Link: https://www.youtube.com/watch?v=XrNgF2sbhGQ&t=331s
Java 6:
To Store information related to class .. we store that in PermGen place.. and this space is never garbage collected.
If PermGen runs outofmemory that means we have large amount of clases or plenty if interim string.. This outofmemory is not due to memory leaks in the code.
So, whenever we redeploy the code into the server... new metadata of the classes created even it's already exisits ... and existing metadata becomes un tracable..however in PermGen never GC is done.. so when we redeply multiple times it may run outofmemory so either increase size or restart the server..

Java 7: Change in PermGen.... the interm strings are no longer stored in PErmGen..are moved to Heap
Java 8: 
-->they removed the PermGen space. instead created MetaSpace where metadata of classes are placed. 
-->MetaSpace is seperate area of memory it is not part of the heap..
-->so maximum available space for MetaSpaces is that of your system space..
-->java 8 whenever we redeploy the code , first it will remove all the older metadata classes and then add new metadata... each time we redeploy... earlier we are not deleting the older metadata of classes.

So, S1.. are survival space


Big O Notation:
---------------
Link: https://dzone.com/articles/learning-big-o-notation-with-on-complexity?oid=facebook&utm_content=buffer40689&utm_medium=social&utm_source=facebook.com&utm_campaign=buffer

O(1)
public boolean isFirstNumberEqualToOne(List<Integer> numbers) {
  return numbers.get(0) == 1;
}
O(1) represents a function that always takes the same take regardless of input size.

O(n)
public boolean containsNumber(List<Integer> numbers, int comparisonNumber) {
  for(Integer number : numbers) {
    if(number == comparisonNumber) {
      return true;
    }
  }
  return false;
}
O(n) represents the complexity of a function that increases linearly and in direct proportion to the number of inputs. This is a good example of how Big O Notation describes the worst case scenario as the function could return the true after reading the first element or false after reading all n elements.

O(n2)
public static boolean containsDuplicates(List<String> input) {
  for (int outer = 0; outer < input.size(); outer++) {
    for (int inner = 0; inner < input.size(); inner++) {
      if (outer != inner && input.get(outer).equals(input.get(inner))) {
        return true;
      }
    }
  }
  return false;
}
O(n2) represents a function whose complexity is directly proportional to the square of the input size. Adding more nested iterations through the input will increase the complexity which could then represent O(n3) with 3 total iterations and O(n4) with 4 total iterations.

O(2n)
public int fibonacci(int number) {
  if (number <= 1) {
    return number;
  } else {
    return fibonacci(number - 1) + fibonacci(number - 2);
  }
}
O(2n) represents a function whose performance doubles for every element in the input. This example is the recursive calculation of Fibonacci numbers. The function falls under O(2n) as the function recursively calls itself twice for each input number until the number is less than or equal to one.

O(log n)
public boolean containsNumber(List<Integer> numbers, int comparisonNumber) {
  int low = 0;
  int high = numbers.size() - 1;
  while (low <= high) {
    int middle = low + (high - low) / 2;
    if (comparisonNumber < numbers.get(middle)) {
      high = middle - 1;
    } else if (comparisonNumber > numbers.get(middle)) {
      low = middle + 1;
    } else {
      return true;
    }
  }
  return false;
}
O(log n) represents a function whose complexity increases logarithmically as the input size increases. This makes O(log n) functions scale very well so that the handling of larger inputs is much less likely to cause performance problems. The example above uses a binary search to check if the input list contains a certain number. In simple terms, it splits the list in two on each iteration until the number is found or the last element is read. This method has the same functionality as the O(n) example — although the implementation is completely different and more difficult to understand. But this is rewarded with a much better performance with larger inputs (as seen in the table).


Java Pass by value OR Pass by reference:
----------------------------------------
Java is pass by value:
-->Primitive Variable:
When we pass a variable to a method .. we are actually passing a copy of that value.
Example:
public static void main(String[] args){
	int localValue = 5;
	calculateValue(localValue);
}
public static void calculateValue(int calcValue){
	calcValue = 10 * calcValue;
}

Stack:
localValue = 5 --> it remains 5
calcValue = 5 --> New copy is created. --> after calculateValue method this will become 50

SO, variable in the method is always a copy of the value passed into it. it does not matter what the variable name is.
So, Passing variable into method in java is always done by creating a copy of a variable. this is known as passing variable by value.

--> Object:
When an object is passed to a method as a parameter a copy of the variable on the stack containing the reference of the object is passed by value.

Final: 
only the reference of which object variable pointing to cannot be changed.


http://www.java67.com/2015/10/java-program-to-find-repeated-words-and-count.html#at_pco=smlwn-1.0&at_si=5906bd97d72ff981&at_ab=per-2&at_pos=0&at_tot=1

toString():
----------------
Always implement or override toString().. the default toString of object which outputs the classname+@+hexadeciaml hashcode of object which is not in a readable format.

Cuncurrency package
Syschronization
Serialization

Marker Interface:
----------------
We can create our own marker interface. It does not have any method in it.. it's a blank interface..
We use marker interface .. just too ensure that the has permission to do so.

example:

interface PrintPermission{
}

class Myclass implements PrintPermission{

public void show(){
	System.out.println("Print Me");
}

so here i can check where this class Myclass has permission to call method show..
i.e,
Myclass class = new Myclass()

if(class instanceOf PrintPermission)
	show();
	
	Servialization:
			That we can give permission to that, you can save the state of the object.
}

Focus on below:
1) Java8 Fetures:
2) Java Cuncurrency
http://howtodoinjava.com/java-concurrency-tutorial/
https://www.javacodegeeks.com/2015/09/concurrency-fundamentals-deadlocks-and-object-monitors.html
https://www.javacodegeeks.com/2015/09/introduction-to-threads-and-concurrency.html
https://www.javacodegeeks.com/2015/09/the-java-util-concurrent-package.html
https://www.youtube.com/watch?v=f4QZ12wMQO8&index=1&list=PLd3UqWTnYXOk0y_HFp2r1eMW_lhZ7yP4w

Docker: https://prakhar.me/docker-curriculum/
-------
an open-source project that automates the deployment of software applications inside containers by providing an additional layer of abstraction and automation of OS-level virtualization on Linux.

10 Things You didnt know about java:
-----------------------------------
Link: https://blog.jooq.org/2014/11/03/10-things-you-didnt-know-about-java/
Quirky enough? Let’s consider the following two pieces of code:
i += j;
i = i + j;
Intuitively, they should be equivalent, right? But guess what. They aren’t! The JLS specifies:

A compound assignment expression of the form E1 op= E2 is equivalent to 
	E1 = (T)((E1) op (E2)), 
where T is the type of E1, except that E1 is evaluated only once.

byte b = 10;
b *= 5.7;
System.out.println(b); // prints 57

https://blog.jooq.org/2013/10/08/java-auto-unboxing-gotcha-beware/	

zeroda

ParseInt and valueOf:
-------------------------
Link:
https://dzone.com/articles/hacking-the-integercache-in-java-9?oid=facebook&utm_content=buffer35db4&utm_medium=social&utm_source=facebook.com&utm_campaign=buffer
--> One can manipulate the IntegerCache which is used by valueOf ... this is not allowed in java 9.
Example:
Class<?> clazz = Class.forName("java.lang.Integer$IntegerCache");
Field field = clazz.getDeclaredField("cache");
field.setAccessible(true); 
Integer[] cache = (Integer[])field.get(clazz);
//Rewrite Integer Cache
for(){
	cache[i] = new Integer(new Random().nextInt(cache.length))
}
Here we are manipulating the cache..

Overloading:
-------------
m1(int i){
}
m1(int... x){ --> var-args introduced in java 1.5
}
psvm(){
t1.m1(); 2nd --> vargargs zero or more arguments
t1.m(10,20) 2nd
t1.m1(10) 1st
}
--> In general "var-args" method will get least priority i,e. if no other method matched then only varargs method will get the chance it is exactly same as default case in side switch statement

-->In overloading,  Compiler is responsible to perform method resolution based on reference types , tuntime objects never play any role in overloading. 

Class.forName("MyClas") and new operator difference:
----------------------------------------------------
--> Class.forName() does not instantiate an object ( at leasst not an object of the class you are calling it for, it might instantiate a Class object). All it does is preload the class for the given name, allowing objects to be instantiated from it.

--> Here "MyClass" must be public and must have a no-arg constructor. And this restriction in case of using new operator.

Class.forName("").newInstance().


Instance Control Flow:
----------------------
Example: 
{
	sysout
}
Whenever we are creating an object in static control flow...then below flow

Whenever we are executing a java class :
--> Static control flow will be executed
--> In the static control flow if we are creating an object the following sequence of events will be executed .as part of instance control flow.
	--> Indentification of instance members from top to bottom
	--> Execution of instance variable assignments and instance blocks from top to bottom
	--> Execution of construction
for a every object creation this above flow is performed
--> Static control flow is one time activity which will be performed at the time of class loading. But instance control flow is not one time activity and it will be performed for "every object creation".
--> Object creation is the most costly operation if there is no specific requirement then it is not recommended to create object. 

Instance Control Flow in Parent to Child Relationship:
-----------------------------------------------------
First:
--> Identification of static members from parent to child from top to bottom.
--> Execution of static variables and static blocks from parent to child from top to bottom.
--> Execution of main method from "CHILD" class.
Next:
--> Identification of instance members from parent to child.
--> Execution of instance variables assignments and instance block only in parent class
--> Execution of parent constructor.
--> Execution of instance variables assignments and instance block in child class
--> Execution of child constructor.

Static execution order:  static control flow is happened at the begining only
---------------------
--> Identification of static members from top to bottom
--> Execution of static variable assignment and static blocks from top to bottom.
--> Execution of main method.
--> If a variable is just identified by the JVM and original value not yet assigned then the variable is said to be in "ReadIndirectly WriteOnly state"  
--> If a is in "ReadIndirectly WriteOnly state" then we cannot perform direct read but we can perform indirect read.
--> If we are trying to read directly then we get compile time error Illigal forward reference

After loading every driver class, we have to register driver class with drivermanager but inside datavase driver class there is a static block to perform this activity and we are not responsible to register explicitly.

Static Control flow in parent to child relationship:
--> Identification of static members from parent to child from top to bottom.
--> Execution of static variables and static blocks from parent to child from top to bottom.
--> Execution of main method from "CHILD" class.

Interaface and Abstract class Loopholes Part-1 || new vs Constructor:
----------------------------------------------------------------------
Link: https://www.youtube.com/watch?v=WyE3t9geWNY&index=1&list=PLd3UqWTnYXOm5UXbKfj8iZfWQNcLPL3HC
new: Responsible to create object
constructor: To initialize object
First "new" is executed , after that constructor.
class Student{
int rollno;
String name;
Student(String name, int rollno){
	this.name = name;
	this.rollno = rollno;
}
Student stu = new Student("abc", 10);
}
new --> object created with default values -
	--> name = null, int = 0;
Constructor--> name = abc , rollno=10

Child Object Vs Parent Constructor-1:
---------------------------------------
Whenever we are creating chilid class object automatically parent class constructor will be executed to perform initialization for the instance variable which are inherting from parent class.

Child Object Vs Parent Constructor-2:
--------------------------------------
--> Whenever we are creating child class object parent constructor will be executed but parent object is not created. But parent constructor will be executed for child purpose only. 
Class P{
P(){
	sop(this.hashCode());
}
}
class C extends P{
  C(){
	sop(this.hashCode());
  }
  
  C c = new C();
}
  
Need of Abstract class constructor-Part 4:
--------------------------------------------
--> For abstract class directly or indirectly we cannot create constructor.  
--> Abstract class can contain constructor.
--> To perform initialization for child class only.
--> code reusability

Part-5 || Abstract class vs Interface wrt constructor:
-------------------------------------------------------
--> 


------------------------------
Multithreading Enhancement:
------------------------------
Thread Group:
-------------
--> Common operation we can perform very easyly
--> A group of thread .. it can also contains sub group threads
--> Based on functionality we can group into a sinle unit which is nothing but thread group. that is thread group of threads 

Three main characters are there :
--> Main method
--> Main thread
--> Main thread group

Main method is called by main thread .. this main thread belongs to "main group".
Every thread group in java is the child group of "System group" either directly or indirectly. Hence System group acts as root for all thread groups in java.

Example:
	class Test{
		sysout(Thread.currentThread().getThreadGroup().getName()); --> Main
		sysout(Thread.currentThread().getThreadGroup().getParent().getName()); --> System		
	}
System Group contain system level threads:
--> Garbage Collector.(Finalizer)
--> Reference handler
--> Signal dispatcher
--> Attach listener

Diagram:
	Video1-1
Thread Group is a "Java" class present in java.lang package and it is the direct child class of object
Constructors:
	1)  ThreadGroup g = new ThreadGroup("FirstGroup");
	--> Creates a new thread group with the specified group name
	--> The parent of this new group is the group of currently executing thread.
	
	2) ThreadGroup g = new ThreadGroup(g, "SecondGroup");
	--> Creates a new thread group with the specified group name.
	--> The parent of this new thread group is specified parent group
	
	ThreadGroup g1 = new ThreadGroup("FirstGroup");
	sysout(g1.getParent().getName()); --> Main
	ThreadGroup g2 = new ThreadGroup(g1,"SecondGroup");
	sysout(g2.getParent().getName()); --> FirstGroup
	
	System
	   |
	Main
	   |
	FirstGroup
	   |
	SecondGroup
Methods of Thread Group:
1) String getName(): returns group name
2) int getMaxPriority(): returns max priority of thread group
3) void setMaxPriority(): to set maximum priority of thread group
	--> the default max priority for the thread and group is "10"
	
Example:
ThreadGroup g1 = new ThreadGroup("g1");
Thread t1 = new Thread(g1, "thread1");--> if we do not set any priority to thread then it will take default priority that is "5"
Thread t2 = new Thread(g2, "thread2");
g1.setMaxPriority(3);
Thread t3 = new Thread(g1, "thread3"); 
sysout(t1.getPriority()); --> 5
sysout(t2.getPriority()); --> 5
sysout(t3.getPriority()); --> 3
Threads in the thread grpup that already have higher priority wont be effected but for newly added thread this maxpriority is applicable

4) ThreadGroup getParent(): return parent grpup of current thread.
5) void list() --> prints information about "ThreadGroup" to console
6) int activeCount() --> to know active threads:--> number of active threads present in the threadgroup
7) int activeGroupCount()--> it returns number of active groups present in the current threadgroup
8) int enumerate(Thread[] t) --> 
   to copy all active threads of this group threads into provide thread array..this enumerate(thread[] t)... in this sub threadgroup threads also will be considered.
	Thread[] t = new Thread[10];
	groupThread.enumerate(t);
	for(Thread t1 : t){
		sysout(t.getName());
	}
9) int enumerate(ThreadGroup[] g):
	--> to copy all active sub thread groups into threadgroup array
10) boolean isDaemon()--> to check whether the threadgroup is Daemon or not
11) void setDaemon(boolean b)
12) void ineterrupt() --> to interrupt all waiting or sleeping threads present in the thread group
13) void destory() --> to destroy thredagroup and its sub threadgroups.

Diagram:
	Video1-2
	
	Example: TheadGroup system = Thread.currentThread().getThreadGroup().getParent();
			 Thread[] t = new Thread[system.activeCount()];
			 system.enumerate(t);
			 for(Thread t1 : t){
				t1.getName() + " : "+ t1.isDaemon()
			 }
			 
Java concurrency Lock:
------------------------
--> The problems with traditional synchronized keyword:
	--> We are not having flexibility to try for a lock without waiting 
	--> There is no way to specify maximum waiting time for a thread to get lock so that thread will wait until getting the lock which may creates performance problems, which may cause dead lock.
	--> If a thread releases a lock then which waiting thread will get that lock we are not having any control on this.
	--> There is no API to list out all waiting threads for a lock.
	--> the synchronized keyword compulsory we have to either at method or within the method and it is not possible to use across multiple methods
		To overcome these problems SUN people introduced java.util.concurrent.locks package in Java 1.5 version.
		
Lock --> Interface
ReentrantLock --> Class 
Lock :
 --> Lock object is similar to implicit lock aquired by a thread to execute synchronized method or synchronized block.
 --> Lock implementations most extensive operations than traditional implicit locks
 Important methods of Lock Interface:
 1) void lock() --> We can this method to acquire a lock. If lock already available then immediatly current thread will get that lock. If the lock is not already available then it will wait until getting the lock it is exactly same behaviour of traditional synchronized keyword.
 2) boolean tryLock() --> Try lock to acquire the lock without waiting. 
						  If the lock is available then the thread acquires that lock and returns true. 
						  If the lock is not available then this method returns false and continue its execution without waiting in this case thread never be waiting state.
						  if(l.tryLock()){
							Perform safe operation
						  }else{
							Perform alternative operations
						  }
 3) tryLock(long time, TimeUnit unit)--> If lock is available then the thread will get the lock and continue its execution.
										 If the lock is not available then the thread will wait until specified amount of time. Still if the lock is not available then thread can continue its execution.
				TimeUnit: timeunit is an ENUM present in java.util.concurrent package
					enum TimeUnit{
						NANOSECONDS
						MICROSECONDS
						MILLISECONDS
						SECONDS
						MINUTES
						DAYS
						HOURS
Void lockInterruptbily()
void unlock: to releases the lock 
		To call this method compulsory current thread should be owner of the lock. Otherwise we will get runtime exception saying IllegalMonitorStateException 

		Life doesn't change bcoz you change "CONTENT" of ur life. Life changes bcoz of you change "CONTEXT" of ur life.
						  
ReentrantLock:
	It is the implementation class of Lock interface and it is the direct child class of object
	
	ReenatrantLock l= new ReentrantLock();
	l.lock(); --> hold count = 1
	l.lock(); -->            = 2
	l.lock(); -->            = 3
	-----------------------------------
	l.unlock() --> hold count = 2
	l.unlock() -->            = 1
	l.unlock() -->            = 0
			--> lock is released
    Reentrant means a thread can acquire same lock multiple times without any issues. Internally reentrant lock increments threads personal count whenever we call lock method and decrements counter whenever thread calls unlock method and lock will be released whenever count reaches zero.
 Constructors:
	1) ReenatrantLock l = new ReentrantLock();
		--> creates an instance reentrant lock
		
	2) ReenatrantLock l = new ReentrantLock(boolean fairness);
		--> creates reentrant lock with the given faireness policy
		--> If faireness is true then, longest waiting thread will get the lock if it is available. that is it follows FIFO
		--> If faireness is false then, which waiting thread will get the change we cannot expect
		
		--> the default value for fairness is false.
	which of the following declarations are equal 
	a) ReentrantLock l = new ReenatrantLock();
	b) ReentrantLock l = new ReenatrantLock(true);
	c) ReentrantLock l = new ReenatrantLock(false);
	d) All the above
	a and c 
	
Important methods of ReenatrantLock:
Lock(I)
  |
  |
ReenatrantLock(C)
int getHoldCount()--> returns number of holds on this lock by current thread
boolean isHeldByCurrentThread()--> returns true if and only if lock is hold by current thread
int getQueueLengh()--> returns number of threads waiting for the lock
Collection getQueuedThreads()--> returns collection of threads which are waiting for the thread.
boolean hasQueuedThreads()--> returns boolean has queued threads. returns true if any thread waiting to get the lock
boolean isLocked()--> returns true if the lock is acquired by some thread
boolean isFair()--> returns true if the fairness policy is set with true value.
Thread getOwner() --> returns the thred which acquired the lock. ( owner of the lock )
	ReenatrantLock l = new ReentrantLock();
	l.lock();
	l.lock();
	sysout(l.isLocked());
	sysout(l.isHeldByCurrentThread());
	sysout(l.getQueueLengh());
	l.unlock();
	sysout(l.getHoldCount());
	sysout(l.isLocked());
	l.unlock();
	sysout(l.isLocked());
	sysout(l.isFair());
	
ThreadPools:
-------------
--> Creating a new thread for every job may create performance and memory problems.
--> To overcome this we should go for thread pool
--> Threadpool is a pool of already created thread reday todo over job.
--> Java 1.5 version introduces threadpool framewrok to implement threadpools.
--> ThreadPool framewrok also known as ExecutorFramework.

ExecutorService service = Executores.newFixedThreadPool(3);
We can submit a runnable job by using a submit() 
service.submit(job)
We can shutdown executor service by using shutdown 
service.shutdown()

--> In the case of Runnable job thread wont return anything after completing the job.
--> If a thread is required to return some result after execution then we should go for Callable interface
	--> Call method --> Callable interface contains only one method call()
	public Object call()throws Exception{
	}
--> If we submit callable object to executor then after completing the job thread returns an object of the type Future. that is future object can be used to retrive the result from callable job.

ThreadLocal:
--> threadlocal class thread local variables
--> Threadlocal class maintains values per thread bases
--> Each threadlocal object maintains a separate value like userid, transaction id etc., For each thread that access that object.


ExecutorFramework:
--------------------
Executor (Interface)
	--> public void execute(Runnable run)
	--> Simple interface that supports launching new "tasks"
	--> Tasks implement the Runnable interface... Represents a command that can be executed.
	Runnable interface
       --> public void run()	
ExecutorService (Interface)
     --> which manages the life cycle of the tasks and also manages the executor itself.
	 --> We can shutdown executor	
	    --> shutdown()
		--> shutdownNow
		--> isShutdown
     --> ExecutorService extends Executor
	 --> Used with other interfaces
		  --> Runnable --> it does the job .. it won't return anything
		  --> Callable --> it does the job .. and has capable of returning the result
		  --> Future
				Represents the result of an asynchronous two-way task.
ScheduledExecutor Service:
completionService:
				--> get()
				--> get(long, TimeUnit)
				--> isDone() boolean
				--> cancel(boolean) boolean
				--> isCancelled() boolean
			ActiveObject Pattern
			Proactive pattern
			
Important LoopHoles of null and NullPointerException in Java Part:
----------------------------------------------------------------
Link: https://www.youtube.com/watch?v=GwXzn2xSUqE			
			
Reserved words: (53)
--> Keywords (50)
--> Reserved Literal words (3)
		--> TRUE
		--> FALSE
		--> null
	We can use null for any object reference 
		--> class type
		--> Interface type
		--> enum type
		--> Annotation type
		--> Array type
	the corressponding object is not there and this variable is Not pointing to any object
		Student s = null;
		
	System.out.println(null);
		PrintStream has overloaded methods for println
				println(int)
				println(char)
				println(char[])
				println(String)
				
		so when we pass null to println(null)
					here println with null matched with multiple overloaded methods 
							1) println(char[])
							2) println(String)
						here ambiguous, compiler confused of which method to call  
					To avoid this we do this
						String str = null;
						here the type is resolved so no error println(str)
--> null is a reserved literal but not keyword in java
--> We can use null for any object reference variable 
					--> class type, interface type, array type, annotation type, enum type
--> If the value of the reference variable null means it is not pointing to any object.
--> null is application only for object types but not for primitives
--> null is the default value for reference variables
		I declared a reference variable but i didn't perform any assignment then JVM will always going to provide default value null for reference variable that value is null.
			default values concept is applicable only for static and instance variables but not local variables.
--> sysout(null) --> Error Ambiguous
		println(char[])
		println(String)
		compiler in confusion which method to call.
--> If we are trying to perform operation on null, then we will get NullPointerException
--> For any object reference r, r == null is always false.
							but null == null is always true.
--> If any object reference r, r.equals(null) is always false.
--> null and empry String("") both are not equals
There is no word like NULL in java
--> If an object is no longer required then assign null to its reference variables then object is eligible to GC.

At JVM level pointer concept is available.. but for programer level pointer is not there.							
				
5 Different ways to create objects in Java with Example:
--------------------------------------------------------
Link: https://programmingmitra.blogspot.com/2016/05/different-ways-to-create-objects-in-java-with-example.html

1) Using new keyword -- Constructor call involved
   Employee emp1 = new Employee();
 
2) Using Class class's newInstance() method -- Constructor call involved
   Employee emp2 = Employee.class.newInstance();
  
3) Using Constructor class's newInstance() method -- Constructor call involved
   Constructor<Employee> constructor = Employee.class.getConstructor();
   Employee emp3 = constructor.newInstance();
   
4) Using clone() method -- Constructor call not involved
   Employee emp4 = (Employee) emp2.clone();
   
5) Using Deserialization -- Constructor call not involved
   ObjectOutputStream oos = new ObjectOutputStream("file.ser");
   FileOutputStream fos = new FileOutputStream(oos);
   fos.writeObject(emp);
   
   ObjectInputStream ois = new ObjectInputStream("file.ser");
   FileInputStream fis = new FileInputStream(ois);
   Employee emp5 = (Employee)fis.readObject();
   
----------------------------------------------------------
ThreadLocalRandom:
http://thoughtfuljava.blogspot.in/2012/09/prefer-threadlocalrandom-over-random.html

https://stackoverflow.com/questions/23396033/random-over-threadlocalrandom#

Java 7 has introduced a new random number generator - ThreadLocalRandom
Normally to generate Random numbers, we either do:
--> Create an instance of java.util.Random OR
--> Math.random() --> which internally creates an instance of Random on fist invocation
Random is thread safe

https://dzone.com/articles/variable-shadowing-and-hiding-in-java?oid=facebook&utm_content=buffer3953d&utm_medium=social&utm_source=facebook.com&utm_campaign=buffer
When an instance variable in a subclass has the same name as an instance variable in a super class, then the instance variable is chosen from the reference type.

Annotation:
https://dzone.com/articles/creating-custom-annotations-in-java?oid=facebook&utm_content=buffer5ce36&utm_medium=social&utm_source=facebook.com&utm_campaign=buffer

Custom AOP:
http://www.baeldung.com/spring-aop-annotation



Clean Code:
https://sivalabs.in/2013/12/clean-code-dont-mix-different-levels-of-abstractions/


https://examples.javacodegeeks.com/core-java/util/hashmap/hashmap-changes-in-java-8/
O(n) performance
The big-O notation is a measure of complexity for a given algorithm. “n” is the amount of data used in the algorithm. It indicates the amount of time the algorithm will take when n tends to infinitive. O(2n) or O(constant * n) do not exist, O(1) means constant time (performance is not related to the data that is processed) and O(n) means that the performance is directly related or proportional to the amount of data that is processed.

O(log n) performance
In this case, it means that the algorithm will perform better when the amount of data is larger. Performance is not directly proportional to the large of the processed data but in a log n relation. O(log n) performs better than O(n).

https://dzone.com/articles/how-cas-compare-and-swap-java

http://flex4java.blogspot.in/2015/03/volatile-atomicity-visibility-and.html

http://flex4java.blogspot.in/2015/03/a-very-interesting-problem-related-to.html

Atomic:
Atomic which supports,  Lock free thread safety programming on single variable

https://stackoverflow.com/questions/1970345/what-is-thread-contention
A contention occurs when a thread is waiting for a resource that is not readily available; it slows the execution of your code, but can clear up over time.

A deadlock occurs when a thread is waiting for a resource that a second thread has locked, and the second thread is waiting for a resource that the first thread has locked. More than two threads can be involved in a deadlock. A deadlock never resolves itself. It often causes the whole application, or the part that is experiencing the deadlock, to halt.

Contention is simply when two threads try to access either the same resource or related resources in such a way that at least one of the contending threads runs more slowly than it would if the other thread(s) were not running.
thread contention is a condition where one thread is waiting for a lock/object that is currently being held by another thread. Therefore, this waiting thread cannot use that object until the other thread has unlocked that particular object

https://spring.io/blog

server.context.path=/bootdemo

Compare And Swap : Atomic
https://howtodoinjava.com/core-java/multi-threading/compare-and-swap-cas-algorithm/

gVideos for Algorithms:
https://www.youtube.com/watch?v=JPyuH4qXLZ0&list=PL8B24C31197EC371C
