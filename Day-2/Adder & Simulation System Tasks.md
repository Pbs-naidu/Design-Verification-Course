
# Full Adder ,Half Adder  (26/03/2026)
## Introducing $monitor,$strobe,$write,$display,$finish,$stop in the code
## HALF ADDER
### VERILOG CODE
### Data Flow Model
```bash
module half_adder(
input [1:0] a,
output sum,carry
);

//Data flow
//assign sum = a[0]^a[1];
//assign carry = a[0]&a[1];

endmodule
```
### Gate level Model
```bash
module half_adder(
input [1:0] a,
output sum,carry
);

//gate level
xor a1(sum,a[1],a[0]);
and a2(carry,a[1],a[0]);

endmodule

```
### TESTBENCH
```bash
module half_adder_tb();
reg [1:0] a;
wire sum,carry;

half_adder dut(.*);
initial begin
a=2'b00;
#5; a=2'b01;
#5; a=2'b10;
#5; a=2'd3;

end

endmodule

```
### RUN
```bash
vlib work 
vlog half_adder.v
vlog half_adder_tb.v +acc
vsim work.half_adder_tb +acc
add wave -r * 
run -all
```
### TRANSCRIPT
<img width="988" height="467" alt="script half adder" src="https://github.com/user-attachments/assets/92feb676-2ef3-4060-8009-f54d3b9459de" /><br>
### WAVEFORM
<img width="1918" height="405" alt="half adder waveform" src="https://github.com/user-attachments/assets/9a89fbde-7eeb-42e3-b006-83bb54b57c8c" /><br>

## FULL ADDER
### VERILOG CODE
```bash
module full_adder(
input [2:0] a1,
output s,c
);
wire s1,c1,c2;

half_adder ha1(.a({a1[2], a1[1]}), .sum(s1), .carry(c1)); //connecting by order
half_adder ha2({s1,a1[0]},s,c2); //connecting by name
or o1(c,c1,c2);

endmodule
```
### TESTBENCH
#### 1) $display
```bash

module full_adder_tb();
reg [2:0] a1;
wire sum,carry;

full_adder dut(.a1(a1), .s(sum), .c(carry));
initial begin
$display("time = %t,a1=%b,sum=%b,carry=%b",$time,a1,sum,carry);
a1=3'b000;
#5; 
a1=3'b001;
#5; a1=3'b010;
#5; a1=3'd3;
$display("time = %t,a1=%b,sum=%b,carry=%b",$time,a1,sum,carry);
#5; a1=3'd4;
#5; a1=3'd5;
#5; a1=3'd6;
#5; a1=3'd7;
end
endmodule

```
### RUN
```bash
vlib work 
vlog half_adder.v
vlog half_adder_tb.v +acc
vsim work.half_adder_tb +acc
add wave -r * 
run -all
```
### TRANSCRIPT
<img width="987" height="632" alt="script for display" src="https://github.com/user-attachments/assets/b58c200e-c11b-43d1-9400-4ffba141bf3c" />
<br>

#### 2) $write
```bash

module full_adder_tb();
reg [2:0] a1;
wire sum,carry;

full_adder dut(.a1(a1), .s(sum), .c(carry));
initial begin

a1=3'b000;
#5; 
a1=3'b001;
#5; a1=3'b010;
#5; a1=3'd3;
$write("time = %t,a1=%b,sum=%b,carry=%b",$time,a1,sum,carry);
#5; a1=3'd4;
$write("time = %t,a1=%b,sum=%b,carry=%b",$time,a1,sum,carry);
#5; a1=3'd5;
#5; a1=3'd6;
#5; a1=3'd7;
end
endmodule

```
### RUN
```bash
vlib work 
vlog half_adder.v
vlog half_adder_tb.v +acc
vsim work.half_adder_tb +acc
add wave -r * 
run -all
```
### TRANSCRIPT
<img width="1035" height="635" alt="script for write full adder" src="https://github.com/user-attachments/assets/52a96f3e-5933-4586-a5d2-c842e1c06eca" />
<br>

