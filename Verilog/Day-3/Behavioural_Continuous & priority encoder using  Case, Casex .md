# Behavioural Model (31/03/2026)
## 1.Continuous
## 2.Sequential

# 1.Continious 
## XOR GATE
### Design Code:
```bash
module xorgate(
input a,b,
output reg y 

);

always@( a or b ) // also can be used as a,b
begin
	if(a==1'b0 && b==1'b0)
		y=1'b0;
	else if(a==1'b0 && b==1'b1)
		y=1'b1;
	else if(a==1'b1 && b==1'b0)
		y=1'b1;
	else if(a==1'b1 && b==1'b1)
		y=1'b0;
	else
	y= 'x;

end

endmodule
```
### Testbench:
```bash
module xorgate_tb;
reg a,b;
wire y;

xorgate dut (a,b,y);

initial 
begin 
$monitor ("time=%t,a=%b,b=%b,y=%b",$time,a,b,y);

#5;a=1;b=0;
#5;a=0;b=0;
#5;a=0;b=1;
#5;a=1;b=1;

#5;$finish();
end

endmodule

```
### RUN
```bash
vlib work 
vlog xorgate.v
vlog xorgate_tb.v +acc
vsim work.xorgate_tb +acc
add wave -r * 
run -all
```
### Transcript:
<img width="825" height="577" alt="xor transcript" src="https://github.com/user-attachments/assets/47ffd743-770c-4eb5-b3c7-b002a9e9a03e" />


## XOR GATE using case
### Design :
```bash
module xorgate(
input [1:0] a,
output reg y 
);
always@( a )
begin
case(a)
	2'b00:y=1'b0;
	2'b01:y=1'b1;
	2'b10:y=1'b1;
	2'b11:y=1'b0;
	default:y='x;
endcase
end
endmodule
```

### Testbench:
```bash
module xorgate_tb;
reg [1:0] a;
wire y;
xorgate dut (a,y);
initial 
begin 
$monitor ("time=%t,a=%b,y=%b",$time,a,y);
#5;a=2'b01;
#5;a=2'b00;
#5;a=2'b10;
#5;a=2'b11;
#5;$finish();
end
endmodule
```
### Waveform:
<img width="1901" height="322" alt="xor behaviour waveform" src="https://github.com/user-attachments/assets/ed90278d-2744-4fea-a40a-08feff6a47c7" /><br>

## Priority encoder using case
### Design Code:
```bash
module pri4_2_enc(
input [3:0]a,
output reg [1:0] y
);
always @(a)
begin
	case(a)
	4'h1xxx:y=2'b11;
	4'h01xx:y=2'b10;
	4'h001x:y=2'b01;
	default : y=2'b00;
	endcase
end
endmodule
```
### Testbench:
```bash
module pri4_2_enc_tb();
reg [3:0] a;
wire [1:0]y;
integer i;
pri4_2_enc dut(.*);
initial
	begin
	 for(i=0;i<16;i=i+1)
		begin
		a=i; #5;
		end
	end
endmodule
```
### RUN
```bash
vlib work 
vlog pri4_2_enc.v
vlog pri4_2_enc_tb.v +acc
vsim work.pri4_2_enc_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1907" height="297" alt="priority encoder wave form for case" src="https://github.com/user-attachments/assets/1f079a47-d0ed-453a-920e-cf18e1c44bf6" /><br>

## Priority encoder using casex
### Design Code:
```bash
module pri4_2_enc(
input [3:0]a,
output reg [1:0] y
);
always @(a)
begin
	casex(a)
	4'b1xxx:y=2'b11;
	4'b01xx:y=2'b10;
	4'b001x:y=2'b01;
	default : y=2'b00;
	endcase
end
endmodule
```
### Testbench:
```bash
module pri4_2_enc_tb();
reg [3:0] a;
wire [1:0]y;
integer i;
pri4_2_enc dut(.*);
initial
	begin
	 for(i=0;i<16;i=i+1)
		begin
		a=i; #5;
		end
	end
endmodule
```
### RUN
```bash
vlib work 
vlog pri4_2_enc.v
vlog pri4_2_enc_tb.v +acc
vsim work.pri4_2_enc_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1893" height="432" alt="casex priority encode waveform" src="https://github.com/user-attachments/assets/65c5d91b-dcde-47a5-956d-ab9649c2f948" /><br>
