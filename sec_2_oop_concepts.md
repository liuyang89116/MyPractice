# Sec 2: OOP Concepts

###13) What is difference between object oriented programming language and object based programming language?
Object based programming languages follow all the features of OOPs **except Inheritance**. Examples of object based programming languages are **JavaScript**, VBScript etc.

###14) What will be the initial value of an object reference which is defined as an instance variable?
The object references are all initialized to null in Java.

###15) What is constructor?
Constructor is just like a method that is used to initialize the state of an object. It is invoked at the time of object creation.

###16) What is the purpose of default constructor?
The default constructor provides the default values to the objects. The java compiler creates a default constructor only if there is no constructor in the class.

###17) Does constructor return any value?
**yes**, that is current instance (You cannot use return type yet it returns a value).

###18)Is constructor inherited?
**No**, constructor is not inherited.

###19) Can you make a constructor final?
**No**, constructor can't be final.


###20) What is static variable?
* static variable is used to refer the common property of all objects (that is not unique for each object) e.g. company name of employees,college name of students etc.
* static variable **gets memory only once** in class area at the time of class loading.
(1) **Program of counter without static variable**
![](sec2_1.png)

**(2) Program of counter by static variable**
![](sec2_2.png)


###21) What is static method?
* A static method belongs to the class rather than object of a class.
* A static method can be invoked without the need for creating an instance of a class.
* static method can access static data member and can change the value of it.
![](sec2_3.png)
![](sec2_4.png)


###22) Why main method is static?
Because object is not required to call static method if It were non-static method,jvm creats object first then call main() method that will lead to the problem of extra memory allocation.
![](sec2_5.png)

###24) Can we execute a program without main() method?
**Yes**, one of the way is static block.

###25) What if the static modifier is removed from the signature of the main method?
Program compiles. But at runtime throws an error "**NoSuchMethodError**".


###26) What is difference between static (class) method and instance method?
![](sec2_6.png)


###27) What is this in java?
It is a keyword that that refers to the current object.
(1) **the problem without this keyword**
![](sec2_7.png)

(2) **Solution of the above problem by this keyword**
![](sec2_8.png)

###28)What is Inheritance?
Inheritance is a mechanism in which one object acquires all the properties and behaviour of another object of another class. It represents IS-A relationship. It is used for **Code Resusability** and **Method Overriding**.
![](sec2_9.png)


###29) Which class is the superclass for every class.
Object class.


###30) Why multiple inheritance is not supported in java?
To reduce the complexity and simplify the language, multiple inheritance is not supported in java in case of class.

###31) What is composition?
Holding the reference of the other class within some other class is known as composition.

###32) What is difference between aggregation and composition?
Aggregation represents weak relationship whereas composition represents strong relationship. For example: bike has an indicator (aggregation) but bike has an engine (compostion).

###33) Why Java does not support pointers?
Pointer is a variable that refers to the memory address. They are not used in java because they are **unsafe**(unsecured) and **complex to understand**.


###34) What is super in java?
It is a keyword that refers to the immediate parent class object.
![](sec2_10.png)
![](sec2_11.png)





