#### 3) $strobe and $display 
```bash

module full_adder_tb();
reg [2:0] a1;
wire sum,carry;

full_adder dut(.a1(a1), .s(sum), .c(carry));
initial begin

a1=3'b000;
#0; 
a1=3'b001;
$display("time = %t,a1=%b,sum=%b,carry=%b",$time,a1,sum,carry);
$strobe("time = %t,a1=%b,sum=%b,carry=%b",$time,a1,sum,carry);
#5; a1=3'b010;
#5; a1=3'd3;
#5; a1=3'd4;
#5; a1=3'd5;
#5; a1=3'd6;
#5; a1=3'd7;
end
endmodule

```
### RUN
```bash
vlib work 
vlog half_adder.v
vlog half_adder_tb.v +acc
vsim work.half_adder_tb +acc
add wave -r * 
run -all
```
### TRANSCRIPT
<img width="1918" height="646" alt="display vs strobe transcript" src="https://github.com/user-attachments/assets/838f05a0-a160-461a-bda0-d9031a9d66bd" />
<br>

#### 4) $monitor and $stop 
```bash

module full_adder_tb();
reg [2:0] a1;
wire sum,carry;

full_adder dut(.a1(a1), .s(sum), .c(carry));
initial begin
$monitor("time = %t,a1=%b,sum=%b,carry=%b",$time,a1,sum,carry);
a1=3'b000;
#5; 
a1=3'b001;
#5; a1=3'b010;
#5; a1=3'd3;
#5; a1=3'd4;
#5; $stop();
#5; a1=3'd5;
#5; a1=3'd6;
#5; a1=3'd7;
end
endmodule

```
### RUN
```bash
vlib work 
vlog half_adder.v
vlog half_adder_tb.v +acc
vsim work.half_adder_tb +acc
add wave -r * 
run -all
```
### TRANSCRIPT
<img width="878" height="622" alt="$stop for full adder script" src="https://github.com/user-attachments/assets/a9384a1d-5e9b-495f-b908-49d0bdd300b6" />

<br>


#### 5) $monitor and $finish 
5.1) $finish in code
```bash

module full_adder_tb();
reg [2:0] a1;
wire sum,carry;

full_adder dut(.a1(a1), .s(sum), .c(carry));
initial begin
//$monitor("time = %t,a1=%b,sum=%b,carry=%b",$time,a1,sum,carry);
a1=3'b000;
#5; 
a1=3'b001;
#5; a1=3'b010;
#5; a1=3'd3;
#5; a1=3'd4;
#5; a1=3'd5;
#5; a1=3'd6;
#5; a1=3'd7;
#10; $finish();
end
endmodule

```
### RUN
```bash
vlib work 
vlog half_adder.v
vlog half_adder_tb.v +acc
vsim work.half_adder_tb +acc
add wave -r * 
run -all
```
### TRANSCRIPT
<img width="956" height="632" alt="$finish for full adder" src="https://github.com/user-attachments/assets/0c019f79-b804-464d-b786-5879afa1762b" />
<br>

5.2) $monitor and $finish in code
```bash
module full_adder_tb();
reg [2:0] a1;
wire sum,carry;

full_adder dut(.a1(a1), .s(sum), .c(carry));
initial begin
$monitor("time = %t,a1=%b,sum=%b,carry=%b",$time,a1,sum,carry);
a1=3'b000;
#5; 
a1=3'b001;
#5; a1=3'b010;
#5; a1=3'd3;
#5; a1=3'd4;
#5; a1=3'd5;
#5; a1=3'd6;
#5; a1=3'd7;
#10; $finish();
end
endmodule

```
### RUN
```bash
vlib work 
vlog half_adder.v
vlog half_adder_tb.v +acc
vsim work.half_adder_tb +acc
add wave -r * 
run -all
```
### TRANSCRIPT
<img width="960" height="637" alt="$finish_monitor for full adder" src="https://github.com/user-attachments/assets/6b1182bb-9612-4585-b18a-bb5843b39011" />

<br>

### WAVEFORM
<img width="1908" height="426" alt="full adder waveform" src="https://github.com/user-attachments/assets/24e4e40d-6571-4160-b5b1-a2e1ccaf93c3" />
