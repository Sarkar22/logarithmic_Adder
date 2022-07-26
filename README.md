# Logarithic_Adder
Logarithmic adders use a tree structure to reduce the time taken for addition to a logarithmic function of the number of bits being added. Brent Kung adder is a simple example of this approach.


A 32 bit Brent Kung adder in VHDL and simulated it using a test bench.


The adder needs logic functions AND, XOR, A + B.C to compute different orders of G, P and final sum and carry outputs. VHDL code has been written data flow style (using logic equations in assignments).

Using the above entities as components, structural descriptions of each level of the tree for generating various orders of G and P values has been written.
The right most blocks of all levels use the available value of C0 to compute the output carry directly and term these as the G values for for computation of P
and G for the next level.
Using the outputs of the tree above, a structural VHDL code for generating the bit wise sum and carry values has been written.

Tested the final adder with a test bench which reads pairs of 32 bit words and a single bit input carry from a file, adds them and compares the result with the expected 32 bit sum and 1 bit carry values stored in the same file.
It uses assert statements to flag errors if there is a mismatch between the computed sum/carry and the stored sum/carry.
Tested the design with 64 randomly chosen pairs of numbers and input carry to be added.

A glimpse of the testbench:
![test_bench](https://github.com/Sarkar22/Logarithic_Adder/blob/main/test_bench.PNG)

It is formatted as such:
a[16-bit] b[16-bit] cin[single bit] sum[16-bit] cout[single bit]

As we are adding 32bit numbers here, there will be 6 stages.
A & B has been taken as 32-bit numbers, and Cin (C0) has been taken as a single bit.
For the first stage we calculated as following:
G[i] = A[i] and B[i], P[i] = A[i] xor B[i] , and Cout[i+1] = A[i] or (B[i] and Cin[i])
For rest of the stages (n denoted as stage number)
Gn[i,i-1] = Gn-1[i] or (Gn-1[i-1] and Pn-1[i]), Pn[i,i-1] = Pn[i] and Pn-1[i-1]
