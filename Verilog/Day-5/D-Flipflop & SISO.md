## 3.D Flipflop (02/04/2026)
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

# Shift Registers
## 1.SISO (Serial In Serial Out)
### Design Code:
```bash
module siso(
	input clk,rst,
	input sin,
	output reg sout
);
	reg q3,q2,q1; // i first declared as wire but it needs to store the value
	always @(posedge clk)
		begin
			if(!rst)
			begin
				q3<=0;
				q2<=0;
				q1<=0;
				sout<=0;	
			end
		else
		begin
			q3<= sin;
			q2<=q3;
			q1<=q2;
			sout<=q1;
		end
        end
endmodule
```
### Testbench:
```bash
module siso_tb;
reg clk,rst;
reg sin;
wire sout;
siso dut(.*);
always #5 clk=~clk;
initial
	begin
		clk=0;rst=0;sin=1'b1;#10;
		rst=1;sin=1'b1;#10;
		sin=1'b0;#10;
		sin=1'b1;#10;
		sin=1'b1;#10;
		sin=1'b0;#10;
		sin=1'b0;#10;
		#10;
		#10;
		#10;$finish();
		end
endmodule
```
### RUN
```bash
vlib work 
vlog siso.v
vlog siso_tb.v +acc
vsim work.siso_tb +acc
add wave -r * 
run -all
```

### waveform:
<img width="1906" height="347" alt="siso waveform" src="https://github.com/user-attachments/assets/a6b7f694-6506-4333-bfbd-9d33fc5afc65" /><br>
