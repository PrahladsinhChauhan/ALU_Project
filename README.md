# ALU_Project

Design of basic ALU from transistor-level circuit using Cadence Virtuoso.
A zip file (Project.zip) of the project library utilized by the software is provided, containing all the original designs and rule checks performed on them.
Images of the design are provided in a seperate folder with a markdown documentation to act as a guide for refering various aspects of the design.


## Design Decisions

1. Arithmetic Logic Unit - ALU :

  The ALU is a crucial component of digital systems, handling arithmetic and logical operations. 
  This design of ALU, involves NOT, NAND and NOR logical operations as these are fundamental operations required to create any logical expression. 
  For arithmetic operations, only adder is used for minimalist approach to ensure less area consumption while considering subtraction functionality using 2’s complement.

2. Adder :

  Adder influences the performance of the circuit and overall efficiency. 
  Static Energy Recovery (SERF) Full adder has a reduced transistor count of 10T compared to conventional 26T full adders. 
  The incorporation of the inverters at the outputs is essential in reducing the noise observed for critical input "110" to the adder. 
  Therefore the adder used in this project has a transistor count of 18T.

3. Multiplexer :

  Multiplexer is pivotal circuit for signal selection and routing.
  In this design, Inverting and Restoring Multiplexers are used. 
  Three 2x1 MUX are used in a two-stage configuration to create 4x1 MUX. 
  So, two 2x1 MUX are connected in series, which eliminates the inverting effect and doesn’t require additional inverters. 
  Use of inverting and restoring MUX provides restored signal which ultimately reduce the noise margins.

4. Inverters :

  Inverters are a universal components for shaping of any digital circuits and can influence area efficiency and critical path delay. 
  This project adopts both scaled & unscaled inverters.
  For the ALU, as the critical delay would arise from the adder, unscaled inverter is used.
  For providing selection signals to MUX, scaled inverter with scaling factor 2 are used as its delay will affect the final output.



## Area Estimation

Using the following calculation, the area of ALU would be 429.72 square micrometers.

| Module | Length (micrometer) | Width (micrometer) | Area (sq. micrometer) |
| ------ | ------------------- | ------------------ | --------------------- |
| Adder            | 8.00 | 6.25 | 50.0000 |
| Inverter_X1      | 1.28 | 2.51 |  3.2128 |
| Inverter_X2      | 1.06 | 2.85 |  3.0210 |
| Multiplexer_2to1 | 2.73 | 4.64 | 12.6672 |
| NAND2            | 1.72 | 2.94 |  5.0568 |
| NOR2             | 1.64 | 3.12 |  5.1168 |

| Module | Submodule Count | Area (sq. micrometer) |
| ------ | --------------- | --------------------- |
| Adder_4bit       | 4   | 200.0000 |
| Inverter_4bit    | 4   |  12.8512 |
| Multiplexer_4to1 | 3+2 |  44.0436 |
| Multiplexer_4bit | 4   | 176.1744 |
| NAND2_4bit       | 4   |  20.2272 |
| NOR2_4bit        | 4   |  20.4672 |
| ALU              | 5   | 429.7200 |



## Critical Path Delay

In this design of ALU, the component with largest delay is the Adder.
For SERF adder, critical delay is observed when inputs A,B,Cin are 110.
This configuration can atmost occur twice for a 4bit adder.
File "ALU_Crit.pdf" shows the waveforms observed from a testbench where the following inputs were given:
A = 0101, B = 0101, S1S0 = 00

One can observe that the Critical Path Delay of this ALU design is 174.594 picoseconds (0.1746 nanoseconds).
