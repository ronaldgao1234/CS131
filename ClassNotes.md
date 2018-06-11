# Class Notes
Metaprogramming: programming environment that you can write about your code in the language that you are using that can be used to generate code.

Orthogonality: how independent are they of each other

Java vs C:
- C: can't return array. can return pointer to array
- Java: Can return array
-
* Efficiency
  - space, time, power, network access

* Simplicity
  - Things should be as simple as possible (Albert Einstein)

* Convenience
  - Easy to use (write code, read code)

[Simplicity & Convenience CONFLICT]

Example: Convenient fbut not Simple
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

Example C Program.
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


   **This is the classical sequence**
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
Interface and Abstract class
---
Why do we use interface ?
- It is used to achieve total abstraction.
- Since java does not support multiple inheritance in case of class, but by using interface it can achieve multiple inheritance .
- It is also used to achieve loose coupling.
- Interfaces are used to implement abstraction. So the question arises why use interfaces when we have abstract classes?
- interfaces may be multiple interherited while abstract classes may not
- The reason is, abstract classes may contain non-final variables, whereas variables in interface are final, public and static
- Abstract classes are similar to interfaces. You cannot instantiate them, and they may contain a mix of methods declared with or without an implementation
- final classes prohibit subclasses

Creating Continuations
-----------------------
- relatively cheap operation

Problems
------
1. can bypass cleanup code
2. stack may not exist
  - *works only if 'setjmp's caller has not returned yet
3. *Scheme does not have this restriction!: Scheme continuations can be used even after the creating function, caller of 'call/cc' has returned.

Activation record
---
An activation record is another name for Stack Frame. It's the data structure that composes a call stack. It is generally composed of:

- Locals to the callee
- Return address to the caller
- Parameters of the callee

Green Thread
---
Use continuations to implement 'green threads'.
- green threads are like garbage collection
- instead of making developer deal with asynchronous(non-blocking) calls, the runtime sstem takes responsibility for this. like garbage collection it reduces code complexity
- they are user-level threads scheduled by an ordinary user-level process, not by the kernel. so they can be used to simulate multi-threading on platforms that don't provide that capability
- implemented at application level
- make a call and then provide a callback function or continuation to handle what to do with the result data
- so everything is done on single thread.
- instead of providing output of read to a variable we provide a
continuation to tell u what to do after
- Upsides: no more loops, cheaper, synchronization is easier
- Downsides: limited to one CPU core, not elegant looking, error handling not straightforward

Storage Management
-------------------
```
control storage to represent all aspects of program
  - objects of program (arrays, etc.)
  - I/O buffers
  - contents of variables
  - compiler temporaries
  - return addresses
  - location of activation records
  - code (program itself lives in memory)
    + program
    + libraries (including storage manager itself!)
  - storage metadata
```

1) static storage
   addresses are chosen before execution starts
     + simple (Fortran, 1956)
     - no recursion

2) stack storage
   LIFO for function locals
     + recursion
     + fast (2 ins/call)

3) heap storage
   not LIFO
     + flexible
     - expensive (random pieces of memory floating around)

Activation record == Stack Frame
----------------------------------
records state of currently executing or suspended function:
- **dynamic scoping**: look in caller, caller's caller
- **static scoping**: look in definer, definer's definer

