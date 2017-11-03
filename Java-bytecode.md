# Java bytecode
* code for Java Virtual Machine (JVM)* calculations use **operand stacks*** subroutine calls tailored to Java methods
## Levels of programming#### High levellanguages designed to be easy for humans  
 - e.g. Java, C, Prolog, Haskell, ...  
 #### Lowest levelmachine code  = instructions stored in memory  ... opcodes + operand bytes  
#### Next level upassembly code  = machine code in form that can be written and read by humans  
- mnemonics, `ld a [b]` etc.- `labels` for jump destinations
## Converting high level to low level /
#### Assembly code -> machine code  **(1) Assembler**  - translates **instruction mnemonics** like `ld a [b]`into machine code bytes  - works out addresses for jumps and calls  - BUT **relocatably** - doesn't fix location in memory 
**(2) Linker**  - combines different assembled parts into a single whole  **(3) Loader**  - loads into memory at a given location
#### Interpret / Compile
**(1) Interpret**
another program  - follows text of P .... source code   - does appropriate actions  Same principle:  - humans running through parts of P  - CPUs as hardware interpreters of machine code  
Interpreter usually does some initial analysis of text - e. g. identify keywords if, while etc..... lexical analysis  
Interpreting is slow.

**(2) Compile**  

converts **source code** (text of P) into **object code** - machine code that does the same as P  
Usually object code is **relocatable**, so can later be linked and loaded  
Compiling is harder than interpreting  - but done once only for each P  - with clever tricks to optimize object code  Then object code executes fast.
## Compiling combined with interpreting 
* more efficiently;  
* a single compiler, independent of CPU;  
* Separate task for each CPU.  
e.g.
* Executing high level programs - source code - a.java files; 
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
Each time you call a method in java,it gets a new `frame` constructed for it.

* storage space for local variables - same principle as registers* space for an operand stack* program counter and stack pointer - for virtual machine, not CPU* reference back to frame of caller 
* other stuff
Frame | 
---- | 
Space for operand stack |
local variables |
pc, sp |
other stuff |
caller's frame | 

#### "Entries" on operand stack or local variablesEnough for  - boolean .... 1 bit  - byte .... 1 byte  - short, char .... 2 bytes   
- int, float .... 4 bytes  Enough for any reference value .... 4 bytes  For long, double need two consecutive entries .... 8 bytes  
#### local variable
**(1) "this" (for a non-static method)**  - reference to the object "this"  
- kept as local variable in slot 0
**(2) parameters of method**  - slot numbers start 0 (static) or 1 (non-static)  **(3) variables declared in method**   - slot numbers start after those for parameters  
Each local variable has a "slot" number, to show where it is stored in the frame.  
A double entry (types long or double) uses two slots. e.g. a long variable with slot number 5 also uses slot 6.
#### Instance variables 
Instance variables a (non-static fields)  
- a value stored in every instance of the class  
- if x is reference to object then`x.a` is variable in that object  
- a on its own means `this.a`

####  Class variables
Class variables b (`static` fields)  - one value stored for the whole class  - use it as classname.b  - can use b on its own within its own class	public class PosVal {    	private static int nextSerial = 0;    	private int serial;    	private int val; //invariant: val >= 0
		public PosVal(int initVal) {    		int v = initVal;    		if (v < 0){				v = -v;			}			val = v;			serial = nextSerial;			nextSerial += 1;
In this case, what types of the variables?
* `class variable` - static int `nextSerial`;
* `instance variables` - private int  `serial` & `val`;
* `local variables` - @param `initVal` & int `v`(slot numbers)
#### Local variables in JVM
JVM doesn't know the names of the local variables (from Java source).   
 Refers to them by **slot numbers** starting at 0.
**For non-static method**  
- variable 0 is `this`,- then parameters start at slot 1,  
- then other local variables.  
**For static method**  
- parameters start at slot 0.
**long or double variables** each need **two slots**, use slot number of first one.

## Bytecode Instructions
