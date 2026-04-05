## PIP0 (Parallel In parallel Out) (02/04/2026)
### Design Code:
```bash
module pipo (
input clk,rst,
input [3:0] pin,
output reg q0,q1,q2,q3
);
always @(posedge clk)
	begin
		if(rst)
			begin	
				q3<= 1'b0;
				q2<=1'b0;
				q1<=1'b0;
				q0<=1'b0;
	        end
		else 
			begin
			q3 <= pin[3];
			q2 <= pin[2];
			q1 <= pin[1];
			q0 <= pin[0];
            end		
	end
endmodule
```
### Testbench:
```bash
module pipo_tb;
reg clk,rst;
reg [3:0] pin;
wire q0,q1,q2,q3;
pipo dut(.*);
always #5 clk=~clk;
initial
	begin
		clk=0;rst=1;pin=4'b1101;
		#10;
		rst=0;
		#10;
		pin=4'b1001;
		#10;
		#80;$finish();
		end
endmodule
```
### RUN
```bash
vlib work 
vlog pipo.v
vlog pipo_tb.v +acc
vsim work.pipo_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1898" height="330" alt="pipo waveform" src="https://github.com/user-attachments/assets/f18dcf03-ba02-4f35-bbd9-4a5de8ec10a3" />

<br>

## PIS0 (Parallel In Serial Out) (02/04/2026)
### Design Code:
```bash
module piso (
input clk,rst,
input m,
input [3:0] pin,
output reg q0
);
reg q3,q2,q1;
always @(posedge clk)
	begin
		if(rst)
			begin	
				q3<= 1'b0;
				q2<=1'b0;
				q1<=1'b0;
				q0<=1'b0;
	        end
		else if(m)
			begin
			q3 <= pin[3];
			q2 <= pin[2];
			q1 <= pin[1];
			q0 <= pin[0];
            end	
		else	
			begin
				q3<=1'b0;
				q2 <= q3;
				q1 <= q2;
				q0 <= q1;
			end			
	end
endmodule
```
### Testbench:
```bash
module piso_tb;
reg clk,rst;
reg m;
reg [3:0] pin;
wire q0;
piso dut(.*);
always #5 clk=~clk;
initial
	begin
		clk=0;rst=1;pin=4'b1101;m=1;
		#10;
		rst=0;
		#10;
		m=0;
		#10;
		#80;$finish();
		end
endmodule
```
### RUN
```bash
vlib work 
vlog piso.v
vlog piso_tb.v +acc
vsim work.piso_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1907" height="461" alt="piso waveform" src="https://github.com/user-attachments/assets/cdc0222d-0be6-4e5d-982d-22ebb33aa43e" />

<br>

## SIP0 (Serial In Parallel Out) (02/04/2026)
### Design Code:
```bash
module sipo (
input clk,rst,
input  sin,
output reg q0,q1,q2,q3
);
always @(posedge clk)
	begin
		if(rst)
			begin	
				q3<= 1'b0;
				q2<=1'b0;
				q1<=1'b0;
				q0<=1'b0;
	        end
	else 
	begin
	    q3<= sin;
		q2<=q3;
		q1<=q2;
		q0<=q1;
	end
	end
endmodule
```
### Testbench:
```bash
module sipo_tb;
reg clk,rst;
reg sin;
wire q0,q1,q2,q3;
sipo dut(.*);
always #5 clk=~clk;
initial
	begin
	clk=0;rst=1;sin=1'b1;#10;
		rst=0;sin=1'b1;#10;
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
vlog sipo.v
vlog sipo_tb.v +acc
vsim work.sipo_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1905" height="290" alt="sipo waveform" src="https://github.com/user-attachments/assets/e9e3211e-bbb2-4487-be22-da86254959e7" />


<br>
