##  (02/04/2026)
### Design Code:
```bash
module d_ff(
	input clk,rst,d,
	output reg q
);
always @(posedge clk)
begin
	if(rst == 1'b1)
	q<=1'b0;
	else
    q<=d;
end
endmodule
```
### Testbench:
```bash
module d_ff_tb;
reg clk,rst,d;
wire q;
d_ff dut(.*);
always #5 clk=~clk;
	initial begin
	$monitor("time =%t,rst=%b,t=%b,q=%b",$time,rst,d,q);
	clk=0;rst=1;d=0;#10;
	rst=1;#10; // default t=0 is stored because of reg type
	rst=0;d=0;#10;
	d=1;#10;
	#5;$finish();
end
endmodule
```
### RUN
```bash
vlib work 
vlog d_ff.v
vlog d_ff_tb.v +acc
vsim work.d_ff_tb +acc
add wave -r * 
run -all
```
### Transcript:
<img width="777" height="387" alt="d_ff script" src="https://github.com/user-attachments/assets/6a702c00-4086-4970-9568-4e803e2ef8e1" />
<br>

### waveform:
<img width="1896" height="247" alt="dff waveform" src="https://github.com/user-attachments/assets/cd85498a-0095-40e6-8bdc-f5433f07e2c1" />

<br>
