# Single-Cycle-RISC-V
Arjun Anand Mallya
![Screenshot 2025-02-21 162911](https://github.com/user-attachments/assets/1913f8b8-5150-4d37-8baf-a723f94d84d3)


This repository contains a single-cycle RISC-V processor implemented in Verilog. The design includes modules for the program counter, instruction memory, register file, ALU, control unit, and supporting multiplexers, adders, and logic. A testbench (`tb_top.v`) is provided to simulate the design in Vivado.

## Overview


This project implements a simplified RISC-V processor with the following key components:

- **Program Counter (PC):** Holds the address of the current instruction. Updates on the rising clock edge.
- **PCplus4 Module:** Computes the next sequential address by adding 4 to the current PC.
- **Instruction Memory:** Stores instructions. Instructions are fetched using word addressing (the address is shifted right by 2).
- **Register File:** A small storage array (32 registers) used to hold operands and results.  
  - **Rs1, Rs2: ** Register addresses for operands.
  - **read_data1, read_data2:** The data reads from registers Rs1 and Rs2.
  - **Rd:** Destination register address for writing.
  - **Write_data:** Data to write to the destination register.
- **Immediate Generator (ImmGen):** Extracts immediate values from instructions based on the opcode.
- **Control Unit:** Decodes the instruction opcode and sets control signals (ALUSrc, MemtoReg, RegWrite, MemWrite, Branch, ALUOp).
- **ALU (Arithmetic Logic Unit):** Performs arithmetic and logical operations.  
  - Its result is available on the signal `address_top`.
- **ALU Control:** Determines the specific ALU operation based on the control signals and function bits (fun7 and fun3) from the instruction.
- **Data Memory:** Used for load and store instructions.
- **Multiplexers (Mux1, Mux2, Mux3):** Select between different data paths (e.g., register data vs. immediate value, ALU result vs. memory output).
- **AND Logic & Adder:** Provide additional combinational operations required in the processor.

The top-level module (`top.v`) instantiates all these submodules and connects them together to form the complete processor. A testbench (`tb_top.v`) is included for simulation.

To test specific operations:
- **Instruction Memory:**  
  The `Instruction_Mem` module is preloaded with a set of instructions (e.g., add, sub, and, or, addi, ori, lw, sw, beq).  
- **Register File:**  
  The register file is initialized with specific values in an `initial` block. You can modify these values to test different scenarios.

## Expected Behavior

- **Program Counter:**  
  Updates on the rising edge of the clock. It shows a one-clock-cycle delay relative to its computed next value (normal in synchronous designs).
- **ALU Operation:**  
  The result of the ALU computation is available on `address_top`. For example, when an add instruction is executed, the sum should match the expected value from the corresponding registers.
- **Memory Operations:**  
  Loads and stores should read/write data correctly from/to the data memory.
## Simulation Waveform:

Below is the simulation waveform with the registers initiated with some random values.

![Screenshot 2025-02-21 161530](https://github.com/user-attachments/assets/74c7ec23-ae3a-4bf9-ae57-f358241684ba)

## Elaborated Design

Below is the Elaborated Design:

![Screenshot 2025-02-21 162754](https://github.com/user-attachments/assets/2fdaa191-ef4e-422b-8b5f-e8a26257e591)



## Future Aspects

- Modify the memory system to communicate with a on-chip network instead of the current shared memory module.
- Implementation of Pipeline
- Hazard Detection Circuit 
- Implementation of a dynamic routing algorithm to optimize data transfer.
- Implementation of the Processor on a FPGA

