# Basic Logic Gates using Model sim and Notepad++ (25/03/2026)
## 1. AND GATE
### VERILOG CODE
<img width="411" height="186" alt="and code" src="https://github.com/user-attachments/assets/e0dd57db-0035-4cee-b28e-896ea7248859" /><br>
### TESTBENCH
<img width="766" height="367" alt="andtb" src="https://github.com/user-attachments/assets/7b6f9684-b856-4955-bb7d-f2f674395c55" /><br>
### RUN
<img width="458" height="211" alt="and run do" src="https://github.com/user-attachments/assets/95a5fab9-74cc-4338-9634-7b2ad31d796c" /><br>
### TRANSCRIPT
<img width="1067" height="535" alt="and transcript" src="https://github.com/user-attachments/assets/23abe823-ca09-4178-9974-97c0a963a381" /><br>
### WAVEFORM
<img width="1905" height="532" alt="and waveform" src="https://github.com/user-attachments/assets/7dd28039-8bd1-4d79-b4dd-a65288900794" /><br>

## 2. OR GATE
### VERILOG CODE
<img width="412" height="185" alt="or code - Copy" src="https://github.com/user-attachments/assets/5b06b05c-60fc-4b46-afef-4d53a6b83f1a" /><br>
### TESTBENCH
<img width="653" height="386" alt="or tb - Copy" src="https://github.com/user-attachments/assets/490a6a95-e65c-4d8e-be27-e28dca87cd5b" /><br>
### RUN
<img width="1052" height="497" alt="or transcript - Copy" src="https://github.com/user-attachments/assets/91afe740-c336-4854-b05b-73b1da4c3228" /><br>
### TRANSCRIPT
<img width="460" height="180" alt="or do file - Copy" src="https://github.com/user-attachments/assets/351e21a0-53f0-4ac6-a283-0f60044102d4" /><br>
### WAVEFORM
<img width="1907" height="311" alt="or waveform - Copy" src="https://github.com/user-attachments/assets/9d08574f-b5c3-4b2f-9e13-f19ec9e0c852" /><br>

## 3. EXOR GATE
### VERILOG CODE
<img width="447" height="217" alt="xor code" src="https://github.com/user-attachments/assets/d9d0fb42-05d9-4870-bc49-6f26d5fe1c4c" /><br>
### TESTBENCH
<img width="675" height="367" alt="xor tb" src="https://github.com/user-attachments/assets/92e5f5a3-c58d-4303-ae09-d4680aaa96fa" /><br>
### RUN
<img width="1916" height="597" alt="or_gate_run_file" src="https://github.com/user-attachments/assets/a34e1622-9ac3-48cb-bcad-68a272b031e8" /><br>
### TRANSCRIPT
<img width="1862" height="667" alt="transcript exor" src="https://github.com/user-attachments/assets/7a284c5f-61d2-433a-8792-5e9ccee27837" /><br>
### WAVEFORM
<img width="1897" height="691" alt="exor_waveform" src="https://github.com/user-attachments/assets/7b5b7d46-51d9-480c-926f-70270d792acb" /><br>

## 4. NAND GATE
### VERILOG CODE
<img width="483" height="221" alt="nand code" src="https://github.com/user-attachments/assets/4f31693c-3ca3-47f2-92f9-3cc9479e610d" /><br>
### TESTBENCH
<img width="771" height="392" alt="nand tb" src="https://github.com/user-attachments/assets/47645031-f91f-41a8-8fbb-8156c46f1dd5" /><br>
### RUN
<img width="648" height="217" alt="nand run" src="https://github.com/user-attachments/assets/d88a2f39-7059-492d-9a23-3d5cc2e06845" /><br>
### TRANSCRIPT
<img width="997" height="497" alt="nand script" src="https://github.com/user-attachments/assets/9851ed8a-5b64-49c9-badf-8c3836950e8f" /><br>
### WAVEFORM
<img width="1893" height="445" alt="nand waveform" src="https://github.com/user-attachments/assets/6cfdb855-ad7c-4cfc-92bc-9a7c1ff3cad3" /><br>

## 5. NOR GATE
### VERILOG CODE
<img width="472" height="212" alt="nor code" src="https://github.com/user-attachments/assets/f4db64ac-3023-4236-811f-360c358f63c6" /><br>
### TESTBENCH
<img width="721" height="407" alt="nor tb code" src="https://github.com/user-attachments/assets/5c496384-fcd0-4255-bdc1-7602c7ae543f" /><br>
### RUN
<img width="487" height="173" alt="nor run" src="https://github.com/user-attachments/assets/abb70378-fc98-4572-a991-893cf3f5f5c9" /><br>
### TRANSCRIPT
<img width="1083" height="503" alt="nor script" src="https://github.com/user-attachments/assets/3f3fc57c-c760-42db-b925-27b5b6675600" /><br>
### WAVEFORM
<img width="1888" height="343" alt="nor waveform" src="https://github.com/user-attachments/assets/7c0558bb-592b-457f-a2c3-ed47da446806" /><br>


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
I) $finish in code
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

II) $monitor and $finish in code
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
