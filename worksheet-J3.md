ALINA JALISI - WORKSHEET J3 

QUESTION ONE: Define polymorphism in the context of Java and provide one example where it is valuable?
//Polymorphism in Java allows objects of different types to respond to the same message in different ways. This is achieved by using interfaces and abstract classes.


QUESTION TWO: Consider the following program from the class notes

public class Ex3 {
  public static void main(String[] args) {
    Random   rand = new Random(System.currentTimeMillis());
    Point    v    = new Point(3, 4);
    LabPoint w    = new LabPoint(5, 2, "A");
    String   x    = "I'm a string";
    Scanner  y    = new Scanner(System.in);

    Object u;
    int i = rand.nextInt(4);

    if( i == 0 )
      u = v;
    else if( i == 1 )
      u = w;
    else if( i == 2 )
      u = x;
    else
      u = y;
    System.out.println(u); //<--
  }
}
Explain how polymorphism makes this program possible.
//Polymorphism allows objects of any type to be assigned to a variable of type Object. This is because all classes in Java implicitly extend the Object class. The variable u in the program is declared as type Object, so it can be assigned to any of the four objects v, w, x, or y.

QUESTION THREE: What is the output of this program? You should be able to do this without running the program!

class A {
    public String toString(){
        return "A";
    }
}

class B extends A{
    public String toString() {
        return "B";
    }
}

class C extends A {
    public String toString() {
        return super.toString();
    }
}

class D extends C {
    public String toString() {
        return super.toString();
    }
}

public class tmp {
    public static void main(final String args[]) {
        D d = new D();
        System.out.println(d.toString());
    }
}
//The output of the program is A because the toString() method of class D returns the string A from its parent class A.

QUESTION FOUR: What is the output of this program? You should be able to do this without running the program!

class A {
    public String toString() {
        return "A";
    }
    
    public String fancyToString() {
        return "~~A~~";
    }
}

class B extends A {
    public String toString() {
        A letterA = this;
        return letterA.fancyToString();
    }
    public String fancyToString() {
        return "~~B~~";
    }
}

public class LetterPrinter {
    public static void main(final String args[]) {
        B letterB = new B();
        System.out.print(letterB.toString() + " ");
        
        A letterA = letterB;
        System.out.println(letterA.toString());
    }
}
//The output of the program is ~~B~~ ~~B~~ because the toString() method of class B calls the fancyToString() method of the A object that is passed to it, which returns the string ~~B~~.

QUESTION FIVE: What is the output of this program? You should be able to do this without running the program!

class A {
    public String toString() {
        return "A";
    }
    
    public String fancyToString() {
        return "~~A~~";
    }
}

class B extends A {
    public String fancyToString(){
        return "~~B~~";
    }
}

public class LetterPrinter {
    public static void main(final String args[]) {
        B letterB = new B();
        System.out.print(letterB.toString() + " ");
        
        A letterA = letterB;
        System.out.println(letterA.toString());
    }
}
//The output of the program is A A because: Class B does not have a toString() method, so when letterB.toString() is called, the toString() method of its parent class A is used. After A letterA = letterB, letterA still refers to the same object as letterB, so letterA.toString() also uses the toString() method of class A.

QUESTION SIX: Consider the first two class declarations. What is the output of compiling the program below?

abstract class Letter {
    protected boolean uppercase;

    abstract String get_name();

    abstract int get_alphabet_position();
}
class A extends Letter {
    public String toString() {
        return "A";
    }

    protected int get_alphabet_position() {
        return 1;
    }

    private String get_name() {
        return "A";
    }
}
//The program will not compile because the get_name() method in class A is declared as private, which is less visible than the get_name() method in the abstract class Letter, which is declared as abstract

QUESTION SEVEN: If we change the implementation of A to the following, what does the code below output?

abstract class Letter {
    protected boolean uppercase;

    abstract String get_name();

    abstract int get_alphabet_position();
}
class A extends Letter {
    public String toString() {
        return "A";
    }

    public int get_alphabet_position() {
        return 1;
    }

    protected String get_name() {
        return "A";
    }
}
public class Main {
    public static void main(final String args[]) {
        A a = new A();
        System.out.println("A: " + a.get_alphabet_position());
    }
}
//The code outputs the following: 
A: 1
This is because the get_alphabet_position() method in class A overrides the abstract method in the abstract class Letter. The overridden method is public, so it can be called from outside of the class. When the get_alphabet_position() method is called on the a object, the overridden method in class A is invoked, which returns the value 1.

QUESTION EIGHT: What is the output of this program? You should do this without running the program.

class A {
    public String toString() {
        return "A";
    }
}

class B extends A {
    public String toString() {
        return "B";
    }
}

public class PolymorphicOverload {
    public void foo(B letterB1, B letterB2) {
        // 2
        System.out.println("foo2: " + letterB1 + " " + letterB2);
    }

    public void foo(A letterA1, A letterA2) {
        // 1
        System.out.println("foo1: " + letterA1 + " " + letterA2);
    }
    public static void main(String args[]) {
        PolymorphicOverload f = new PolymorphicOverload();
        B letterB = new B();
        A letterA = (A) new B();
        f.foo(letterB, letterA);
    }
}
//The output of the program is foo1: B B because the foo() method with the parameter types A and A is called, even though the letterB and letterA objects are both of type B. This is because the letterA object is declared as an A object, so the compiler will try to find the most specific method that matches the parameters.



QUESTION NINE: Assume that class A is implemented in such a way so that the program will compile and run. What is the output? You should do this problem without running the code.

