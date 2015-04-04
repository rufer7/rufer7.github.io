---
layout: post
category: reader-experiences
title: OCA Java SE 7 Programmer I Certification Guide
date: 04 Apr 2015
tags: Java programming book reader-experience
---

As recommended to prepare for the Java SE7 associate programmer certification I read the certification guide written by Mala Gupta. In this post I would like to go into the most interesting things treated by this book.


<div class="inline-img-left">
    <img src="{{ site.url }}/assets/book-covers/oca-java-SE7-programmer-I-certification-guide.jpg" alt="Book cover of OCA Java SE7 Programmer I certification guide"/>
</div>


### General Impression
In my opinion reading this book wasn't very hard because the author did a very good job. The book is structured logically and goes from basics to more complex topics. Additionally the author tried to work with graphical representations for easier understanding. Last but not least every chapter has a question section where you can verify if you understood the stuff treated in the corresponding chapter. 


### Most interesting things

Now, as announced I'll go through some of the most interesting things I learned from this book. The selection of "most interesting things" is a personal and subjective selection.


#### String Pool

The explanations about the String pool was a welcome refresher. The Java String pool is managed by the JVM and holds a couple of String objects, which could be referenced by several String variables. If a String value is assigned to a String variable without instantiating a new String object, a new String object will be created in the String pool if the value doesn't already exist and then the reference will be assigned to the String variable.

<pre>
  <code class="java">
    // Assigning a String value to a String variable results in referencing
    // and if not yet existing as well in creation of a String object in the pool
    String s = "abc";
    
    // Creating a new String object (Not in pool)
    String s2 = new String("abc");
  </code>
</pre>

If the two Strings will be compared with `==` the result is `false` because not both variables are pointing to the object, which holds `abc` of the pool. If there will be a another variable (`s3`) initialized like `s` comparison of `s3` and `s` by `==` will result in `true` because both variables are referencing the same object in the String pool.


#### StringBuilder vs. StringBuffer

For String manipulations like concatenation, insertion,... the fluent APIs of StringBuilder and StringBuffer are very helpful. The main difference between the two builder classes every Java developer should know is, that StringBuilder in contradiction to StringBuffer is not thread save. So if working with multi-thread applications you should always use StringBuffer instead of StringBuilder. 


#### Arrays

Concerning arrays the book provides a lot of information. The most important thing to know about arrays from my point of view is the fact, that every array is an object. As well in the case if it only holds primitive types like `int`, `long`,...
Another interesting thing about arrays is, that declaration can be done in different ways as you can see below.

<pre>
  <code class="java">
    int[] array;
    int array[];
    
    int[][] towDimensionalArray;
    int[] towDimensionalArray[];
    int towDimensionalArray[][];
  </code>
</pre>


#### Polymorphism

The book also treats the topic polymorphism. I grabbed one special thing out of this topic, which is very important to know if working with Java.
Assume there is a class-hierarchy as follows
<img src="{{ site.url }}/assets/screenshots/class-hierarchy.png" alt="Employee class hierarchy"/>


Let's now have a look what happens, if the following code will be executed:

<pre>
  <code class="java">
    Employee employee = new FullTimeEmployee();
    
    employee.calculateSalary();
    String employeeName = employee.name;
  </code>
</pre>


`employee.calculateSalary()` will execute the calculateSalary-method of FullTimeEmployee because method invocation in Java is resolved by instance type. If accessing instance variables it's the other way around, so employee.name will return the value of the instance variable of the super class as well, if the object of the subclass (in this case FullTimeEmployee) provides as well an instance variable called `name`.


#### Try with resources

<pre>
  <code class="java">
    public void doSomething() {
    }
  </code>
</pre>


### Recommendation

If you would like to take the exam as well I would recommend you to split your preparation into two steps. First reading the book from Mala Gupta, which covers all the topics of the certification exam. And secondly do some training exams. There are several providers of such training exams. One I could recommend you is [Enthuware](http://enthuware.com/).