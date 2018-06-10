# Class Notes
Metaprogramming: programming environment that you can write about your code in the language that you are using that can be used to generate code.

Orthogonality: how independent are they of each other

Java vs C:
C: can't return array. can return pointer to array
Java: Can return array
* Efficiency
  - space, time, power, network access

* Simplicity
  - Things should be as simple as possible (Albert Einstein)

* Convenience
  - Easy to use (write code, read code)

[Simplicity & Convenience CONFLICT]

Example: Convenient but not Simple
-----------------------------------
i = i + 1;
i += 1;
i++;
++i;

* Safety (Security Issues)
  - compile-time (complier warnnings about safety)
  - run-time (run-time good enough to handle problems)
    - C++ (crash if lucky, undefined behavior if unlucky)

Programming Language Catetories
--------------------------------
- Imperative vs. Functional vs. Logic
- Objective Oriented vs. Non Objective Oriented
- Compiled vs. Scripting

Imperative/Procesural Languages (most common & popular)
--------------------------------------------------------
* In sequence

Functional Languages
---------------------
FUNCTIONS

* NO commands
* Evaluate expression
* Calling functions
* F1(F2(x)) (Can also use C this way)
* **Referential Transparency** -  it usually means that an expression always evaluates to the same result in any context
* Performance: von Neumann bottleneck -  idea that computer system throughput is limited due to the relative ability of processors compared to top rates of data transfer
* get better clarity and performance with functional


Logic Languages
----------------
PREDICATES

* P1(x) & P2(x)
* Don't evaluate
* Don't execute
* Theorem proving program (?)
* Highest level

Compile-time is the instance where the code you entered is converted to executable while Run-time is the instance where the executable is running

implicit vs explicit casting:
These explicit casts are time-consuming and ugly

2 arguments in their favor:
1. need explicit casting for type inference which saves bunch of time
2. implicit errors hard to find
3. do no favors for urself when u need to do expensive casts so might as well list.

better to catch errors early: compile time vs run time. better catch in compile time

Sapir-Wharf Hypothesis
-----------------------
* the language we use determines how to view the world & how we think

How to choose a syntax
-----------------------

Leibniz's Criterion - a proposition's form should mirror reality
- let x = 37 * 3 in x * x    (1)
- (fun x -> x * x) 37 * 3 (out-of-order, right to left)
- if (x >= 0 && x < n) print ("OK");     (2)
- if (0 <= x < n) print ("OK"); (always use less than, not greater than)

Example C Programm
* Phase 0: interpret
* Phase 1: throw away spaces, newlines, comments
* Phase 2: Tokenization or Lexical Analysis (lexing)

* Token: member of a known fixed finite set

```
byte strings --> char strings --> token strings --> parse tree (derivation)
|                                             |     |                     |
+----------------------+----------------------+     +-----------+---------+
                     lexing                                  parsing

-----------------> attributed tree ---------------> simple abstract machine
name resolution                     intermediate    +---------------------+
type checking                        code gen       | main:               |
                                                    |---------------------|
                                                    |   push    getchar   |
                                                    |   call    0         |
                                                    |   long              |
                                                    |   ret               |
                                                    +---------------------+

|                                                                         |
+-------------------------------------+-----------------------------------+
                          machine independent code

                           machine dependent code
+-------------------------------------+-----------------------------------+
|                                                                         |

--> machine dependent code -----> optimization ------> asm --> ld --> load
   +---------------------+     +-----------------+      |       |      |
   | leal  getchar, %eax |     | call getchar    |      *       |      *
   | pushl %eax          |     | tstl %eax, %eax |   .o file    |     RAM
   | popl  %eax          |     | sete %el        |              *
   | call  *%eax         |     | ret             |          executable
   | tstl  %eax, %eax    |     +-----------------+
   | sete  %el           |
   | ret                 |
   +---------------------+


   Summary: page 47 This is the classical sequence
  ```

Interpreter
-----
- Language systems that interpret a program run it much more slowly than those that compile the program
- Compiling takes more time up front but results in machine language program that runs at hardware speed.

Virtual Machines
----
JVM- allows platform independent when you compile to intermediate code


Linking
---
- linking just includes the library functions in the executable FILE
- delayed linking:
  - many different approaches: Windows does dll. dynamic load-time linking where the loader finds the .dll files and links to program just before it start running


Traditionally:
  - compilers: translate Fortran to x86-64 efficient execution
  - interpreters: execute BASIC programs directly via a machine language interpreter

Traditional Java
  - javac (compiler)
  - can be done on separate machines

```
+------------------+
Foo.java --> Foo.class --> | Java Interpreter |
 +------------------+
+--- databases server ---+ +----- client -----+
+------------------------------+
| JIT (Just In Time) Compiling |
+------------------------------+

Java Interpreter + bytecode -> machine code -> compiler
(counts #times
code gets executed) --> machine code
```

Dynamic Linking
----------------
A program can call the linker
  ("Please link in a JPEG decompression library")

f = ... (return a pointer to function)
f (...)

