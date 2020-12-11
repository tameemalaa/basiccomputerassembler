# Basic Computer Assembler

## What is this?

This a simple assembler designed for the Basic Computer described in M.Mano's book "Computer System Architecture". The Basic Computer has a 16-bit instruction divided into 12-bit address, 3-bit opcode and 1-bit for direct(0)/indirect(1) addressing modes.

The Basic Computer's ISA supports 25 instructions as following:
* Memory-Reference Instructions (MRI) : (7)
* Register-Reference Instructions (RRI) (12)
* Input-Output Instructions (IOI) (6)

The following is the detailed ISA:

### Memory-Reference Instructions (MRI) : (7)
| Instruction | Binary Representation |
|-------------| -------|
|AND          |I000xxxxxxxxxxxx|
|ADD          |I001xxxxxxxxxxxx|
|LDA          |I010xxxxxxxxxxxx|
|STA          |I011xxxxxxxxxxxx|
|BUN          |I100xxxxxxxxxxxx|
|BSA          |I101xxxxxxxxxxxx|
|ISZ          |I110xxxxxxxxxxxx|

These instructions have one operand, which is an address in memory. Each instruction starts with the addressing mode bit (I). If I = 0, the addressing is direct, which means that the address (the 12-bit x's) holds the value of the operand. However, if I=1, the addressing is indirect which means the address holds the value of the address of the actual operand.

### Register-Reference Instructions (RRI) (12)
| Instruction | Binary Representation |
|-------------| -------|
|CLA          |0111100000000000|
|CLE          |0111010000000000|
|CMA          |0111001000000000|
|CME          |0111000100000000|
|CIR          |0111000010000000| 
|CIL          |0111000001000000|
|INC          |0111000000100000|
|SPA          |0111000000010000|
|SNA          |0111000000001000|
|SZA          |0111000000000100| 
|SZE          |0111000000000010|
|HLT          |0111000000000001|

These instructions don't have any operands and are translated directly into machine code.

### Input-Output Instructions (IOI) (6)
| Instruction | Binary Representation |
|-------------| -------|
|INP          |1111100000000000|
|OUT          |1111010000000000|
|SKI          |1111001000000000|
|SKO          |1111000100000000|
|ION          |1111000010000000|
|IOF          |1111000001000000|

Similar to RRI, these instructions don't have any operands and are translated directly into machine code.

### Pseudo Instructions

There are four more instructions that can appear in the assembly code which does not directly map into a binary representation: `ORG`, `END`, `HEX`, and `DEC`. These instructions tell the assembler that their location has a special meaning.

## Assembly Language Rules

The assembly code supported by this simple assembler must stick to some basic rules otherwise it will yield unpredictable results.

* Each line consists of four parts:
    1. *Label's column*: 3 characters followed by a comma. Any label that is not following this convention will yield an error.
    2. *Instruction's column*: as shown in the three tables above, this column can have any of the preceding instructions.
    3. *Operand's column*: the operand must correspond to label included in this assembly code. Reference to labels that do not exist in the same assembly file will cause an error.
    4. *Addressing mode flag*: add I if the instruction is indirect.
    5. *Comments' column*: starts with `/` followed by any text. This whole text will be discarded by the assembler and serves the purpose of documentation only.
* There is at least one space between every column.
* Addresses placed after `ORG` are in hexadecimal and are written directly without preceding it with any special characters i.e. `100` is actually (32)<sub>10.
* Similar to the last point, labels created using the `HEX` pseudo instruction should also be without any special characters and should directly write the hexadecimal digits i.e. `AC41`.
* The output binary file is a `.txt` file where the first column represents the address of the instruction and the second column represents the binary value of the corresponding instruction.


## Changing ISA

The current ISA is divided into three different files `mri.txt`, `rri.txt`, and `ioi.txt`. You can add, modify or remove any instruction by changing the corresponding files.

## How to use?

Basically, one class `Assembler` is responsible for almost all operations regarding the assembly process. You first creat an object of the `Assembler` class and pass the MRI, RRI and IOI file paths to the constructor. This way, the object automatically loads the ISA from the files and saves them into internal data structures. Next, you call the method `assemble(assembly_file_path)` and passes the path to your assembly file path. The assembly file must end with `.S` or `.asm` file extension otherwise, the code will yield an error. As a starter, an assembly code is provided in `code.asm` file and the output assembly binaries are stores in `out.txt`.

The method `assemble()` returns a dictionary, where the keys represent locations (or memory addresses) and values represent the binary representations of the instructions at the corresponding key's value (location or address).


## How to report a bug?

This code is a very early implementation of the assembler. In case you faced any bugs or problems, please start an issue indicating the problem in details.

## Notes

The code in this repo is an exercise to design a simple assembler for the Basic Computer as per M.Mano's book (“Computer System Architecture,” Pearson Publisher, 3rd Edition, 1992). It is a part of "CSE311 Computer Organization" course taught in Egypt-Japan University of Science and Technology, Egypt - by Prof. Mostafa Soliman. The code here is written by Eng. Osama Adel in December 2020 as part of his role as a Teaching Assistant of this course.