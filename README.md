Paralace Programming Language

Paralace is a high-performance AOT programming language with a clean, English-like syntax and a direct NASM/MASM backend.

It combines high-level readable source, explicit memory and data structures, and straightforward lowering into native assembly, with parallelism and SIMD provided via libraries rather than compiler-driven speculation.

Paralace is designed for developers who want clear, structured code that compiles into predictable, efficient native binaries without a complex optimization brain in the compiler.

---

Core identity

Paralace is:

- Ahead-of-time compiled  
- Strongly typed  
- Statically typed  
- NASM/MASM-backed  
- Performance-aware  
- Struct-centered  
- Explicit with memory  
- Manual with errors  
- Library-driven for concurrency  
- Flexible with idioms  
- Native-metal in behavior  
- High-level in expression  

Its style is:

`paralace
entry

    print "Hello, World"

;
`

---

Compilation pipeline

Paralace Source  
↓  
Lexer  
↓  
Parser  
↓  
AST Builder  
↓  
Semantic Analyzer  
↓  
NASM/MASM Generator  
↓  
Assembler (NASM/MASM)  
↓  
Native Binary

There is no virtual interpreter and no internal optimization command layer.  
Optimization is achieved through:

- good code generation patterns  
- efficient NASM/MASM emission  
- external assemblers and linkers  
- performance-oriented libraries (SIMD, parallelism, batching)

---

Philosophy

Paralace now has a refined belief:

> Write clearly. Lower directly. Run natively.

The language allows abstraction at the source level, but the compiler focuses on:

- predictable lowering  
- clean assembly output  
- library-based performance (SIMD, threads, batching)  

The programmer controls performance through data layout, loops, and library choices, not speculative compiler magic.

---

Paradigm

Paralace is a definition-oriented systems language.

It supports:

- Systems programming  
- Procedural programming  
- Struct-oriented programming  
- Data-oriented programming  
- Batch-oriented programming  
- Definition-oriented programming  
- Library-based parallel programming  
- Performance-first application design  

Structs are the center of the language.  
Definitions describe behavior.  
Pockets store data.  
Libraries provide concurrency, SIMD, and batching.

---

Syntax rules

Paralace uses:

- ; end marker  
- # comments  
- -- preprocessor  
- @ includes/imports  

Spaces are intrinsic.  
Indents are inherent.  
Formatting is part of meaning.

Example:

`paralace

comment

@system.io
@math.vector

--if DEBUG
    print "debug mode"
--endif

entry

    print "Paralace running"

;
`

---

Types

Paralace is strong and static.

Basic types:

`paralace
number age = 38;
decimal speed = 4.5;
text name = "Konnie";
bool ready = true;
`

Booleans:

`paralace
true
false
`

Null is explicit:

`paralace
null<Player>
`

---

Structs

Structs are the main building block.

`paralace
struct Player

    text name
    number hp
    decimal speed

;
`

Methods attach directly:

`paralace
define Player.damage

    takes number amount

    hp -= amount

;
`

---

Functions

`paralace
define add

    takes number a
    takes number b

    return a + b

;
`

Calling:

`paralace
number result = add 10 25;
`

Automatic returns when allocation is obvious:

`paralace
define makePlayer

    Player p

    p.name = "Alex"
    p.hp = 100

;
`

The compiler recognizes the returned allocation and lowers it into appropriate assembly.

---

Conditionals

`paralace
if age >= 18

    print "adult"

else

    print "minor"

;
`

Nested conditionals can be written compactly by the programmer; the compiler lowers them directly into branches without speculative flattening.

---

Loops

`paralace
repeat 100

    print index

;

while running

    update

;

until finished

    render frame

;

during timer

    update physics

;
`

Loop performance is controlled by:

- programmer’s structure  
- library calls (e.g., SIMD loops, parallel loops)  
- assembler-level optimizations

---

Pockets

Pockets are Paralace’s storage abstraction.

`paralace
pocket inventory

inventory insert sword
inventory insert shield
inventory remove sword
`

A pocket can lower into:

- stack memory  
- heap memory  
- arena memory  
- static memory  
- register storage  
- vector storage  
- thread-local storage  
- packed batch storage  

