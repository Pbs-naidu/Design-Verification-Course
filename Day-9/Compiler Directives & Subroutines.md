# Compiler Directives (08/04/2026)
1.`include 

2.`timescale 

3.`define 

```bash
`timescale 1ns/1ns
`include "fulladder_dut.v"
`define word_len = 64'h7891;
// define is also like parameter but its more like Customized value length given to the variable
module repeat_loop_Eg #(parameter data_width = 32);
    input [data_width-1:0] a,b,
    output [data_width-1:0] y
);

assign y = a + b;
assing y = word_len;

endmodule
```
# Subroutines
!.Function 
2.Task

## Function
```bash
function integer [1:0] carry();//return data type is integer
    input a,b; //arguments
    sum = a ^ b;
    c = a . b;
    carry = {sum, c} //function only returns single variable value
endfunction
```
## Task
```bash
task automatic integer barry();
    input a,b;
    output s,c;
    inout y;
    sum = a ^ b; #5; 
    c = a . b; #7;
    i = 1;
    i = 0; i = 1; 2; 3; 0000 //automatic does remember the values because of seperate memory allocation each time
endtask
```
