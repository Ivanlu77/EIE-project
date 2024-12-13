### Summary
- **Developed, tested, and debugged top modules** for Non-Pipeline and Pipeline CPUs.
- **Assisted in debugging single-cycle and pipeline designs**, with a focus on design logic and component interaction.
- **Supported the development of the hazard unit**, ensuring seamless instruction flow within the pipeline.
- **Created testbenches for multiple testing scenarios**, including running PDF results on VBuddy.
- **Developed an F1 test program** to validate proper CPU execution.
- **Engineered a testbench to control VBuddy lights**, tracking system output through visual feedback.

### Non-Pipeline CPU
As a key contributor, I was responsible for **integrating all modules and creating the top module** to ensure proper execution. This involved identifying and resolving unexpected errors in the submodules to guarantee the CPU’s overall functionality. Key challenges and solutions included:

- **Issue 1: Register File Clock Edge**
  - **Problem**: The register file did not use `negedge`, causing misalignment of signals.
  - **Solution**: Corrected the clock edge trigger in the register file to `negedge`, ensuring proper synchronization.

- **Issue 2: Missing ALU Instructions**
  - **Problem**: The ALU lacked essential instructions.
  - **Solution**: Added the missing instructions to the ALU module and ensured compatibility with the control unit.

- **Issue 3: JALR Instruction Handling**
  - **Problem**: The main decoder failed to detect `JALR` instructions.
  - **Solution**: Introduced the **JumpLinkReg** signal to the main decoder, which activates upon detecting `JALR`. The logic was implemented as follows:

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

**F1 Program**: Designed and executed an **F1 program** to verify CPU performance. The VBuddy lights activate in a sequence (1, 3, 7, 15, ...), mimicking a "left shift and add 1" pattern. Since shift instructions were not available, I used **ADD instructions to simulate the shift**. The testbench was updated to allow VBuddy to read the value of `a0` and control the light bar accordingly.

### Pipeline CPU
For the pipeline CPU, I collaborated with team members to **build the top module and connect all submodules**. 

- **Initial Challenges**: Initial test runs failed due to the complexity of the top module. The non-pipeline version had too many signal checks and logic embedded directly in the top module.
- **Solution**: Worked with Michael to **modularize the non-pipeline design**, ensuring submodules were self-contained. This simplification improved debuggability and test coverage.
- **Testing and Debugging**: The first three test cases passed successfully. However, the `JALR` test failed due to a missing signal. Working with Giannis, we realized the **JumpLinkReg** signal was not being passed to the DE register. After correcting this, the final test passed.

### Hazard Unit
To create the **Hazard Unit**, we used a diagram-based approach to detect and resolve hazards during pipeline execution.

- **Issue**: The `ALUOp1` signal was delayed by one clock cycle.
- **Solution**: Discovered that the register file was not using `negedge`, causing synchronization issues. After modifying the design to use **negedge**, the hazard unit operated as intended.

Through consistent debugging, collaboration, and rigorous testing, I successfully contributed to the development of a functional, efficient CPU pipeline with hazard resolution.

### Learnings and Skills Acquired

- **Collaborative Development with GitHub:**

  Mastered using GitHub for version control, enabling effective collaboration with team members, managing code repositories, and handling branches and merges seamlessly.

- **SystemVerilog Proficiency:**

  Enhanced skills in writing and debugging SystemVerilog modules, including designing complex hardware components and ensuring their correct interaction within a CPU architecture.

- **Module Testing and Validation:**

  Gained expertise in creating and running testbenches to validate module designs, utilizing simulation tools to ensure functionality and performance.

- **Understanding RISC-V32I CPU Architecture:**

  Deepened understanding of the RISC-V32I CPU’s working principles, including instruction decoding, execution, hazard detection, and pipeline management.

### Future Improvements and Goals

- **Enhanced Team Communication:**

  Plan to maintain consistent communication with team members at each stage of development to streamline debugging processes and foster collaborative problem-solving.

- **Adherence to Coding Standards:**

  Commit to using uniform coding rules across all modules to improve code readability, maintainability, and reduce the likelihood of integration issues.

- **Pipeline Optimization:**

  Aim to further optimize the pipeline CPU design by implementing advanced hazard detection techniques and exploring out-of-order execution for improved performance.

- **Comprehensive Testing:**

  Intend to expand testbench scenarios to cover a wider range of instructions and edge cases, ensuring robust CPU performance under various conditions.
