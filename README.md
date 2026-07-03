# 4kb_ROM_UG
## Experiment: Write the Verilog HDL Code for 4 KB ROM Memory for Read and Write Operation and Verify with Testbench

## Aim

To design and simulate a 4 KB ROM memory using Verilog HDL and verify its read operation through a testbench using Xilinx Vivado.

> **Note:** A ROM (Read-Only Memory) supports only **read operations** during normal operation. The memory contents are initialized before simulation. Therefore, the verification focuses on reading the stored data rather than writing during runtime.

## Apparatus Required

* Computer System
* Xilinx Vivado Design Suite
* Verilog HDL Simulator (Vivado Simulator)
* Windows/Linux Operating System

## Procedure

1. Open Xilinx Vivado and create a new RTL project.
2. Create a Verilog source file named **rom_4kb.v**.
3. Declare a 4 KB ROM using a memory array.
4. Initialize the ROM with sample data.
5. Create a testbench file named **rom_4kb_tb.v**.
6. Apply different addresses through the testbench.
7. Run Behavioral Simulation.
8. Observe the data outputs corresponding to each address.
9. Verify the correctness of the ROM contents.

## Verilog HDL Code

```verilog id="z8l9j2"
module rom_4kb(
    input  [11:0] address,
    output reg [7:0] data
);

reg [7:0] memory [0:4095];

integer i;

initial
begin
    for(i = 0; i < 4096; i = i + 1)
        memory[i] = i % 256;
end

always @(*)
begin
    data = memory[address];
end

endmodule
```

## Testbench Code

```verilog id="8um4ws"
`timescale 1ns/1ps

module rom_4kb_tb;

reg [11:0] address;
wire [7:0] data;

rom_4kb uut(
    .address(address),
    .data(data)
);

initial
begin
    address = 12'd0;
    #10;

    address = 12'd10;
    #10;

    address = 12'd100;
    #10;

    address = 12'd255;
    #10;

    address = 12'd1024;
    #10;

    address = 12'd4095;
    #10;

    $finish;
end

endmodule
```

## Expected Output

## Result

The 4 KB ROM memory was successfully designed and simulated using Verilog HDL. The output data matched the initialized memory contents for the applied addresses.

## Conclusion

Thus, the Verilog HDL implementation of a 4 KB ROM memory was successfully verified using a testbench in Xilinx Vivado. The simulation confirmed the correct retrieval of stored data for the given memory addresses.
