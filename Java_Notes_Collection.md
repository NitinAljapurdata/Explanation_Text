Collections:
----------------

Fail first - Fail Fast:
------------------------
Fail Safe( ConcurrentHashMap ):
The Iterator of ConncurentHashMap always work on the snapshot of the hashMap. So, even if we make any changes to the map it wont throws ConcurrentModificationException

Fail Fast( HashMap ):
If we try to modification or add new element to the map while iterating map using iterator it will throw ConcurrentModificationException. Because internally hashMap's iterator 
	stores ModCount = size of hashmap ( if any modification add or delete done the ModCount changes )
		   ExpectedModCount = size of hashmap
		   
		   So getting elements data it checks the ModCount and ExpectedModCount
			HashMap's iterator
			 if (modCount != expectedModCount)
                throw new ConcurrentModificationException();
Example: http://javaconceptoftheday.com/fail-fast-and-fail-safe-iterators-in-java-with-examples/

HashMap and LinkedHashMap:
-------------------------
-->LinkedHashMap maintains insertion order.. HashMap does not maintains any order.
-->LinkedHashMap and HashMap both are non sysnchronized. To make them synchronized we can use Collections.SyschronizedMap().
-->LinkedHashMap extends HashMap and implements Map interface.

HashMap:
---------
Article: http://www.baeldung.com/java-hashmap


NumberFormat,

IntegerFormat extends NumberFormat
DecimalFormat extends NumberFormat
IntegerFormat extends NumberFormat
IntegerFormat extends NumberFormat
IntegerFormat extends NumberFormat


List<List<String>>


list = null
	list
	
	list.cler()
	
	list = null;
	
	32Bit --> 4GB
	64Bit --> 
	
	HashTable -> Inital capacity 11
	HashMap -> initialcapacity 16
	LinkedList -> default capacity 1
				  It grows as we put data into it
				  Each LinkedList$Entry contains:
						Object previous
						Object next
						Object entry
						Additional 24bytes per entry
						For a 10,000 entry LinkedList, the overhead is ~240k
						LinkedList is smaller when compared to HashSet, HashMaps
	ArrayList --> 
				Default capacity is 10 entries
	Stringbuffer --> default capacity is 16 characters
					Empty size is 72bytes
	
	-------------------------------------------------------------------------	
	Collection     DefaultCapacity    EmptySize  10kOverhead   Expansion		
	-------------------------------------------------------------------------
	HashSet			16					144			360k		*2
	HashMap			16					128			360k		*2
	HashTable		11					104			360k		*2 + 1
	LinkedList		1					48			240k		+1
	ArrayList       10					88			40k			*1.5
	Stringbuffer	16					72			24			*2
						
						
	Set initialcapacity
    Techniques for minimizing memory:
		--> Lazy allocation of collections
				Do not create a collection until you have something to put into it.
		--> Do not create collections for asingle Object
		--> Correct sizing of collections
				if you know that only 2entries will be stored, create with size 2:
					Example: HashMap map = new HashMap(2);
		--> Collections do not shrink once expanded

Set:		
https://dzone.com/articles/the-developers-guide-to-collections-sets?oid=facebook&utm_content=buffer67461&utm_medium=social&utm_source=facebook.com&utm_campaign=buffer


Prefer System.lineSeparator() introduced in Java7 for Writing System-Dependent Line Separator Strings in Java:
On UNIX systems:
	--> it returns "\n"
On Microsoft Windows systems 
	--> it returns "\r\n"
Earlier we suppose to use:
	--> System.getProperty(“line.separator”) 	
Link: https://www.javacodegeeks.com/2018/02/prefer-system-lineseparator-writing-system-dependent-line-separator-strings-java.html