Array Storage
--------------
```
* static (Fortran~56):
  figure out how many arrays, how large each arrays
  then lay them out in memory
    + fast
    - inflexible

* fixed stack-dynamic (C89)

array had fixed size
allocated dynamically on the stack
could declare array local to function, won't be laid out until function called

  int f(int x) {    // 32 other bytes
    int a[100];     // 400 bytes
    if (...) {                           <-----     subl $1232, %esp   (enter)
      int b[200];   // 800 bytes         <-----     addl $1232, %esp   (leave)
    }
  }

+ fast allocation
- inflexible (array size depend on function parameters?)


* varying stack dynamic (C99)

  int f(int x) {    // 32 other bytes
    int a[x];       // ? bytes                   no longer const, computed
    if (...) {                           <-----     subl $1232, %esp   (enter)
      int b[200];   // 800 bytes         <-----     addl $1232, %esp   (leave)
    }
  }

- dangerous (what if 'x' is negative?)      |         |
            (what if 'x' is extra large)    |         |
                                            +=========+
                                            | barrier |
                                            +=========+
      only works if smaller than barrier    |         |
        - check that array sizes >= 0 and   |       ^ |
          < max (depends on stack)          |       | |
                                            |       | |
     runtime check (omitted by default)     |       | |
      user programs bust beware!            |  stack  |
                                            +---------+

  int f(int x) {
    int a[100];
    if (...) {
      int b[200];    // 'b' valid only in 'if'
    } else {         // 'b' & 'c' can exist simultaneously
      int c[300];    // 'c' valid only in 'else'
    }
  }

'alloca(n)' : sp -= n, return sp
  lifetime = that of calling function

* without 'alloca' or dynamically sized arrays, we could simply add 'const'
  to %esp and get the stack top.

* with dynamic arrays we have to represent stack size, %esp, %ebp

+-------------------------------------------------------------------------+
| Scope vs. Lifetime                                                      |
| -------------------                                                     |
| Scope: set of places where variable is visible                          |
| Lifetime: set of instances of time during execution that variable eists |
+-------------------------------------------------------------------------+

```
Other Array Allocation Places
---
Heap (Java)
```
persistent (across executions)
  disk/flash
    I/O is slow (but you can batch it, and do it in background)
      not robust, may vary depending on OS
```


Thread-local Storage
---
- no locking required
Think of a random number generator where the seed must be maintained on a per-thread basis. Using a thread-local seed means that each thread gets its own random number sequence, independent of other threads.

If your seed was a local variable within the random function, it would be initialised every time you called it, giving you the same number each time. If it was a global, threads would interfere with each other's sequences.

Some more array ideas
----------------------
```
1) automatically-grown
     a[i] is always valid!?
       + avoid array allocation errors (array size)
       - performance, efficiency
       - subscript errors --> memory hogs

2) associative arrays (implemented with hash tables)
   e.g. Python dictionaries
     - iteration through them is
       (1) somewhat random
       (2) a bit slower
```

Strong vs. Weak Hash Associative Arrays
----------------------------------------
```
Strong: will get back whatever you stored into associative array

Weak: will get back either value, or 'I forgot the value'
    +- one that will spontaneously forget
    |
    +---> garbage collection

    --> "weak references"

A weak entity is one that can only exist when owned by another one. For example: a ROOM can only exist in a BUILDING. On the other hand, a TIRE might be considered as a strong entity because it also can exist without being attached to a CAR.
```

Heap Management
----------------
- coalesce free blocks
- split free blocks
- lessen fragmentation via roving pointer

**problem**: performance: 'malloc' is expensive

```
* without GC
* with GC

Q1: How to keep track of roots (point to heap but not part of heap)?

      stored: in registers
              on the stack in activation record or array

      these areas contain some roots and some other stuff
      roots allow u to know which stuff is alive. if u can reach root then u alive.
      how to distinguish roots?
      --------------------------
      1) when generating code, keep track of registers & other variables,
         if it contains pointer, compiler records which registers & stack
         locations are roots --> languages like Java

      2) compiler doesn't bother --> languages like C++, e.g.
         smaller programs but harder heap management

      3) there's just one root, e.g. %rdx points into activation records
         & activation records point to the heap


Q2: How to keep track of free space efficiently?

+--+--+---------+----------+--------+------+--------------------------+--+----+
|  |O1|         |    O2    |        |  O3  |                          |O4|    |
+--+--+---------+----------+--------+------+--------------------------+--+----+

represent free list inside free space

keep a piece of memory at start of each free block, and pointer that points to
next free block of memory
```