Java also performs some argument checking during program execution (run-time), but most argument checking is done statically by the compiler before a Java program executes. A Java compiler enforces a syntactic discipline on program text called static typing. The compiler uses a collection of type-checking rules to determine whether a program is well-typed or not. Programs that are not well-typed are rejected with an explanation of which rules were broken.

- Dynamic type-checking is the process of verifying the type safety of a program at runtime
- Static type-checking is the process of verifying the type safety of a program based on analysis of a program's source code.

Primitive vs. Constructed Types
--------------------------------
Primitive: Built-in types
Constructed: Built by programmer using type constructors

|abstract         |   exposed types|
-------------------|--------------------------
ops only way to make progress| ops + details about representation|
|users dont care about representation   | users know how types are laid out   |
|stdio.h <br>typedef struct FILE   |structs   |

```
struct complex {      +------+------+
  double re;          |  re  |  im  |
  double im;          +------+------+
}
```
- Abstraction. Omitting or hiding low-level details with a simpler, higher-level idea.
- Modularity. Dividing a system into components or modules, each of which can be designed, implemented, tested, reasoned about, and reused separately from the rest of the system.
- Encapsulation. Building walls around a module (a hard shell or capsule) so that the module is responsible for its own internal behavior, and bugs in other parts of the system can’t damage its integrity.
- Information hiding. Hiding details of a module’s implementation from the rest of the system, so that those details can be changed later without changing the rest of the system.
- Separation of concerns. Making a feature (or “concern”) the responsibility of a single module, rather than spreading it across multiple modules.

strongly typed
---------------
all operations are type checked (compile or run-time)

Java & OCaml are stronly typed
C/C++ are not

Strongly/Weakly vs Static/Dynamic
---
- Static/Dynamic Typing is about when type information is acquired (Either at compile time or at runtime)

- Strong/Weak Typing is about how strictly types are distinguished (e.g. whether the language tries to do an implicit conversion from strings to numbers).

structural equivalence vs name equivalence
----
- structural equivalence -- two types as the same if they consist of the same components. Same thing in memory.
- name equivalence -- each type declaration introduces a new type, distinct from all others.
- declaration equivalence -- two types are equivalent if they lead back to the same type.

subtypes
---------

Pascal: type 'lower' = 'a' .. 'z';
'lower' is subtype of 'char'

CommonLisp: (declare (type (and integer (satisfies evenp)) x))

* subtypes inherit operations of supertypes
* subtypes have more operatison than supertypes

s = char *
t = char const *

Is 's' a subtype of 't' or is 't' a subtype of 's'?
---> 's' is a subtype of 't'


char *p = ...;
char const *q = ...;

p = q; // not allowed because 'q' is a subtype of 'p'
q = p; // this works

coercion
---------
system converts types as need to make things work

a (float) + b (int) // coerce 'b' to type float

Overloading
-----
type of ad hoc Polymorphism

Parametric Polymorphism
------------------------
types contain type variables

* runtime type checking : type variables are just variables
* compile-time type checking : types are not objects
* fun f(a,b) = (a=b) has type ''a-> ''a -> bool because the a and b can be anything. doesn't have to be char
* In C++,
```
template<class X>  max (X a, X b){
  return a>b ? a : b ;
}
```

2 Ways to implement Parametric Polymorphism**
---
_1_-Templates (C++)
---
something that isn't complete until you know the type compile after instantiation

_2_-Generics (Java, OCaml)
---
- compile them right away
- type-check them right away


Is List<\String> a subtype of List<\Object> No it's not
---
The subtype of a some parent thing usuall has more operations

Duck Typing
------------
-Type checking based on behavoir only
  - assumes no compile-time checking
  - assumes flexible runtime, any object allowed
- Type checking done at method call (at runtime)
- Duck typing means that a piece of code requires that an object supports the operations that are used and nothing more.
```
1 + o <-- some random object
    ----> o.add(1)
```

Pros & Cons of Duck Typing
---------------------------
+ simplicity
+ flexibility -> easier to debug
- performance
- reliability -> runtime errors, not checked at compile-time

Implementing Generics
----------------------
```
           javac
foo.java ---------> Foo.class (bytecode) -----> JVM (run)
```
> Statement: Generic type information is not available at runtime in Java for backwards compatibility reasons.

What does it mean?
```
Type information is always ERASED. Imagine you have a
set of strings, you would (now) use Set<String> - but before generics were added it would be simply Set.
To ensure backwards compatibility when generics were added to Java (in 2004 with J2SE 5.0) the
type information is removed. So Set<String>
compiles to Set to allow compatibility with code written before generics were added.
```

ERASED (Java type erasure)
-------
- List: bytecodes know only about list
- Insert runtime test (type cast) that will always succeed
- Type erasure can be explained as the process of enforcing type constraints only at compile time and discarding the element type information at runtime. This means less overhead too

Bindings
---
- Relationship between a name and a value
- set of bindings = symbol table / environment

Example bindings:
```
int i = 10;
    value of variable: i+0
    address of variable: &i
'i' doesn't stand for '10' but to the variable which has value '10'
```
