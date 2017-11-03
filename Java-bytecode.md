# Java bytecode
* code for Java Virtual Machine (JVM)

 - e.g. Java, C, Prolog, Haskell, ...  
 

- mnemonics, `ld a [b]` etc.











converts **source code** (text of P) into **object code** - machine code that does the same as P  




* a single compiler, independent of CPU;  
* Separate task for each CPU.  


* compile to intermediate level - Java bytecode - .class files(by javac);  
* interpret intemediate language - JVM

## Java Virtual Machine (JVM)
### How JVM works

* Frame = space for calculation; operand stack; storage space for local variables...
* Bytecode instructions
* Method calls create frames
* Heap for objects
* symbolic references to methods

 
### Frame
Each time you call a method in java,

* storage space for local variables - same principle as registers
* other stuff

---- | 
Space for operand stack |
local variables |
pc, sp |
other stuff |
caller's frame | 

#### "Entries" on operand stack or local variables
- int, float .... 4 bytes  


- kept as local variable in slot 0





- a value stored in every instance of the class  
- if x is reference to object then
- a on its own means `this.a`

####  Class variables
Class variables b (`static` fields)  







 

- variable 0 is `this`,
- then other local variables.  

- parameters start at slot 0.



