Difference between @Autowired and @Inject annotation in Spring?
----------------------------------------------------------------
Link: http://javarevisited.blogspot.in/2017/04/difference-between-autowired-and-inject-annotation-in-spring-framework.html#axzz4l6rW2DUl

You can potentially avoid that development effort by using standard annotations specified by JSR-330 e.g.  @Inject, @Named, @Qualifier, @Scope and @Singleton. A bean declared to be auto-wired using @Inject will work in both Google Guice and Spring framework, and potentially any other DI container which supports JSR-330 annotations.
--> We can use @Inject from Spring 3.0 onwards
https://scanlibs.com/getting-started-spring-framework/

10 Things Every Java Programmer Should Know about String:
-----------------------------------------------------------
http://javarevisited.blogspot.in/2013/07/java-string-tutorial-and-examples-beginners-programming.html#axzz4l6rW2DUl

10 Examples of forEach() method in Java 8:
------------------------------------------
Link: http://www.java67.com/2016/01/how-to-use-foreach-method-in-java-8-examples.html

forEach in parallel does not guarantee sequence.. if we need sequence then ise forEachOrdered


Java 1.5 Generics Tutorial: How Generics in Java works with Example of Collections, Best practices, Gotchas:
-----------------------------------------------------------------------------------------------------------
Link: http://javarevisited.blogspot.in/2011/09/generics-java-example-tutorial.html
Arrays don't support Generics in Java so you can not create Arrays like T[]
Though there is a work around which requires cast from Object[] to T[].
Example:
private T[] contents;
contents = new T[size];//compiler error
contents = (T[]) new Object[size]; //Workaround --casting object to generic type.

ThreadLocal:
-----------
https://dzone.com/articles/painless-introduction-javas-threadlocal-storage
https://veerasundar.com/blog/2010/11/java-thread-local-how-to-use-and-code-sample/

ThreadLocal context = new ThreadLocal();
context.set
context.get
context.remove

Volatile:
-----------
Link: https://www.youtube.com/watch?v=y8_jrkHEZpg
https://dzone.com/articles/java-volatile-keyword-0
If two Threads(Suppose t1 and t2) are accessing the same object and updating a variable which is declared as volatile then it means t1 and t2 can make their own local cache of the object except the variable which is delcared as a volatile. So,the volatile variable will have only in main copy which will be updated by different threads and updation by on thread to the volatile variable will immediately reflect to the other thread.
So, the volatile variable is used in the Thread context.