Problems
---------
1) external fragmentation
   no single free block that can satisfy request, even though
   we have enough total memory for the request
   - the various free spaced holes that are generated in either your memory or disk space
2) internal fragmentation
   restrictions on amount of memory that can be allocated
   for alignment, allocate wasted storage after objects
    - the wasted space within each allocated block because of rounding up from the actual requested allocation to the allocation granularity
```
first fit: walk through free list, carve off from end of free block
           O(N) : # free blocks, too many leadiing runts

best fit: O(N) unless fancy data structure

roving pointer: make free list circular data structure
                increase pointer each time we allocate


How to implement free(p)?
--------------------------
difficulty: efficiently coalescing adjacent free blocks

When allocating storage, give pointer to users, then store useful information
in the few words before the pointer: size, pointer to previous object/free
block, in-use flag. When freeing, we turn in-use flag off, and if off we can
coalesce the adjacent free blocks.
```

Memory Allocation
------------------
stack and heap

```
quick lists
------------
implement 'cons' quickly

  malloc (sizeof(void *) * 2)
          <-----8----->
          <--------16------->

  struct cons *free_cons;

    check this first when 'cons'ing
    when freeing, don't call 'free', just put on this list

    this bypasses 'malloc' (in normal case) & 'free'


  Suppose 80% of 'malloc' is 16 bytes &
          18% of 'malloc' is 48 bytes

  then we keep a free list for each independent 'size'

  Downside
  ---------
    may chew up extra memory that we won't use,
    but we don't care about memory these days as we care about speed
```
Heap management hassles
------------------------
```
(1) dangling pointers
    pointers into free'd storage

(2) memory leak
    allocate'd memory but never free'd

    roots (in stack or registers) that points to heap
    1. memory leak occurs when a block of memory is unreachable from a 'root'

    2. memory leak occurs when a block of memory is never accessed by program

      (!) performance issue only  -->  correctness issue
```
Garbage Collector
------------------
```
Handle the above issues automatically

  compiler tells you where the roots are
  compiler tells you the object layout

    C/C++ compilers don't help the memory manager (no GC)
    let's implement a GC for C,C++ (Emacs, GCC)


  Conservative Garbage Collector (run-time)
  ------------------------------------------
  doesn't know where the pointers are
  inspects entire stack and all registers looking for pointers
    has meta data on heap since it is memory manager

  assumes any bit pattern looking like a pointer is a pointer (may be wrong)
  if we see an object in a heap, we look for bit patterns recursively
    * it does leak memory but not significant to be worried about


  Typical Garbage Collector
  --------------------------

  (1) Mark     finds roots
    O(#inuse)  find all objects reachable

  (2) Sweep    go thru all objects
    O(#all)      clear mark bit
               or free object

  Is this going to work for multithreaded programs?
  Can we put the GC in a separate thread?

    (!) pause computation, do GC, then resume
        not real-time
        not scalable, larger the program, longer it freezes

    (!) 'malloc' is still slow


  Generation-Based Copying Collectors
  ------------------------------------

  heap
                      +--------------+--------------+
  +----------------+  | +---+  +---+ | +---------+  |
  | oldest objects |<-+ |   |  |   +-+ | nursary +--+
  +----------------+    +---+  +---+   +---------+


  old objects tend to not point to new ones

  GC rarely looks at old objects
  GC focuses on 'nursary'


  fast malloc via nursary
  ------------------------

  +-------------+--------+----------------------------+
  | new objects |        | <--------- free ---------> |
  +-------------+--------+----------------------------+
  ^                  ^   ^                            ^
  |                  |   |                            |
  bp                 |   hp                           lp
                     |
                  new obj

  increment 'hp' and we get new obj

  'malloc' is fast


  copying collector
  ------------------

  <----cacheline----><----cacheline----><----cacheline---->
  +--+--+-----------+-------+--------+--------------------+ old nursary
  |  |  |     *     |       |    *   |        free        |
  +--+--+-----|-----+-------+----|---+--------------------+
              |                  |
        +-----+    +-------------+
        |          |
  +-----|-----+----|---+----------------------------------+ new nursary
  |     *     |    *   |               free               |
  +-----------+--------+----------------------------------+
  <----cacheline----><----cacheline----><----cacheline---->


  copy 'non-garbage' to new nursary

    - update all pointers to objects
    + fast 'new'
    + O(#inuse)
    + using cache more efficiently
      cache is much faster than RAM
```

