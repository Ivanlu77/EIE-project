Test Instructions

Running 5 Tests

Navigate to the test directory

cd repo/tb

Run the tests

./doit.sh

This will execute 5 tests automatically, and the tests should run as expected.

Running F1 Test and PDF Plot

Navigate to the outermost folder where cpu_testbench and f1_testbench are located.

Run the PDF plot

./doit.sh

Note that the program.hex file will be used as the instruction memory file.

Run the F1 test

./f1.sh

For the F1 test, you need to ensure the instruction memory file is updated to program_f1.hex.

Important Notes

Ensure you update the file name in the instrmem directory accordingly:

PDF Plot uses: program.hex

F1 Test uses: program_f1.hex

Verify that you have the required permissions to execute the scripts (./doit.sh and ./f1.sh). If necessary, make the scripts executable:

chmod +x doit.sh f1.sh

By following these steps, you will be able to run the standard tests, the F1 test, and generate the PDF plot without any issues.
