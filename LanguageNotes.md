# OCaml
----------
## Basic Properites
* Good support for functions + functional forms (much better than in Java or C)
* **Compile-time type checking (like C++, Java) (unlike Python, Scheme)
* Heavy-duty type inference
* No need to worry about storage management, has garbage collection
  (unlike C/C++) (like Java, Python)
* strongly typed - no implicit conversions
* structurally equivalent

\# if 3 < 5 then "a" else 0;;-> <br>
[error, wrong type] <br>
\# ();;     <br>
-: unit = ()<br>
\# [];;<br>
-: 'a list = []<br>
\# [1; 3] @ [5];;<br>
-: int list = [1; 3; 5]<br>
\# fun f(a,b) = (a=b)<br>
=: ''a * ''a -> bool

Random problems:

1.Write a function last : 'a list -> 'a option that returns the last element of a list.
```OCaml
# let rec last = function
    | [] -> None
    | [x] -> Some x
    | _ :: t -> last t;;
val last : 'a list -> 'a option = <fun>
```

2.Find the last but one (last and penultimate) elements of a list.
```OCaml
# let rec last_two = function
    | [] | [_] -> None
    | [x;y] -> Some (x,y)
    | _::t -> last_two t;;
val last_two : 'a list -> ('a * 'a) option = <fun>
```

3.Find the k'th element of a list.
```OCaml
# let rec at k = function
    | [] -> None
    | h :: t -> if k = 1 then Some h else at (k-1) t;;
val at : int -> 'a list -> 'a option = <fun>

4.Find the number of elements of a list.
```OCaml
# (* This function is tail-recursive: it uses a constant amount of
     stack memory regardless of list size. *)
  let length list =
    let rec aux n = function
      | [] -> n
      | _::t -> aux (n+1) t
    in aux 0 list;;
val length : 'a list -> int = <fun>
```
5.Reverse a list
```OCaml
# let rec rev l [work to be done] a [work already done] =
  match l with
  | [] -> a
  | h::t -> rev t (h::a);;
