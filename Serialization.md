Link: 
https://stackoverflow.com/questions/2475448/need-of-serialization-in-java (Short story about serialization)
https://www.quora.com/What-is-the-need-for-serialization-in-java

Serialization:
---------------
-->Introduction
-->Object graph in serialization
-->Customized serialization
-->Serialization wrt inheritance
-->Externalization
-->SerialVersionUID

Explanation 1:
Serialization is usually used When the need arises to send your data over network or stored in files. By data I mean objects and not text.
Now the problem is your Network infrastructure and your Hard disk are hardware components that understand bits and bytes but not JAVA objects.
Serialization is the translation of your Java object's values/states to bytes to send it over network or save it.
This is analogous to how your voice is transmitted over PSTN telephone lines.

Explanation 2:
Serialization is used for RMI,remote method invocation.
Suppose you are invoking a method on the remote machine by passing the primitive values,then its okay.
But if you are trying to invoke a method on the remote machine by passing reference type , then you should know when you pass a reference variable , it contains only the address on which the other machine has no significance , since on the other machine this address location can have other variable so pointing to different object.
So Serialization comes in play in that situation , where you save the state of object to a file and send it over the network in encrypted form and then remote machine receives the file having object state and decrypt and use that object for the required purpose.

Serializable (Interface):
	--> Java.io package
	--> No methods

------------
Process of saving state of an object to a file

Process of converting java supported form into either network supported form or file supported form this process is called serialization.
Reverse process de-serialization.

By using FileOutstream and ObjectOutstream classes we can  implement serialization

Deserialization: the process of reading state of an object from the file is called de-serialization.
It is the process of converting an object from either file supported form or network supported form into Java supported form.
By using FileInputStream and ObjectInputStream classes we can implement de-serialization

If we are not implementing the interface Serializable.. then program will compile correctly.. but fails at run time.
--> writeObject
--> readObject

Transient Keyword: Use this modifier only for variable ... it cannot be used for any other that is methods classes etc.,
Since we are saving the object state to file .. there may be few sensitive information that should be saved to file . So, to avoid those sensitive information to be serialized or saving to file we use transient..
Example: 
i=50; transient j=10;
after serialization .. j value will be stored as default value j=0.. instead j=10
------------	
	
Serialization:
-------------
--> We can serialize only serialiable objects
--> An object is said to be serializable if and only if the corressponding class implemenets serializable interface.
--> Serializable interface present in java.io package and it does not contains any methods. It is a market interface.
--> If we are trying to serialize a non-serializable object then we will get run-time execption saying...
				-->NotSerializableException --> is CheckedException

Transient:
--> Transient modifier applicable only for variables but not for methods and classes.
--> At the time of serialization if we don't the value of a particular variable to meet security constraints then we should declare that variable as transient.
--> While performing serialization JVM ignores original value of transient variable and save default value to the file.. 
						Hence, transient means not to serialize.
Transient VS Static:
-->Static(static is class level data) is not part of object state.. serialization concept only applicable for object. So, static variable won't participate in serialization. 

-->Static variable is not part of object state and hence it won't participate in seralization due to this declaring static variable as transient there is no use or no impact

Transient VS Final:
--> Final variables will be participated in serialization directly by the value. Hence declaring a final as transient there is no impact.

--> Every final variable will be replaced by the value at compile time only .. for normal variable the variable replacement is happened at runtime.
    --> if it is in variable form them JVM checks variable is in transient .. since final variable is in value 

***SUMMARY***

Declaration 			Output
int i=10;				10, 20
int j=20;

transient int i=10		0 20
		  int j=20
***Important***:
If we try to serialize an object and the object is not implementing the serialization till it compiles fine... but fails at runtime says object java.io.NotSerializableException
If the dog doest not implemenets serializable no problem at compile time but fails at runtime
transient static int i=10  10 0
transient int j=20

transient int i=10         0
transient final int j=20   20

transient static int i=10  10, 20
transient final int j=20

Using Object reference we can access Class level data ( access static variables )

Serialize Multiple Objects:
--> In serialization and de-serialization order of objects is important.. otherwise we get ClassCastException
	Example: 
			A a = new A()
			B b = new b()
			C c = new C()
			Here we serialized A --> then B --> then C
			So, we have to de-serialize the objects we get those objects in the same order we serialized.
			that is
			A a = (A)ois.readObject();
			B b = (B)ois.readObject();
			C c = (C)ois.readObject();
			
			If we changed the sequence as
			B b = (B)ois.readObject();
			A a = (A)ois.readObject();
			C c = (C)ois.readObject();
			Here we get ClassCastException
			