Python Memory Management
----
```

CPython
--------
does garbage collection atop lower level
finds garbage, then calls 'free' on C level

via. reference counting
------------------------
each object has extra word that counts #references to obj

  +---+
  | p |----+
  +---+    |
           |        +---+---------+
           +---+--> | 2 | "hello" |
               |    +---+---------+
  +---+---+    |
  | c | q |----+
  +---+---+

every assignment     decrements reference count of old object
                     increments reference count of new object


Issues
-------

- assignment is >= 3x expensive
+ garbage collection is easier
  when reference count is 0, then it is garbage, reclaim it immediately
- room for reference counter
    how large?
      convention: use 16 bits
        if reference count is (2^16 - 1), object lives forever
- circular references

    +-------------------+
    |   +---+         +-|-+
    +-> | q |   +---> | p |
        +-|-+   |     +---+
          +-----+

  write program carefully

    def f(x):
      d1["a"] = d2
      d2["b"] = d1

      <--- computation --->

      d1["a"] = null  # basically same to 'free'


  Currently CPython has two-level garbage collector
    reference count regularly
    mark + sweep fall back

+ finalization

  Java
    finalize called before your object becomes garbage

  for a reference-count-based approach where you have no cycles
  finalzie is called immediately
    free any resources & close any connections


JPython
--------
built atop JVM

(1) finalize isn't called immediately
(2) JVM has two heaps
    "copying heap"        (contains most objects)
    "mark + sweep heap"   (finalization-needing objects)
```

