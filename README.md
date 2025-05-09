
# MIPS ISA – Instruction Set Architecture

## Overview

MIPS (Microprocessor without Interlocked Pipeline Stages) is a RISC (Reduced Instruction Set Computing) architecture that was developed by MIPS Computer Systems. It is widely used in embedded systems, networking devices, and educational platforms due to its simplicity and ease of understanding. This repository provides a detailed exploration of the MIPS Instruction Set Architecture (ISA), covering various aspects of its operations, instructions, and the underlying design principles.

## Table of Contents

- [Introduction](#introduction)
- [MIPS Architecture](#mips-architecture)
  - [Registers](#registers)
  - [Memory Model](#memory-model)
  - [Instruction Formats](#instruction-formats)
  - [Pipeline Stages](#pipeline-stages)
- [MIPS Instructions](#mips-instructions)
  - [R-Type Instructions](#r-type-instructions)
  - [I-Type Instructions](#i-type-instructions)
  - [J-Type Instructions](#j-type-instructions)
- [MIPS Addressing Modes](#mips-addressing-modes)
- [MIPS Assembly Syntax](#mips-assembly-syntax)
- [Example MIPS Code](#example-mips-code)
- [MIPS Processor Design](#mips-processor-design)
  - [Control Unit](#control-unit)
  - [ALU](#alu)
  - [Instruction Fetch Unit](#instruction-fetch-unit)
  - [Memory and Data Path](#memory-and-data-path)
- [Conclusion](#conclusion)

---

## Introduction

MIPS is a 32-bit RISC architecture known for its clean and simple design. It uses a fixed instruction length (32 bits) and supports a small set of instructions that are easy to decode and execute in a pipeline structure. The ISA is designed to be efficient for both academic purposes and real-world applications, making it an excellent choice for learning and implementation in processor design projects.

This repository provides detailed information about the MIPS ISA, including the instruction set, addressing modes, and how these concepts are implemented in hardware.

---

## MIPS Architecture

### Registers

MIPS provides 32 general-purpose registers, each 32 bits wide. The registers are typically divided into categories based on their usage:

- **$zero**: Constant value 0.
- **$at**: Assembler temporary register.
- **$v0-$v1**: Function return values.
- **$a0-$a3**: Function arguments.
- **$t0-$t9**: Temporary registers.
- **$s0-$s7**: Saved registers.
- **$sp**: Stack pointer.
- **$fp**: Frame pointer.
- **$ra**: Return address.

The registers are mapped to specific instructions and can be accessed directly by the MIPS CPU.

### Memory Model

MIPS uses a load/store architecture, meaning that all data processing must be done on registers. Memory accesses are performed via special load and store instructions. MIPS memory is byte-addressed, and data is typically aligned on word (4-byte) boundaries.

### Instruction Formats

MIPS instructions are 32-bits wide and come in three basic formats:

1. **R-Type (Register)**: Instructions that perform operations between registers.
2. **I-Type (Immediate)**: Instructions that use an immediate value as an operand.
3. **J-Type (Jump)**: Instructions for jump operations, allowing program control to transfer to a specified address.

### Pipeline Stages

MIPS uses a 5-stage pipeline architecture:

1. **IF (Instruction Fetch)**: Fetches the instruction from memory.
2. **ID (Instruction Decode)**: Decodes the instruction and fetches operands.
3. **EX (Execution)**: Executes the arithmetic or logical operation.
4. **MEM (Memory Access)**: Accesses memory (for load/store instructions).
5. **WB (Write Back)**: Writes the result to the register file.

---

## MIPS Instructions

### R-Type Instructions

R-Type instructions perform operations on the contents of registers. These instructions use the following format:

```
opcode (6 bits) | rs (5 bits) | rt (5 bits) | rd (5 bits) | shamt (5 bits) | funct (6 bits)
```

Example R-Type instructions:
- **add**: Adds two registers.
- **sub**: Subtracts two registers.
- **and**: Bitwise AND operation.
- **or**: Bitwise OR operation.
- **slt**: Set less than (used for comparisons).

### I-Type Instructions

I-Type instructions are used for operations involving constants or memory addresses. These instructions use the following format:

```
opcode (6 bits) | rs (5 bits) | rt (5 bits) | immediate (16 bits)
```

Example I-Type instructions:
- **addi**: Adds an immediate value to a register.
- **lw**: Loads a word from memory.
- **sw**: Stores a word to memory.
- **beq**: Branch if equal (conditional branch).

### J-Type Instructions

J-Type instructions are used for jump operations. These instructions use the following format:

```
opcode (6 bits) | address (26 bits)
```

Example J-Type instructions:
- **j**: Jump to a specified address.
- **jal**: Jump and link (used for function calls).

---

## MIPS Addressing Modes

MIPS supports the following addressing modes:

- **Immediate Addressing**: Used in I-Type instructions where a constant value is directly provided.
- **Register Addressing**: The operands are registers, and the result is stored back in a register.
- **Base/Offset Addressing**: Used in load/store operations, where the effective address is calculated by adding a base register and an offset.

---

## MIPS Assembly Syntax

MIPS assembly instructions are written using the following syntax:

```asm
<operation> <destination>, <source1>, <source2>
```

For example:
```asm
add $t0, $t1, $t2   # Adds $t1 and $t2, stores result in $t0
```

Common MIPS directives:
- **.data**: Used to define data sections.
- **.text**: Used to define the code section.
- **.word**: Used to allocate space for a word.

---

## Example MIPS Code

```asm
# Simple program to add two numbers
.data
num1: .word 5
num2: .word 10
result: .word 0

.text
main:
    lw $t0, num1        # Load num1 into $t0
    lw $t1, num2        # Load num2 into $t1
    add $t2, $t0, $t1   # Add $t0 and $t1, store result in $t2
    sw $t2, result      # Store the result into memory at 'result'
    li $v0, 10          # Exit program
    syscall
```

---

## MIPS Processor Design

### Control Unit

The Control Unit generates control signals based on the opcode and function code of the instruction. It coordinates the operation of the other components in the CPU.

### ALU (Arithmetic Logic Unit)

The ALU performs all arithmetic and logical operations in MIPS. It takes two inputs (register values or immediate values), performs the specified operation, and outputs the result.

### Instruction Fetch Unit

This unit fetches the instruction from memory, decodes it, and provides it to the Control Unit for execution.

### Memory and Data Path

MIPS uses a memory hierarchy with an instruction cache and data cache. Data is accessed via load and store instructions.

---

## Conclusion

MIPS is a powerful and simple ISA that is widely used in both academic and industrial contexts. Its simple and efficient design makes it ideal for teaching computer architecture concepts and for implementation in various processor designs. This repository provides a comprehensive overview of the MIPS ISA, its instruction set, addressing modes, and implementation details.

Feel free to explore, contribute, and learn more about MIPS by checking out the various examples, designs, and implementation details provided here.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