val rev: a' list -> 'a list -> 'a list
```
-----------------
Labeled namespaces (partial function from names to values)
--> Motiviation:
  - manage complexity (for reader)
  - ability to separately compile (efficient rebuilding)

OCaml namespace management
---------------------------

Structures
-----------
```
module qu =
  struct
    type 'a queue =
      | Empty
      | Node of int * 'a * a' queue
    ===== IMPLEMENTATION OF PRIORITY QUEUE =====
  end
  ```


OCaml Signatures
-----------------
```
module type q =
  sig
    type 'a queue
    (isempty decl)
    (other decl)
  end
  ```


# Java
----------
- statically typed
- strongly typed
- name equivalence
- single inheritance
- Garbage collector works by tracking live objects and everything else is designated garbage. not other way around
- To achieve its goal of "Write once, run anywhere," Java does both: a Java compiler converts Java code into machine-readable bytecode, then the Java Virtual Machine interprets the code for the computer it runs on.
- allocate heap in advance to be managed by JVM while program is running.
  - This means object creation is faster because global synchronization with OS is not needed for every single object  An allocation simply claims some portion of a memory array and moves the offset pointer forward (see Figure 2.1). The next allocation starts at this offset and claims the next portion of the array.
  - When an object is no longer used, the garbage collector reclaims the underlying memory and reuses it for future object allocation. This means there is no explicit deletion and no memory is given back to the operating system.
- JIT is faster:
```
  A JIT compiler runs after the program has started and compiles the code (usually bytecode or some kind of
VM instructions) on the fly (or just-in-time, as it's called) into a form that's usually faster, typically
the host CPU's native instruction set. A JIT has access to dynamic runtime information whereas a standard
compiler doesn't and can make better optimizations like inlining functions that are used frequently.
  This is in contrast to a traditional compiler that compiles all the code to machine language before the
program is first run.
  To paraphrase, conventional compilers build the whole program as an EXE
file BEFORE the first time you run it. For newer style programs, an assembly is generated with
pseudocode (p-code). Only AFTER you execute the program on the OS (e.g., by double-clicking on its icon)
will the (JIT) compiler kick in and generate machine code (m-code) that the Intel-based processor
or whatever will understand.
```
Java Information Hiding
------------------------
Label each name to control visibility
```
+-----------+--------------+-----------+---------+------------+
|           | within class | everyelse | package | subclasses |
+-----------+--------------+-----------+---------+------------+
|  public   |     yes      |           |   yes   |    yes     |
+-----------+--------------+-----------+---------+------------+
|  private  |     yes      |           |         |            |
+-----------+--------------+-----------+---------+------------+
| protected |     yes      |    yes    |   yes   |            |
+-----------+--------------+-----------+---------+------------+
|  (none)   |     yes      |           |   yes   |            |
+-----------+--------------+-----------+---------+------------+
```

- arrays are objects
- arrays are allocated via new on the heap
- size determined dynamically when allocated
- runtime checking is easy (since the size is included)

# Prolog
----------
- **Variables are capitalized**
- searches top to down, left to right, backtracks
- goals are evaluated depth first search
- More efficient method usually has 1 more variable as accum
- Unification: matching goals to clause heads, binds variables
- infinite term: ?- x = f(x)
- ! stops backtracking
- **ORDER MATTERS!**
1) facts      heads only             append([],L,L).
2) rules(clause)      heads + bodies         head :- nonempty body
3) goals      no head + bodies       ?- append(A,B,[]).
4) predicate is one or more clauses
- backwards chaining from goals through rules to facts
- clauses are treated left to right to match goals
- goals are evaluated left to right
1.Length
```
length([], 0).
     length([_|R], L) :-
       length(R, RL),
       L is RL + 1.

```
2.Append
```
The first list appended onto the second list is the third list.
      We need to define the relationship between these three things, and that is our program.

      myappend([],R,R).
      myappend([X|Y], L2, [X|R]) :-
        myappend(Y, L2, R).
```
3.Reverse
```
reverse(List, RevList) :- revacc(List, [], RevList).
     revacc([H|T], Acc, R) :- (T, [H|Acc], R).
     revacc([], Acc, Acc).
```

Equality stuff:
```
X = Y
(X is equal to Y, if X and Y match)
X == Y
(X is literally equal to Y, if X and Y
 are identical)
X \== Y
(X is not literally equal to Y - for
 arbitrary terms X and Y)
X =:= Y
(the value of X equals the value of Y)
X =\= Y
(the value of X is not equal to the
 value of Y)
X is Y
(if X matches the value of Y, where X
 is a variable or a constant, and Y is
 an arithmetic expression)
 ```

 Syntactic Sugar
 ----------------
 ```
 []       =  '[]'
 [x|L]    =  '.'(x,L)
 [x,y|L]  =  '.'(x,'.'(y,L))
 [x,y,z]  =  '.'(x,'.'(y,'.'(z,[]))))
 ```

 Operators
 --------
 ```