Multithreaded Allocators
-------------------------
```
still want 'new' to be fast

+-------+---+---------------+
|       | ^ |               |
+-------+-|-+---------------+
   old hp | hp              lp
          |
       new obj

for multithreaded we may get two objects at same location

(1) lock around 'malloc'

    1. heap bottlenecks
       give each thread same heap (nursary), still retain locality

    2. real-time garbage collector
       need hard upperbound on each operation
       'new x()' takes at most '10000' instructions (have instruction budget)

       incremental garbage collector
       ------------------------------
       for each time calling 'new', do some more work (some garbage collection)
         way slower than nursary version
```
Performance Tricks (that don't always work, have become obsolete)
------------------------------------------------------------------

```
(1) quick lists

    assume 'malloc' is slow, want to become fast
    keeping individual 'size list'

      obsolete if we have copying collector --> becomes slow list
      (!) copying collector copies the 'free list'

(2) explicit nulling

    def f(x):
      # d1 using
      # not using d1 (GC can free d1 here)

      # cannot free 'd1' because we will 'use' it later

      d1["b"] = null  # break cyclic data structure to find garbage
                      # maintain 'd1' because we are 'using' it
      d2 = null       # tell garbage collector we don't need 'd2'


    (!) pain to maintain
    (!) slows program down
        increase storage use if assume copying collector

    while (true) {
      # do work
      System.GC()   # greatly slows down larger applications
    }               # expensive to do GC if we have many objects
```

class
---
```
--------------------------------------------------------------------------
  class-based              vs.             prototype based
--------------------------------------------------------------------------

C++, Java, OCaml, Python                 (have no classes)

    o = new C()                              p.clone()
    o.clone()

(new is a packaging of clone)                (simpler)

                                        use prototypes (just objects)
                                        in place of classes

                                        + simpler (need clone() anyway)
                                        + can help performance
                                        - easy to become disorganized
                                        + more flexible
                                        - can't easily use static typing
                                          (buggier, slower)
```

Parameter Passing (key notation)
---------------------------------
```
* correspondence issue

    positional, names, variable number of arugments

* implementation strategies

    want something that is fast, clear

    +---------------+
    | call by value |
    +---------------+

      - caller evaluates the expression
      - passes a copy of value to callee
      - callee operates on copies

        + simple
        + clear
        + fast
        - slow for big objects

        C, C++, OCaml, Scheme

    +-------------------+
    | call by reference |
    +-------------------+

      - caller evaluates addresses of arguments
      - callee's responsibility to dereference these pointers
      - callee can modify arguments

        + pretty simple
        + fast for arrays
        - aliasing

        +---------------------------------------------------------------------+
        |                                                                     |
        |   possible solutions to alias problem                               |
        |   ------------------------------------                              |
        |                                                                     |
        |   Fortran : behavior is undefined if you alias                      |
        |                                                                     |
        |             + get performance                                       |
        |             - lose reliability, clarity                             |
        |                                                                     |
        |   C/C++   : 'noalias' keyword --> same as Fortran convention        |
        |                                                                     |
        |   Ada     : alternate calling conventions                           |
        |                                                                     |
        |             +----------------+                                      |
        |             | call by result |                                      |
        |             +----------------+                                      |
        |                                                                     |
        |               - caller passes address to callee                     |
        |               - callee operates on a copy                           |
        |               - just as it returns, copies result back              |
        |                                                                     |
        |             +----------------------+                                |
        |             | call by value-result |                                |
        |             +----------------------+                                |
        |                                                                     |
        |               - callee operates on a copy                           |
        |               - copy is copied back on return                       |
        |                                                                     |
        |                 int f (int vr x) {                                  |
        |                   x++;                                              |
        |                 }                                                   |
        |                                                                     |
        |                 int f (int *px) {              int f (int *px) {    |
        |                   int x = *px;                   (*px)++;           |
        |                   x++;                 OR      }                    |
        |                   *px = x;                                          |
        |                 }                                                   |
        |                                                                     |
        +---------------------------------------------------------------------+

        - expensive or invalid arguments

        +---------------------------------------------------------------------+
        |                                                                     |
        |  solutions                                                          |
        |  ----------                                                         |
        |                                                                     |
        |    +--------------+                                                 |
        |    | call by name |                                                 |
        |    +--------------+                                                 |
        |                                                                     |
        |      - caller passes a thunk (parameterless procedure) such that    |
        |        when you call the thunk, it rturns the argument address      |
        |      - callee: when it needs the value, it calls the thunk          |
        |                                                                     |
        |                                                                     |
        |        void printavg (int avg, int nstudents) {                     |
        |          if (nstudents == 0)                 sum = 0                |
        |            print ("NA!");               ==>  sum += o[i]            |
        |          else                                printavg (sum/n, n)    |
        |            print("average is:", avg);                               |
        |        }                                                            |
        |                                                                     |
        |                                                                     |
        |        void printavg (int name avg, int nstudents) {                |
        |          if (nstudents == 0)                 sum = 0                |
        |            print ("NA!");               ==>  sum += o[i]            |
        |          else                                printavg (sum/n, n)    |
        |            print("average is:", avg);        (lambda()(sum n))      |
        |        }                                                            |
        |                                                                     |
        |                                                                     |
        |        + avoids unnecessary copies and executions                   |
        |        - a bit slower than ABI (think API)                                     |
        |        - way slower if expression is expensive (evaluate twice)     |
        |                                                                     |
        |    +------------------------+                                       |
        |    | call by need (Haskell) |                                       |
        |    +------------------------+                                       |
        |                                                                     |
        |      - call by name, except callee caches result of internal calls  |
        |                                                                     |
        |        + fixes "way slower" problem above                           |
        |        + accesses after the first call are fast                     |
        |        + good match for functional programming                      |
        |        +  infinite data structures are supported                    |
        |                                                                     |
        |                                                                     |
        |      lazy evaluation                                                |
        |      ----------------                                               |
        |      call by need for everything                                    |
        |                                                                     |
        |      eager evaluation                                               |
        |      -----------------                                              |
        |      call by value                                                  |
        |                                                                     |
        +---------------------------------------------------------------------+

        C++

           what you see                 code
          --------------               ------
          int f (int &v) {        int f (int *pv) {
            return v+1;             return *pv+1;
          }                       }

          int a;                  int a;
          f (a);                  f (&a);

```

## Error Handling - ways to handle errors
---
compile-time checks
--------------------
```
static checking

  + most reliable
  - least flexible
  - hardest to implement in general
    e.g. dereferencing null pointers?
```
- can help make sure it satisfies interface

precondition
-------------
- check in beginning with try catch
- post condition, just use assertions
- invariants are things that shouldn't change. use this to check if some multithreaded app messed something up that should never be mess up. like a balanced tree
```
caller's responsibility
runtime property, partly of API's

  int i, j;
  i/j  -->  precondition: j != 0 && !(i == INT_MIN && j == -1)

behavoir undefined if precondition is not satisfied

  + fast
  - reliability is a problem (preconditions not checked)
```

total definitions
------------------
```
use special values for errors (IEEE floating point) (system calls)

  + relatively simple
  + relatively fast
  - lazy programmers omit checks (requires programmers to check for errors)
```

fatal errors
-------------
```
exit()
_exit()
abort()  -->  always crash + dump core

can check preconditions and exit() or abort()

  + more reliable than preconditions
  + more flexible
  - fatal
```

exception handling
-------------------
be similar to fatal errors but don't crash or exit
```
  Java
  -----
  (1) define exception objects that form a hierarchy
  (2) if a function can throw an exception, it must be declared

  try {
    // some code with errors (indirectly)
  } catch (IOException e) {
    // code that deals with 'e'
  }

  omit all errors

  try {
    // some code
  } catch (Exception e) { }
```

argument for exception handling
--------------------------------
```
(1) makes code simpler to read (only in simple examples)
(2) makes code more reliable
```
argument against exception handling
------------------------------------
```
(1) makes code harder to read

    a = allocate();
    try {
      x = f(a);
      y = a(x);
    } finally {
      free (a);
    }

(2) lazy is as lazy does (lazy programmers can still ignore exceptions)
```

## Cost models - can dominate some apps!
--------------------------------------
mental models of resources needed to run
```
  - O(n) vs tuning  (constant factor)
  - what are you costing?
    - time                  ---+
    - power/energy             +--->  $$$
    - memory                   |
    - network use (I/O use) ---+

    +------+
    | time |
    +------+

    classic example: lists
    -----------------------
    Scheme:      car   O(1)
                 cdr   O(1)
              append   O(n)
    Python:   append   O(1) amartized


    more examples
    --------------
    Scheme:      (eq? a b)   O(1)
                (eqv? a b)   O(min(a,b))
              (equal? a b)   O(INF)
    Prolog:         X = Y    O(min(X,Y))

```
procedure call costs (assume call by value)
--------------------------------------------
```
          +---------------------+
caller    | evaluates arguments |
          +---------------------+
          copies values to registers
          save return address
          jump to callee start

callee    allocates frame
          save registers as needed
          +--------------+
          | do real work |
          +--------------+
          copy results to return register
          deallocate frame
          jump back

things not in box are overhead

how to avoid overhead?

  - inlining (removes most or all overhead)
    Definition of inlining: a compiler optimization that replaces a function call site with the
    body of the callee. This optimization may improve time and space usage at runtime,
    at the possible cost of increasing the size of the final program

  - tail call optimization
    - does not need to save return address
    - can reuse frame
    - does not need to save registers
```

Escape analysis
----------------
```
compiler statically looks for what places a new's result can be

  Point location() { return new Point(x,y); }
  void showLocation {
    Point p = o.location
    System.out.println("@" + p.x + p.y)
  }

  compiler can put 'Point p' on the stack here since it goes out of scope
  when function ends. It is not passed to other functions.


COST MODELS CHANGE FASTER THAN ANY OTHER THINGS RELATED TO THE SUBJECT
```

Semantics
----------
what does a program mean? (as opposed to syntax, which is "easy")
BNF, EBNF

static semantics (intermeddiate)
---------------------------------
semantics of the program before it is running
```
  type checking
  scope checking

  attribute grammars
  -------------------
  basic idea

    (1) symbols have attributes
    (2) rules specify constraints on attributes

        E1 -> E2 * E3
           type(E1) = if type(E2) = int & type(E3) = int
                      then int
                      else float

           symtab(E2) = symtab(E1)
           symtab(E3) = symtab(E1)


        synthesized attribute
        ----------------------
        parent value is defined by children


        symtab attribute
        -----------------
        maps identifiers to compile-time binding (e.g. types)

        suppose the dependency graph loop
          (1) check for loops while builidng
          (2) prove that loops are impossible (normally taken)


        inherited attributes
        ---------------------
        children's attributes are function of parents

        +------------------------------------------------+
        |                                                |
        |   int f (int y) {                              |
        |     int x = y;                                 |
        |     return x + y;                              |
        |   }                                            |
        |                                                |
        |   body -> decl stmt                            |
        |   symtab(stmt) = symtab(body) U newsym(decl)   |
        |                                                |
        |              body                              |
        |              /  \                              |
        |             /    \                             |
        |          decl    stmt                          |
        |                                                |
        +------------------------------------------------+

  +-----------------------------+
  |                             |
  |   BNF inspired parse tree   |
  |                             |
  |          a + b * c          |
  |                             |
  |                             |
  |          + (type)           |
  |        /   \                |
  |       /     \               |
  |      /       \              |
  |     /         \             |
  |    /           \            |
  |  ID (type)      * (type)    |
  |  |            /   \         |
  |  a (int)    ID     ID       |
  |             |      |        |
  |     (float) b      c (int)  |
  |                             |
  +-----------------------------+
```


dynamic semantics (hardest)
----------------------------
```
semantics of the program as it is running
  when you run the program what does it do


+--------------------------+
| operational (imperative) |
+--------------------------+

In order to define the semantics of language L, we write an interpreter for it
that accepts a language-L program P as input, and runs P, produces output.
```

Problems
---------
```
  (1) some features may be unimplementable
  (2) suppose interpreteris written in M, N, C...

      define the semantics of Lisp by writing a Lisp interpreter!

      could load the Lisp interpreter into machine and run the Lisp interpreter
      to check if it had same behavior as the Lisp machine

      LI : semantics of L -> semantics of L (take the fixed point!)
```

ML Grammar
-----------
```
<E,C> -> V

  E : expression
  C : context -> maps names to values
  V : value

+--------------------------------------------------+
|                                                  |
| <E1,C> -> V1 , <E2,C> -> V2                      |
| ---------------------------                      |
|      <E1+E2,C> -> V1+V2                          |
|         |           |                            |
|         |           +-----> mathematical 'plus'  |
| 'plus' in ML source code                         |
|                                                  |
+--------------------------------------------------+

+--------------------------------------+
|                                      |
| <K,C> -> K        'K' is a constant  |
|                                      |
+--------------------------------------+

+----------------------------------------------------------------+
|                                                                |
| <V,C> -> C(V)     apply context to variable (context matters)  |
|                                                                |
+----------------------------------------------------------------+

+------------------------------------------------------------------+
|                                                                  |
|                     +---> bind V1 to x and produces new context  |
|                     |                                            |
| <E1,C> -> V1 , <E2,bind(x,V1,C)> -> V2                           |
| --------------------------------------                           |
|       <let x = E1 in E2,C> -> V2                                 |
|                                                                  |
+------------------------------------------------------------------+

+--------------------------------------------------------------------------+
|                                                                          |
| <fun x->E,C> -> D(x,E,C)                                                 |
|                 |                                                        |
|                 +-----> create data structure and bind (don't evaluate)  |
|                                                                          |
+--------------------------------------------------------------------------+

+----------------------------------------------------------------+
|                                                                |
|           +---> create a function                              |
|           |                                                    |
| <E1,C> -> D(xf,Ef,Cf) , <E2,C> -> V2 , <Ef,bind(xf,V2,Cf) -> V |
| -------------------------------------------------------------  |
|                         <E1,E2,C> -> V                         |
|                                                                |
| dynamic scoping here if we use 'bind(xf,V2,Cf)'                |
|                                                                |
| ML uses static scoping so when we bind the data structure to   |
| create function we keep the context to use later               |
|                                                                |
+----------------------------------------------------------------+

eval(call(E1,E2), C, V) :-
  eval(E1, C, lambda(xf,Ef,Cf)),
  eval(E2, C, V2),
  eval(Ef, [xf=V2|Cf], V).



+-------------------+
| axiomatic (logic) |
+-------------------+

{P} S {Q}

if propotision P is true before executing the statement S, and if S terminates
then Q is true afterwards.


             +--> assume no side effects here
             |
{Q[x/E]} x = E; {Q}
 |
 +--> take 'Q', and substitute all free occurrences of 'x' with 'E'


  {x < -1}  x = x + 1;  {x < 0}

  {x + 1 < 0}  x = x + 1;  {x < 0}
               x     E        Q


+---------------------------+
|         assingment        |
|                           |
| P -> Q, {Q} S {R}, R -> S |
| ------------------------- |
|         {P} S {R}         |
+---------------------------+

+-----------------------+
|       sequencing      |
|                       |
| {P} S {Q} , {Q} T {R} |
| --------------------- |
|     {P} S ; T {R}     |
+-----------------------+

+--------------------------------------------+
|                if then else                |
|                                            |
| {P^E} S1 {Q} , {P^~E} S2 {Q}               |
| ----------------------------               |
|   {P} if (E) S1 else S2 {Q}                |
|           |                                |
|           +--> assume no side effects here |
+--------------------------------------------+

+-------------------------------------------------------+
|                    while loops                        |
|                                                       |
|                   {P^E} S {P}                         |
|              ---------------------                    |
|              {P} while(E) S {P^~E}                    |
|               |                                       |
|               +--> loop invariant                     |
|                                                       |
|                                                       |
|          {0 < i ^ 10 < i} i = i/10 {0 < i}            |
|   -------------------------------------------------   |
|   {0 < i} while (10 < i) i = i/10 {0 < i ^ i <= 10}   |
|                                                       |
+-------------------------------------------------------+


+---------------------------+
| demotational (functional) |
+---------------------------+

Lambda Calculus
----------------


lambda expressions
-------------------

             x         variable name
  (lambda x).M         lambda expression
         (F A)         both 'F' and 'A' are lambda expressions


lambda reduction
-----------------

((lambda x).M A) ==> M[x/A]
-------------+-------------
             |
             +--> Church + Rosser (UCLA)


(lambda(x).(x y) (lambda x).x) ==> ((lambda x).x y) ==> y
             M         A                       M A

((lambda x).(x x) (lambda x).(x x)) ==> ((lambda x).(x x) (lambda x).(x x))
                                    ==> ... ==> ...


((lamda y).z ((lambda x).(x x) (lambda x).(x x))) ==> ... (call by value)
           M                  A
  ===> z (call by name)
```