If we don't know the order of objects in serialization:

Object Graphs in Serialization:
--> Whenever we are serializing an object, the set of objects which are reachable from that objects will be serialized automatically this group of object is Object Graph in Serialization
--> In object graph every object should be serializable if any of the class is not serialized then we get runtime exception NotSerializableException

class Dog{
	Cat cat = new Cat();
}
class Cat {
	Rat rat = new Rat();
}
class Rat{
	int i = 20;
}


ServialVersionUID:
------------------
In Serialization both sender and receiver need not be same and need not be from the same location and need not to use same machine. Persons may be different, locations may be different and machines may be different.

At the time of serialization JVM will save a unique id with every object. This unique id will be generated by JVM based on .class file.
At the time of de-serialization Receiver side JVM compare object unique id with local .class unique id. If both are matched then only de-serialization will be performed otherwise reciever unable to de-serialize and we will get Runtime Exception saying InvalidClassException.

The unique Id nothing but SerialVersionID.

Customnized Serialization: Part - 8
---------------------------
Need of customized serialization:

In default serialization there may be chance of loss of information because of trainsent keyword to recover this loss of information we should go for customized synchronization.
class Account{
	String name = "abc";
	transient String password = "efg"; --> because of this "efg" is lost in de-serialization
}

Do extra work at sender and receiver side --> is is nothing but customized serialization

private void writeObject(ObjectOuputStream oos) throws Exception --> contains extra work to recover loss of information
private void readObject (ObjectInputStream ois) throws Exception --> contains extra work to recover loss of information

--> oos.defaultWriteObject() --> to perform default serialization
--> ois.defaultReadObject () --> to perform default de-serialization

We implement customized serialization by using above 2 methods
At the time of serialization if we want to do any extra work we have to define in above 2 methods .. these methods get called automatiacally at the of serialization(writeObject) , de-serialization(readObject)

These 2 methods will be called automatically by the JVM such methods considered as Callback methods.
Process of customized Serialization:

Serialization with respect to inheritance:
-------------------------------------------
We have 2 Cases
--> Parent implements Serializable but child class doesn't implements serilazable
--> Parent doesn't implements Serializable but child class implements serilazable

Case 1: 
Parent implements Serializable but child class doesn't implements serilazable:

Class Parent implements Serializable{
	int i = 10;
}

Class child extends Parent{
	int j = 20;
}

If the Parent implements serilazable then automatically by default every child is always serializable. Serializable nature is inheriting from parent to child

**NOTE**
GenericServlet implements Serializable so by default all servlets are serializable because of parent is serializable

Case 2:
Parent doesn't implements Serializable but child class implements serilazable:
Eventhough parent does not implements serializable we can able to serlize child class object
Conclusion 1:
To serializable child class object parent class need not be serializable
	--> If there is a restriction that parent should be serializable then we cannot create instance of any class because Object class does not implements Serializable

-->At the time of "serialization" JVM will check is any instance variable inheriting from non serializable area. If any instance variable inheriting from non serializable area then JVM will ignore's original value and stores there default value.
Case 3:
-->At the time of "de-serialization" JVM will check if any parent class doest not implements serializable then JVM executes instance control flow in every non serializable parent.
	--> Identification of instance member
	--> Execute instance assignement and instance blocks.
	--> Execute constructor and share instance value to current object 
Case 4:
	But should be compulsory contain constructor supplied by either programmer supplied or compiler. otheriwse we will get "InvalidClassException".
	
	Externalizable implemented class should compulsory contain public no arg constructor otherwise we will get run time InvalidClassException
	
	In Externalization everything taken care by developer .. transient wont play any role .. since we are going for externalization for saving part of the object 
	
Static Controll Flow:
		1) Identification of static members from top to bottom
		2) Execution of static variable assignment and static blocks from top to bottom
		3) Execution of main method
		3) Execution of main method
		
	1) Elvis elvis
	2) boolean 
	3) main
	
	i=0, j=0
	j = 0,j = 20, i=10
	First static block
	
	second static block