The compiler uses simple, deterministic rules to choose storage forms; advanced batching and SIMD are provided by libraries.

---

Memory

Memory is user-defined:

`paralace
stack number counter
heap Player hero
arena EnemyGroup enemies
static Config settings
shared WorldState world
thread WorkerData local
`

Paralace does not hide memory behavior. It lets the user state intent while the compiler emits clear NASM/MASM for that layout.

---

Pointers

Paralace supports intuitive pointer forms:

`paralace
pointer<Player> hero
raw<Player> enemy
smart<Player> owner
null<Player> missing
`

Pointer action:

`paralace
hero points player
`

Pointer safety depends on the selected pointer type and user-defined rules; concurrency and aliasing are handled by libraries and programmer discipline.

---

Errors

Errors are manually defined.

`paralace
error FileMissing

handle FileMissing

    print "file missing"

;
`

Throwing:

`paralace
throw FileMissing;
`

Errors are not automatically optimized or transformed; they lower into straightforward control flow and calls.

---

Includes

Includes use @:

`paralace
@system.io
@system.memory
@math.simd
@graphics.vulkan
@concurrency.threads
@batch.processing
`

Libraries provide:

- threading  
- SIMD operations  
- batch processing  
- task scheduling  

---

Preprocessor

Preprocessor directives use --:

`paralace
--define FAST_MODE

--if FAST_MODE

    optimize aggressive

--endif
`

Preprocessor affects source inclusion and configuration, not speculative optimization.

---

Concurrency (library-based)

Parallelism is provided via libraries, not compiler deduction.

Example:

`paralace
@concurrency.threads

entry

    threads.spawn physics_update
    threads.spawn ai_think
    threads.join_all

    print "frame complete"

;
`

Batch parallelism:

`paralace
@batch.processing

batch.parallel enemies

    enemy.hp -= poison

;
`

The compiler lowers these calls into NASM/MASM; the libraries implement the concurrency model.

---

SIMD and vectorization (library-based)

SIMD is exposed via libraries:

`paralace
@math.simd

batch.simd numbers

    output = input * 2

;
`

The compiler emits calls or inline assembly as defined by the SIMD library; it does not perform automatic widening or speculative vectorization.

---

Idioms

High-level form:

`paralace
batch enemies

    move_toward player

;
`

Lower-level form:

`paralace
for enemy in enemies

    enemy.x += enemy.dx
    enemy.y += enemy.dy

;
`

Both lower into clear assembly; performance differences depend on library implementations and programmer choices.

---

Operators and flows

Operators:

`paralace
+
-
*
/
%
==
!=
<
>
<=
>=
and
or
not
&
|
^
<<
>>
`

Flows:

`paralace
if
else
repeat
while
until
during
batch
group
concurrent   # via libraries
do
return
`

---

Example program (revised)

`paralace
@system.io
@math.simd
@concurrency.threads
@batch.processing

struct Enemy

    number hp
    decimal x
    decimal y
    decimal dx
    decimal dy

;

pocket enemies

define updateEnemy

    takes Enemy enemy

    enemy.x += enemy.dx
    enemy.y += enemy.dy

;

entry

    batch.parallel enemies

        updateEnemy enemy

    threads.spawn damage_step
    threads.spawn collision_step
    threads.join_all

    print "frame complete"

;
`

This program relies on:

- batch.parallel for parallel batch processing  
- threads library for concurrency  
- math.simd for SIMD operations inside library implementations  

The compiler’s job is to lower this cleanly into NASM/MASM, leaving concurrency and SIMD behavior to the libraries.

---

Final definition

Paralace is a parallel-capable, AOT, NASM/MASM-backed systems language with English-metal syntax, static strength, manual memory, user-defined errors, pocket-based storage, and library-driven concurrency and SIMD, using a simple AST + semantic analyzer + direct assembly backend instead of a speculative virtual interpreter and internal optimization command layer.

It is built to feel readable at the surface, predictable in the compiler, and native at runtime, with performance controlled by data layout, loops, and libraries rather than an opaque optimization engine.
