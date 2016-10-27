# Sec 1: Basics of Java Questions

###1) What is difference between JDK,JRE and JVM?
**JVM**   
JVM is an acronym for **Java Virtual Machine**, it is an abstract machine which provides the runtime environment in which java bytecode can be executed. It is a specification.
JVMs are available for many hardware and software platforms (so **JVM is platform dependent**).  

**JRE**  
JRE stands for **Java Runtime Environment**. It is the implementation of JVM.

**JDK**    
JDK is an acronym for **Java Development Kit**. It physically exists. It contains JRE + development tools.

###2) How many types of memory areas are allocated by JVM?
![](sec1_1.png)

###3) What is JIT compiler?
**Just-In-Time(JIT) compiler**:It is used to improve the performance. JIT compiles parts of the byte code that have similar functionality at the same time, and hence reduces the amount of time needed for compilation.Here the term “compiler” refers to a translator from the instruction set of a Java virtual machine (JVM) to the instruction set of a specific CPU.

###4) What is platform?
A platform is basically **the hardware or software environment** in which a program runs. There are two types of platforms software-based and hardware-based. Java provides **software-based** platform.

###5) What is the main difference between Java platform and other platforms?
The Java platform differs from most other platforms in the sense that it's a software-based platform that runs on top of other hardware-based platforms.It has two **components:**
* Runtime Environment
* API (Application Programming Interface)


###6) What gives Java its 'write once and run anywhere' nature?
The bytecode. Java is compiled to be a byte code which is the intermediate language between source code and machine code. This byte code is not platform specific and hence can be fed to any platform.

###7) What is classloader?
The classloader is a subsystem of JVM that is used to load classes and interfaces.There are many types of classloaders e.g. Bootstrap classloader, Extension classloader, System classloader, Plugin classloader etc.


###8) Is Empty .java file name a valid source file name?
Yes, save your java file by .java only, compile it by **javac.java** and run by **java yourclassname**
![](sec1_2.png)

###9) Is delete,next,main,exit or null keyword in java?
No.

###10) If I don't provide any arguments on the command line, then the String array of Main method will be empty or null?
It is empty. But not null.

###11) What if I write static public void instead of public static void?
Program compiles and runs properly.

###12) What is the default value of the local variables?
The local variables are not initialized to any default value, neither primitives nor object references.




