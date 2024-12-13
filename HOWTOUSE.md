# Test Instructions
For Pipeline Cpu With Harzard in the main branch


For Pipeline Cpu Without Hazard in Pipeline_CPU-V2.0
https://github.com/GiannisChristodoulou1/RISCV-CPU-14/tree/Pipeline-CPU-V2.0

For nonpipeline CPU in Non-Pipeline-CPU-V3.0
https://github.com/GiannisChristodoulou1/RISCV-CPU-14/tree/Non-Pipeline-CPU-V3.0
## Running 5 Tests

1. **Navigate to the test directory**
   ```bash
   cd repo/tb
   ```

2. **Run the tests**
   ```bash
   ./doit.sh
   ```
   This will execute 5 tests automatically, and the tests should run as expected.

---

## Running F1 Test and PDF Plot

1. **Navigate to the outermost folder** where `cpu_testbench` and `f1_testbench` are located.

2. **Run the PDF plot**
   ```bash
   ./doit.sh
   ```
   Note that the **`program.hex`** file will be used as the instruction memory file.

3. **Run the F1 test**
   ```bash
   ./f1.sh
   ```
   For the F1 test, you need to ensure the instruction memory file is updated to **`program_f1.hex`**.

---

## Important Notes

- Ensure you update the file name in the `instrmem` directory accordingly:
  - **PDF Plot** uses: `program.hex`
  - **F1 Test** uses: `program_f1.hex`



