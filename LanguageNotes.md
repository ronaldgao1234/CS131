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
-: int list = [1; 3; 5]

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
# Java
----------
- statically typed
- strongly typed
- name equivalence
- To achieve its goal of "Write once, run anywhere," Java does both: a Java compiler converts Java code into machine-readable bytecode, then the Java Virtual Machine interprets the code for the computer it runs on.
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
# Prolog
----------

# Scheme
----------

# Python
----------
- Dynamically typed
- strongly typed 
