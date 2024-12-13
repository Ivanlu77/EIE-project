### Ivan Personal Statement
- **Developed, tested, and debugged top modules** for Non-Pipeline and Pipeline CPUs.
- **Assisted in debugging single-cycle and pipeline designs**
- **Supported the development of the hazard unit**
- **Created testbenches for multiple testing scenarios**, including plot PDF results on VBuddy.
- **Developed an F1 test program** run on Vbuddy to simulate the f1 light

### Non-Pipeline CPU
As a key contributor, I was responsible for **integrating all modules and creating the top module** to ensure proper execution. This involved identifying and resolving unexpected errors in the submodules to guarantee the CPU’s overall functionality. Key challenges and solutions included:

- **Issue 1: Register File Clock Edge**
  - **Problem**: The register file did not use `negedge`, causing misalignment of signals.
  - **Solution**: Corrected the clock edge trigger in the register file to `negedge`, ensuring proper synchronization.
    

   [GitHub commits]( https://github.com/GiannisChristodoulou1/RISCV-CPU-14/commit/15d22f31502b1235e8ad730080da6ba39b3765b4)
 

- **Issue 2: Missing ALU Instructions**
  - **Problem**: The ALU lacked essential instructions.
  - **Solution**: Added the missing instructions to the ALU module and ensured compatibility with the control unit.

- **Issue 3: JALR Instruction Handling**
  - **Problem**: The main decoder failed to detect `JALR` instructions.
  - **Solution**: Introduced the **JumpLinkReg** signal to the main decoder, which activates upon detecting `JALR`. The logic was implemented as follows:
     [GitHub commits](https://github.com/GiannisChristodoulou1/RISCV-CPU-14/commit/125aae6fd0ad07a18d2274e5459f6ef5fc08961b)
```verilog
JALR: begin    // JALR
    RegWrite    =   1'b1;
    ImmSrc      =   3'b000;
    ALUSrc      =   1'b1; 
    MemWrite    =   1'b0;
    ResultSrc   =   2'b10;   
    Branch      =   1'b0;
    ALUOp       =   2'b10;
    Jump        =   1'b1;
    JumpLinkReg =   1'b1;
end

JAL: begin    // JAL
    RegWrite    =   1'b1;
    ImmSrc      =   3'b011;
    ALUSrc      =   1'b0; 
    MemWrite    =   1'b0;
    ResultSrc   =   2'b10;   
    Branch      =   1'b0;
    ALUOp       =   2'b00;
    Jump        =   1'b1;
    JumpLinkReg =   1'b0;
end
```
With these updates, the handling of `JALR` instructions was successfully implemented.

**Testbench for PDF Plot**: I created a testbench that plotted PDF results. To optimize runtime, the display was restricted to only activate when `a0` had a non-zero value, ensuring a clear and efficient visual display.
**Testbench for F1**I create a testbench also for running the f1 program. 
**F1 Program**: Designed and executed an **F1 program** to verify CPU performance. The VBuddy lights activate in a sequence when a0 is(1, 3, 7, 15, ...), mimicking a "left shift and add 1" pattern. Since shift instructions were not available, I used **ADD instructions to simulate the shift**. The testbench was updated to allow VBuddy to read the value of `a0` and control the light bar accordingly.
[Github commits](https://github.com/GiannisChristodoulou1/RISCV-CPU-14/commit/9711e457a883d5c4d874dba04b12579bd7ac6b1d)
**doit.sh and F1.sh** these two files are used to run the programs.


### Pipeline CPU
For the pipeline CPU, I collaborated with team members to **build the top module and connect all submodules**. 

- **Initial Challenges**: Initial test runs failed due to the complexity of the top module. The non-pipeline version had too many signal checks and logic embedded directly in the top module.
- **Solution**: Worked with Michael to **modularize the non-pipeline design**, ensuring submodules were self-contained. This simplification improved debuggability and test coverage.
- **Testing and Debugging**: The first three test cases passed successfully. However, the `JALR` test failed due to a missing signal. Working with Giannis, we realized the **JumpLinkReg** signal was not being passed to the DE register. After correcting this, the final test passed.
[Github commits](https://github.com/GiannisChristodoulou1/RISCV-CPU-14/commit/5f80b904d02fced8e16d96fadbd1f95f1655fc81)
### Hazard Unit

**forward mux** I wrote the two mux to placed in the pipeline to select the correct data source for operands, thereby bypassing certain pipeline stages and eliminating stalls. 
To create the **Hazard Unit**, we design it based on this graph.
[Github commits](https://github.com/GiannisChristodoulou1/RISCV-CPU-14/commit/e4021b9e3f0082e77ae897f22e199a5d91031784)
- **Issue**: The `ALUOp1` signal was delayed by one clock cycle.
- **Solution**: Discovered that the register file was not using `negedge`, causing synchronization issues. After modifying the design to use **negedge**, the hazard unit operated as intended.

Through consistent debugging, collaboration, and rigorous testing, I successfully contributed to the development of a functional, efficient CPU pipeline with hazard resolution.


### Mistakes
At the very beginning, we designed the nonpipelined CPU. When I was testing it, I directly put all the changes into the top module. For example, [top.sv](https://github.com/GiannisChristodoulou1/RISCV-CPU-14/blob/Non-Pipeline-CPU-V1.1/repo/rtl/top.sv), where you can see a lot of `assign` statements in the top module. This made the code hard to read and also caused some mistakes. After discovering this, I quickly adjusted it, ensuring that each operation was moved back into its respective module. (https://github.com/GiannisChristodoulou1/RISCV-CPU-14/blob/Non-Pipeline-CPU-V3.0/repo/rtl/top.sv ) The thing i learned is when doing verification, I need to understand each module is doing insted of just modify things what are missing.






### Learnings and Skills Acquired

- **Collaborative Development with GitHub:**

  Mastered using GitHub for version control, enabling effective collaboration with team members, managing code repositories, and handling branches and merges seamlessly.

- **SystemVerilog:**

  Enhanced skills in writing and debugging SystemVerilog modules

- **Module Testing and Validation:**

  Gained expertise in creating and running testbenches to validate module designs, utilizing GTKWaves to ensure functionality and performance.

- **Understanding RISC-V32I CPU Architecture:**

  Deepened understanding of the RISC-V32I CPU’s working principles, including instruction decoding, execution, hazard detection, and pipeline management.

### Future Improvements and Goals


- **Adherence to Coding Standards:**

  Commit to using uniform coding rules across all modules to improve code readability, maintainability, easier to debug


- **Comprehensive Testing:**

  Intend to expand testbench scenarios to cover a wider range of instructions and edge cases, ensuring robust CPU performance under various conditions.
