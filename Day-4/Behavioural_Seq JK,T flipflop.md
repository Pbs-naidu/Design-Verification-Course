# Flipflops (01/04/2026)
## 1.jk Flipflop 
### Design Code:
```bash
module jk_ff(
	input clk,rst,j,k,
	output reg q
);

always @(posedge clk)
begin
	if(j == 1'b0 && k == 1'b0)
		q<= q;
	else if(j == 1'b0 && k == 1'b1)
		q<=1'b0;
	else if(j == 1'b1 && k == 1'b0)
		q<=1'b1;
	else
		q<=~q;
end
endmodule
```
### Testbench:
```bash
module jk_ff_tb;

reg clk,rst,j,k;
wire q;
jk_ff dut(.*);
always #5 clk=~clk;
	initial begin
    clk=0;rst=1;j=0;k=1;
	clk=0;j=1;k=0;
	#10;j=0;k=1;
	#10;j=0;k=0;
	#10;j=1;k=1;
	#10;$finish();
end
endmodule
```
### RUN
```bash
vlib work 
vlog jk_ff.v
vlog jk_ff_tb.v +acc
vsim work.jk_ff_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1888" height="313" alt="jk flipfliop waveform after removing @posedge from test bench" src="https://github.com/user-attachments/assets/df1a6cd6-3fd3-46c5-af0d-61946404e939" />
<br>

## 2.T Flipflop (02/04/2026)
### Design Code:
```bash
module t_ff(
	input clk,rst,t,
	output reg q
);

always @(posedge clk)
begin
	if(rst == 1'b1)
	q<=1'b0;
	
	//else if(j == 1'b1 && k == 1'b0)
	else if(t == 1'b0)
		q<= ~q;
	else
		q<=q;

end
endmodule
```
### Testbench:
```bash
module t_ff_tb;

reg clk,rst,t;
wire q;
t_ff dut(.*);

always #5 clk=~clk;
	initial begin
	$monitor("time =%t,rst=%b,t=%b,q=%b",$time,rst,t,q);
	clk=0;rst=1;t=0;#10;
	rst=1;#10; // default t=0 is stored because of reg type
	rst=0;t=0;#10;
	t=1;#10;
	#5;$finish();

end

endmodule
```
### RUN
```bash
vlib work 
vlog t_ff.v
vlog t_ff_tb.v +acc
vsim work.t_ff_tb +acc
add wave -r * 
run -all
```
### Transcript:
<img width="968" height="588" alt="skript for t flipflop" src="https://github.com/user-attachments/assets/fc6d21d0-7c03-402b-95c0-37df39c35819" /><br>

### waveform:
<img width="1912" height="347" alt="t_ff_waveform" src="https://github.com/user-attachments/assets/91f39d19-36d6-4116-b6f4-fba5c95a3f8b" />

<br>