x + y  =  '+'(x,y)
-x     =  '-'(x)
x - y  =  '-'(x,y)
x , y  =  ','(x,y)     AND
x ; y  =  ';'(x,y)     OR
x :- y =  ':-'(x,y)    IF
```
Performance because of Order
---
```
sort(L, S) :- sorted(S), perm(L, S)
The Prolog interpreter does a left-first depth-first search. As a result, the new clause would have better
performance for certain questions. The performance will remain the same for question like
sort([4, 3, 5], [3, 4, 5]). It would immediately check if [3, 4, 5] is a sorted version of [4, 3, 5],
after which it will check if [3, 4, 5] is a permutation of [3, 4, 5]. For the original clause,
it would first try to check if [3, 4, 5] is a permutation of [4, 3, 5]
```
# Scheme
----------
- with tail recursive call never have stack overflow
- evaluated in any order, left to right, right to left, procedure before arguments isn't necessary
- Continuation restriction: *Scheme does not have this restriction!: Scheme continuations can be used even after the creating function, caller of 'call/cc' has returned.
- procedure is evaluated in the same way as arg1 ... argn. While procedure is often a variable that names a particular procedure, this need not be the case. See ((car (list + - * /)) 2 3). Here, procedure is (car (list + - * /)). The value of (car (list + - * /)) is the addition procedure, just as if procedure were simply the variable +.
Scheme Characteristics
- '() is the empty list
------
| Characteristics| Like | Unlike|
|----------------|-----:|-------:|
|Objects are allocated dynamically and neveer freed, thus assume there is a 'heap' and a 'GC'  | Java, ML, Lisp   | C, C++  |
|types are LATENT or IMPLICIT TYPING (associated with values at run-time) , not MANIFEST or EXPLICIT TYPING(associated with names, variables, functions)  | Prollog Lisp  | ML, Java, C, C++   |
| static scoping   | ML, Java, C, Prolog, Python  | Lisp    |
|  call-by-value functions, evaluates all arguments first then evaluate function by coping arguments |  ML, Java, C, C++, Lisp | C++(&), Prolog    |
|large collection of builtin objects, pairs (+lists), numbeers, vectors, strings, procedures (including continuations)   | none  | all others   |
|simple syntax, data easily represents program    | Lisp, Prolog   | Java, C, C++, ML   |
|tail recusion is required of the implementation of Scheme (recursion not allowed to grow stacj if we do only tail calls) (last instruction calls itself and returns value, implementation does not grow stack)   | mostly none    | most others  |
|nice arithmetic, no integer overflow (2^31) exact rationals (1/3==1/3) which decreases performance | mostly none   | most others    |
|   |   |   |
```
let d = 2 in
let f = λx. x + d in
let d = 1 in
f 2
static scoping evalues the inner d to 2
dynamic scoping evaluates the inner d to 1 since d = 1 is most recent
```
Dynamic scoping
---
```
|  + easy to explain                                            |
|  + lets you specify alternate environments                    |
|      expot PATH=/usr/local/cs/bin:$PATH                       |
|  - run-time scope checking required (variable not defined)    |
|  - reliability                                                |
|  - performance
```

- numberic equality: =
- "pointer" reference comparison: eq?
- "contents" comparison: eqv?
- recursive comparison: equal?

"goto" in Scheme
-----------------
(goto k) ==> (ip, ep) = k

Syntax: simply call it, alters (ip, ep)
  (k expr)

# Python
----------
- Dynamically typed
- strongly typed
- run-time language
- __init__(self) is like constructor for classes in python


classic Python builtin types
-----------------------------
```
(1) None (null pointer) (OCaml unit())

(2) numbers :   Int       Long     Float Complex Boolean (1, 0)
               bounded  unbounded
                fast     slower
                       no overflow

(3) sequences : String    Unicode     XRange    Tuple   List Buffer
                 byte    character   sequence             Mutable
               strings    strings      with
                                     pattern


```
Sequence operations
---
```
(1) s[i]  ( -1 <= i < n )
      0th-origin indexing

    s[-1]

(2) s[i:j]
      sub-sequence from 'i' (inclusive) to 'j' (non-inclusive)

    s[i:]
      defaults to 'n'

    s[:j]
      defaults to '0'

  +--------------------+
  | Python     Scheme  |
  +--------------------+
  |  s[0]      (car s) |
  | s[1:]      (cdr s) |
  +--------------------+

(3) s[i] = v (mutable sequences only)

    s[i:j] = s1
      copy sequence into subsequence
      can change length of 's'

    del s[i:j]
      delete subsequence s[i:j]

    del s[i]
      delete s[i]
```
List Operations
----------------
```
(1) s.append(v)
      1) append 1 item 'v' to 's'
      2) fast, O(1) on average

      +---+---+-----+
      | * | n | max |
      +-|-+---+-----+
        |
        |   +-+-+-+-+-+-+-+-----+-+
        +-> | | | | |/|/|/| ... |/|
            +-+-+-+-+-+-+-+-----+-+
            0       n             max

(2) s.extend(s1)

(3) s.insert(i,v)
      insert 'v' before 'i'-th element of 's'

(4) s.pop(i)
    s.pop() == s.pop(-1)

(5) s.reverse()

(6) s.sort()
      assumes generic comparison
```
Mappings: Dictionary Operations
--------------------------------
```
(1) d[k]
    d[k] = v
      'k' can be any immutable object
      makes multithreading practical

      use h(k) (hash function for finding key-object relationship)

(2) del d[k]

(3) d.has_key(k)
      check if 'd' has 'key' to prevent subscript errors

(4) d.get(k[,v]) ('v' is optional)
      returns 'd[k]' if 'v' is defined
      otherwise return 'None'
```
Callables
----------
```
Function, BuiltinFunction
Class
Method  ----------->  (class, object, function)
UnboundMethod ----->  (class,         function)
Generator ----------> can 'yield', not 'return' (coroutines)