public class Temp {
    public static void foo(A a) {
        System.out.println("foo1: " + a.get_name());
    }
    public static void foo(Letter a) {
        System.out.println("foo2: " + a.get_name());
    }
    public static void main(final String args[]) {
        Letter a = (Letter) new A();
        foo(a);
    }
}
//The output of the program is foo2: A because the foo() method with the parameter type Letter is called, even though the a object is an instance of class A. This is because the a object is declared as a Letter object, so the compiler will try to find the most specific method that matches the parameter.

QUESTION TEN: Suppose you had the following class structures

public class Species {
    String genus;
    String species;
    public Species(String g, String s) {
        genus = g;
        species = s;
    }
    
    public Species(Species s) {
        genus = s.genus;
        species = s.species;
    }
    
    public String toString() {
        return genus + " " + species;
    }
}

public class Breed extends Species {
    protected String breed;

    public Breed(String b, String g, String s) {
        super(g, s);
        breed = b;
    }

    public Breed(String b, Species s) {
        super(s);
        breed = b;
    }

    public String toString() {
        return super.toString() + "(" + breed + ")";
    }
}

public class Pet {
    String name;
    Species species;

    public Pet(String n, Species s) {
       name = n;
       species = s;
    }

    public String toString() {
        String ret = "Name: " + name + "\n";
        ret += "Species: " + species;
        retunr ret;
    }       
}
What is the output of the following snippet of code? If there is an ERROR, describe the error. You should not need to run the code to determine the output.
   Species dog = new Species("Canis","Familaris");
   Breed shorthair = new Breed("shorthair", new Species("Felis","Catus"));
   Pet fluffy = new Pet("fluffy", new Breed("pomeranian", dog));
   Pet george = new Pet("george", dog);
   Pet brutus = new Pet("brutus", (Species) shorthair);
   
   System.out.println(fluffy);
   System.out.println(george);
   System.out.println(brutus);
//OUTPUT AND EXPLANATION: 
Name: fluffy
Species: Canis Familaris(pomeranian)
Name: george
Species: Canis Familaris
Name: brutus
Species: Felis Catus(shorthair)

The brutus pet object is the only one that is different from the other two. This is because the shorthair breed object is of type Species, even though it is a subclass of Species. When the brutus pet object is created, the (Species) shorthair cast is necessary to convert the shorthair breed object to a Species object.

QUESTION ELEVEN: Draw the class hierarchy for the above classes, that is the UML diagram that simply shows who inherits from whom.
//SCREENSHOT UPLOADED TO GIT REPO INCLUDING UML DIAGRAM

QUESTION TWELVE: Continuing with the classes from the previous question, consider a mystery function that returns a object of the given class. You do not know the definition of the mystery function, other than it compiles properly and returns an object of the class. For each of the following method calls marked below, indicate the value of the output, if the output cannot be determined, or if there is an error.


A a = mysteryA(); //<-- mystery function, this line compiles (the below may not!)
System.out.println(a.foo()); //<-- Mark A.1
System.out.println(a.bar()); //<-- Mark A.2
System.out.println(a.baz()); //<-- Mark A.3


B b = mysteryB(); //<-- mystery function, this line compiles (the below may not!)
System.out.println(b.foo()); //<-- Mark B.1
System.out.println(b.bar()); //<-- Mark B.2
System.out.println(b.baz()); //<-- Mark B.3

D d = mysteryD(); //<-- mystery function, this line compiles (the below may not!)
System.out.println(d.foo()); //<-- Mark D.1
System.out.println(d.bar()); //<-- Mark D.2
System.out.println(d.baz()); //<-- Mark D.3
//
A.1: Compiles, output not deterministic. The mystery function could return an object of type A, B, C, or D, each of which has a different implementation of the foo() method.

A.2: Compiles, output not deterministic. The mystery function could return an object of type A, B, C, or D, each of which has a different implementation of the bar() method.

A.3: Doesn't compile, no output. The baz() method is not defined in the A class, so it cannot be called on an object of type A.

B.1: Compiles, output is 41. The mystery function could return an object of type B, which has a foo() method that returns the value 41.

B.2: Compiles, output is 49. The mystery function could return an object of type B, which has a bar() method that returns the value 41 + 8.

B.3: Compiles, output is y. The mystery function could return an object of type B, which has a baz() method that returns the value y.

D.1: Compiles, output is 42. The mystery function could return an object of type D, which has a foo() method that returns the value 42.

D.2: Compiles, output is 7. The mystery function could return an object of type D, which has a bar() method that returns the value 7.

D.3: Doesn't compile, no output. The baz() method is not defined in the D class, so it cannot be called on an object of type D.

QUESTION THIRTEEN: 
What is the difference between a class and an abstract class?
//A class is a blueprint for creating objects, while an abstract class is a blueprint for creating other classes. Classes can be instantiated, but abstract classes cannot. Abstract classes are used to define common functionality that can be inherited by concrete subclasses.

QUESTION FOURTEEN: If you were to create an abstract class for a Car – what features could be defined in the implemented class vs. what could be defined in the abstract class? Provide justifications for your design.
//Features that could be defined in the implemented class:

Specific car attributes: make, model, year, color, etc.
Specific car behaviors: accelerate, brake, turn, etc.
Specific car features: sunroof, heated seats, etc.
Justification: These features are specific to each car model and should not be shared by all cars.

Features that could be defined in the abstract class:

Common car functionality: start engine, stop engine, shift gears, etc.
Common car safety features: airbags, seatbelts, etc.
Common car performance features: fuel efficiency, top speed, etc.
Justification: These features are common to all cars and should be implemented in the abstract class so that they can be inherited by all concrete subclasses.

This design allows for flexibility and reusability. Concrete subclasses can define their own specific features, while the abstract class provides a foundation of common functionality
