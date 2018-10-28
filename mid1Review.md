# EECS370 MID1 Review Sheets

##Figure Convention

### Two's compliment

* Most significant bit negative, the rest are positive

$$
10000001_{2}=-1\cdot 2^{7}+1=-127
$$

* Tricky Approach

  Perform bit-wise negation and add 1, assuming unlimited sign extension of most significant bit

### Floating point arithmetic

![image-20181028162905886](/Users/zhuhaoxuan/Library/Mobile Documents/com~apple~CloudDocs/UM/EECS370/MIDREVIEW/Review Notes.assets/image-20181028162905886.png)

* 31: Positive(0) or Negative(1)

* 30-23: Exponent

  Add 127 to value of the exponent to encode

  | -127 | 00000000 |
  | :--: | :------: |
  | -126 | 00000001 |
  |  0   | 01111111 |
  |  1   | 10000000 |

* 22-0: Mantissa

**Watch Out**

1. Exponent needs to substract 127 (used biased base 127 encoding)
2. Mantissa shows the 23 most siginificant bits after the decimal point

### Arithmetic manipulation

1. Multiplication
   1. add two exponents (Remember the bias of 127)
   2. multiply significands (Remeber implicit 1 bit)
   3. Renormalize if necessay
   4. Compute sign bit (exclusive-or)
2. Addition
   1. Shift smaller exponent right to match larger
   2. Add significands
   3. Normalize and update exponent
   4. Check for out of range



## ARM Assembly Code

* 64-bit registers
* 32-bit instruction

### Data layout

* starting address must be multiple of the number of bytes of the data type
* For struct, besides starting address, the total bytes used must be a multiple of the largest number of bytes used by its elements **(Padding)**
* If a struct container certain structs, the largest number of used bytes is still determined by premitives

### Watch Out

* Pay attention to shift 

## Memory Map

**Stack**

* Parameters(that were not passed through registers)
* Local variables
* Temporary storage (Caller/Callee save)
* Return Address

**Heap**

* Allocation done explicitly with `malloc()`

**Static**

* All global variables
* Static local variables
* Strings(Ptr to the string is stored on stack)

**Text**

* instructions

### Big endian/ little endian

* Big endian: most significant figure stores first
* little endian: least significant figure stores first



## Callee/Caller Save

### Caller-saved

* **Live**: Assign value before function call, and use that value after the function call
* Leaf function do not need to save/store if utilized caller-save

### Callee-Saved

* Only needs saving at begining of function and restoring at end of function
* Only save/restore it if function overwrites the register



## Linker

### ELF (Executable and linkable format)

* **Header**: contains sizes of other parts
* **Text**: machine code
* **Data**: global and static data
* **Symbol table**: symbols and values (globals that are out of scope)
* **Relocation table**: references to addresses that may change
* **Debug info**: mapping of object back to source(only in debug mode)

**Symbol Table**: where is it

1. Location of function call, global variable, static variable

**Relocation Table**: where is it used