def f(x):                      (define (f x)
    return x + 3                   (+ x 3))

f = lambda x : x + 3           (define f
g = f                              (lambda (x) (+ x 3)))
f(2)
g(12)


arctan(x = 2.9, y = 1.7)
  do a function call with names matching formal parameters


def printf(format, *args, **namedargs):
    ......

printf("%d, %s\n", 29, "abc", quoting_style = 3, output = stdout)

-> {'quoting style': 3, 'output': stdout}
```

Duck typing
------------
```
you can define your own numbers, sequences, etc.
you have to implement the basic operations, e.g. n.__add__(m)
```
# Overall
-----

|Name | Ocaml | Scheme | Java | Python | Prolog |
| ---|-------|----------|------|----------|---------|
| Typing   | Strong and static   | Weak and dynamic | Static & strong    | Strong and dynamic   | weak and dynamic   |
|Memory Allocation |Runtime uses heap from OS to hold heap blocks which it fills up in response to allocation reqests from program  | stack for recursive procedure calls. Heap for dynamically allocated stuff  | Dynamic only, eveerything allocated on the heap | Memory management in Python involves a private heap containing all Python objects and data structures    |  static  |
|Memory Management | Uses Stop and Copy (removes fragmentation in memory) and Mark and Sweep (marks unreferenced areas in memory an frees them up)   | GC  | GC   |heap, static memory allocation      |GNU Prolog lacks garbage collection for both the heap and for the atoms    |
|Run type   | Compiled |Interpreted/Compiled   | Compiled  | Interpreted   | Compiled and interpreted  |   |
| Evaluation strategy  | Strict   | Partially lazy evaluation using keyword delay  | Strict and call-by-value  |Lazy   |  Lazy |   |
| Concurrency/Parallelism  | None  | Multi-threaded and supports Parallelism  | Extensive support for multi-threading, volatile, atomic variables, ...  | Single-threaded, asynchronous ocncurrency using an event loop (asyncio)   | None  |   |
|scoping   | static  |  static |  static | static  | static  | static |


## _Defnitions:_

---
Scoping:
- static - compiler first searches in the local block, then surrounding blocks, then the global variables
- dynamic - searches the current block then all the successive calling functions

Typing:
- static: Every variable name is bound to both an object and a type (at compile time via a data declaration )
- Every variable name is bound only to an object (unless its null)
- weak: variables can be implicitly coerced to unrelated types. e.g. int x = 5.0 is legal
- Strong: type conversions must be explicit e.g. in Python, print (str(4))

Run-Type:
- compiled: code is stored as a binary as instructions the CPU can directly execute
- interpreted: code is stored as a source and must be translated to machine code by interpreter at runtime

Memory-allocation:
- static: allocation of memory at compile time; allocated on stack, one for each function, does not require any runtime memory management since the loader finds space for all statically allocated blocks of data before the program begins running
- dynamic: allocation of memory at runtime, usually via calls like malloc; allocated on heap
- automatic: allocation of memory on entrance of a new scope (e.g. function, loop body, etc.) allocated on stack

Evaluation-strategy:
- strict: an expression is evaluated as it is bound to a variable (or function argument) = eager
- eager: function arguments are evaluated before the funtion call. More common than lazy.
- lazy: delas the evaluation of an expression until its value is read/accessed in the functions. call by need and call by value
- greedy: evaluated as soon as it is bound to a variable
- call-by-name: the argument is evaluated every time it is used
- call-by-need: evaluated the first time it is used  and the value recorded so that subsequently it need not be re-evaluated.
- call-by-value: Creates new copies of the function arguments to pass into function
- call-by-reference: Passes the location/address/reference of the arguments rather than a new copy

multiple-inheritance
---
```
--------------------------------------------------------------------------
multiple inheritance                vs.       no multiple inheritance
--------------------------------------------------------------------------
   C++, Python                                        Java

+ combine independent classes into        + no tricy structures (duplicated
  one that shares both behaviors            function names)

--------------------------------------------------------------------------
```

A subclass typically inherits from a superclass or maybe implements and interface (Java)
A subtype has all of the functionality of the supertype plus its own functionality, all the while being a subset of the values.
A subclass is a subtype
A subtype is NOT always a subclass.
