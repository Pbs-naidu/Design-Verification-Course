# Function
## Model 1
## Design Code:
```bash
module rca_4_bit_function(
    input [3:0] a, b,
    input cin,
    output [4:0] result
);
    function [4:0] add_rca;
        input [3:0] i1, i2;
        input c;
        begin
            add_rca = i1 + i2 + c;
        end
    endfunction
    assign result = add_rca(a, b, cin);
endmodule
```
## Test Bench:
```bash
module rca_tb;
    reg [3:0] a, b;
    reg cin;
    wire [4:0] result;
    rca_4_bit_function dut (.*);
    initial
    begin
        a = 4'b1011; b = 4'b1010; cin = 1; #10;
        a = 4'b0111; b = 4'b1110; cin = 1; #10;
    end
endmodule
```
## Run:
```bash
vlib work 
vlog rca.v
vlog rca_tb.v +acc
vsim work.rca_tb +acc
add wave -r * 
run -all
```
## Waveform:
<img width="1901" height="207" alt="function waveform" src="https://github.com/user-attachments/assets/6966d5a2-cff9-47e7-a1c0-d68236fc8347" />

## Model 2
## Design Code:
```bash
module rca_4_bit_function(
    input [3:0] a, b,
    input cin,
    output [4:0] result
);
    function [4:0] add_rca;
        input [3:0] i1, i2;
        input c;
		reg s,c;
        begin
    s = a ^ b ^ c;
    c = (a & b) | (b & cin) | (a & cin);
      add_rca = {s, c};
        end
    endfunction
    assign result = add_rca(a, b, cin);
endmodule
```
## Test Bench:
```bash
module rca_tb;
    reg [3:0] a, b;
    reg cin;
    wire [4:0] result;
    rca_4_bit_function dut (.*);
    initial
    begin
        a = 4'b1011; b = 4'b1010; cin = 1; #10;
        a = 4'b0111; b = 4'b1110; cin = 1; #10;
    end
endmodule
```
## Run:
```bash
vlib work 
vlog rca.v
vlog rca_tb.v +acc
vsim work.rca_tb +acc
add wave -r * 
run -all
```
## Waveform:
<img width="1912" height="273" alt="function waveform 1" src="https://github.com/user-attachments/assets/996050da-b367-44e6-9a68-0d82ca688d1d" />

<br>