Externalization:
-------------------
--> In Serialization everything takes care by JVM and programmer doesn't have any control.
--> In seralization it is always possible to save total object to the file and it's not possible to save part of the object, which may creates performance problems.
--> To overcome this problem we should go for externalization.
--> The main advantage of Externalization over serialization is everything takes care by programmer and JVM doesn't have any control based on our requirement we can save either total object or part of the object, which improves performance of the system.

--> Serializable performance is low.. Externalization performance is high
--> Serialization is the best choice if you want to store complete object. If you want to store part of the object then Externalizationis the best choice.

To provide externalizable ability for any java object compulsory the corressponding class should implement externalizable interface. Externalizable interface defines two methods.
--> writeExternal()
--> readExternal()

Serializable (Interface) 1.1Version of java
	|
	|
	|
Externalizable ( Interface ) 1.1 Version of java 
	--> writeExternal(ObjectOutput output) throws IOException
	--> readExternal()
	
class ExternalizationDemo implemenets Externalizable{
	String s;
	int i;
	int j;
	public void writeExternal(ObjectOutput) throws IOException{
		out.writeObject(s);
		out.writeInt(1);
	}
	public ExternalizationDemo(){
		sysout("Public no-arg constructor");
	}
	--> this method will be exeecuted automatically at the time of serialization 
	--> Within this method we have to write code to save required variable to the file.
	
	public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException{
		s = (String)in.readObject();
		i = in.readInt();
	}
	--> This method will be executed automatically at the time de-seralization
	--> Within this method we have to write code to read required variables from the file and assign to current object.
	
	
	public static void main(String arg[]){
		ExternalizationDemo e = new ExternalizationDemo("durga", 10, 20);
		FOS fos = new FOS("read.ser");
		OOS oos = new OOS(fos);
		oos.writeObject(oos);
			
		FIS fis = new FIS("read.ser");
		OIS ois = new OIS(fis);
		oos.readObject();
	}
}
--> But strictly speaking at the time of de-seralization JVM will create a seperate new object (since we do not have complete method in serialized file) by executing public no arg constructor on that object JVM call readExternal(ObjectInput) method.
--> Hence, every externalizable implemented class should compulsory contain public no-arg contrctor otherwise we will get runtime exception saying InvalidClassException

--> If the class implements Serializable interface then total object will be saved to the file in this case output is durga 10, 20.
--> If the class implements Externalizable then only required varialbes will be saved to the save in this case output is 
public no-arg constructor
durga 10 0

-->In serialiazation Transient keyword will play role but in externalization transient keyword won't play any role. because in externalization we are filtering the variables in writeExternal. Transient key work not required.

Serialization							|						Externalization
-------------------------------------------------------------------------------------------------------------------
--> Default Serialization										--> Customized seralization
--> Takes care by JVM											--> take care by programmer
--> Total object is serialized
--> Performance islow											--> performance high
--> Best choice to save complete object 						--> best choice for partial object serialiazation
--> Marker interface 											--> not marker interface
--> public default constructor not required						--> public no-arg constructor 
																		InvalidClassException
--> transient play role.                 						--> transient does not play any role.


Java serialization: readObject() vs. readResolve():
https://stackoverflow.com/questions/1168348/java-serialization-readobject-vs-readresolve

The readResolve Method
For Serializable and Externalizable classes, the readResolve method allows a class to replace/resolve the object read from the stream before it is returned to the caller. By implementing the readResolve method, a class can directly control the types and instances of its own instances being deserialized. The method is defined as follows:

ANY-ACCESS-MODIFIER Object readResolve() throws ObjectStreamException;

Interview question: about Java serialization and singletons:
https://stackoverflow.com/questions/2958863/interview-question-about-java-serialization-and-singletons

--> Serialization is used for RMI,remote method invocation.
--> Suppose you are invoking a method on the remote machine by passing the primitive values,then its okay.
--> But if you are trying to invoke a method on the remote machine by passing reference type , then you should know when you pass a reference variable , it contains only the address on which the other machine has no significance , since on the other machine this address location can have other variable so pointing to different object.
--> So Serialization comes in play in that situation , where you save the state of object to a file and send it over the network in encrypted form and then remote machine receives the file having object state and decrypt and use that object for the required purpose.

http://java-questions.com/Serialization-interview-questions.html

Multi thread
