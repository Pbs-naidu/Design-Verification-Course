## Synchronous and Asynchronous Counters (Up Counter/Down Counter/Up Down Counter) (06/04/2026)
## Synchronous up Counter
### Design Code:
```bash
module sync_up_counter(
input clk,rst,
output reg [3:0] q
);
always @(posedge clk)
	begin
		if(rst)
			q<= 4'h0;
		else
			q<= q+1'b1;
	end
endmodule
```
### Testbench:
```bash
module sync_up_counter_tb;
	reg clk,rst;
	wire [3:0] q;
	sync_up_counter dut (.*);
	always #5 clk=~clk;
	initial
	begin 
     clk=0;rst=1;#10;
rst=0;#10;
#200;$finish();	 
	end
	endmodule
```
### RUN
```bash
vlib work 
vlog sync_up_counter.v
vlog sync_up_counter_tb.v +acc
vsim work.sync_up_counter_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1912" height="290" alt="up count waveform" src="https://github.com/user-attachments/assets/77df29a9-2105-4c52-a6cc-72bcee774ae1" />

<br>

## Synchronous Down Counter
### Design Code:
```bash
module sync_down_counter(
	input clk,rst,
	output reg [3:0] q
);
always @(posedge clk)
	begin
		if(rst)
			q<=4'hf;
		else
			q<=q - 1'b1;
	end
endmodule
```
### Testbench:
```bash
module sync_down_counter_tb;
	reg clk,rst;
	wire [3:0] q;
	sync_down_counter dut (.*);
	always #5 clk=~clk;
	initial
	begin 
     clk=0;rst=1;#10;
rst=0;#10;
#200;$finish();	 
	end
	endmodule
```
### RUN
```bash
vlib work 
vlog sync_down_counter.v
vlog sync_down_counter_tb.v +acc
vsim work.sync_down_counter_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1913" height="316" alt="down counter waveform" src="https://github.com/user-attachments/assets/00614178-d9cd-4683-a1d7-a5ec35201ce3" />


<br>

## Synchronous Up Down Counter
### Design Code:
```bash
module sync_up_down_counter(
	input clk,rst,m,
	output reg [3:0] q
);
always @(posedge clk)
	begin
		if(rst)
			q<=4'hf;
		else if(m)
			q<=q + 1'b1;
		else 
		q<=q-1'b1;
	end
endmodule
```
### Testbench:
```bash
module sync_up_down_counter_tb;
	reg clk,rst,m;
	wire [3:0] q;
	sync_up_down_counter dut (.*);
	always #5 clk=~clk;
	initial
	begin 
     clk=0;rst=1;m=1;#10;
rst=0;#10;
#50;m=1;
#20;m=0;
#200;$finish();	 
	end
	endmodule
```
### RUN
```bash
vlib work 
vlog sync_up_down_counter.v
vlog sync_up_down_counter_tb.v +acc
vsim work.sync_up_down_counter_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1897" height="323" alt="up_down_counter waveform" src="https://github.com/user-attachments/assets/735e005c-1d90-48be-a507-1d83f58bec26" />

<br>


## ASynchronous Up Counter
### Design Code:
```bash
module Async_up_counter(
input clk,rst,
output reg [3:0] q
);
always @(posedge clk or posedge rst)
	begin
		if(rst)
			q<= 4'h0;
		else
			q<= q+1'b1;
	end
endmodule
```
### Testbench:
```bash
module Async_up_counter_tb;
	reg clk,rst;
	wire [3:0] q;
	Async_up_counter dut (.*);
	always #5 clk=~clk;
	initial
	begin 
     clk=0;rst=1;#20;
rst=0;#10;
#200;$finish();	 
	end
	endmodule
```
### RUN
```bash
vlib work 
vlog Async_up_counter.v
vlog Async_up_counter_tb.v +acc
vsim work.Async_up_counter_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1905" height="293" alt="async up copunter waveform" src="https://github.com/user-attachments/assets/3a422065-b846-4ee9-b277-8bab9717ebe7" />


<br>

## ASynchronous Down Counter
### Design Code:
```bash
module Async_down_counter(
	input clk,rst,
	output reg [3:0] q
);
always @(posedge clk or posedge rst)
	begin
		if(rst)
			q<=4'hf;
		else
			q<=q - 1'b1;
	end
endmodule
```
### Testbench:
```bash
module Async_down_counter_tb;
	reg clk,rst;
	wire [3:0] q;
	Async_down_counter dut (.*);
	always #5 clk=~clk;
	initial
	begin 
     clk=0;rst=1;#10;
rst=0;#10;
#200;$finish();	 
	end
	endmodule
```
### RUN
```bash
vlib work 
vlog Async_down_counter.v
vlog Async_down_counter_tb.v +acc
vsim work.Async_down_counter_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1892" height="235" alt="async down copunter waveform" src="https://github.com/user-attachments/assets/162721da-bfcc-4eee-b608-bb321572938a" />

<br>

## ASynchronous Up Down Counter
### Design Code:
```bash
module Async_up_down_counter(
	input clk,rst,m,
	output reg [3:0] q
);
always @(posedge clk or posedge rst)
	begin
		if(rst)
			q<=4'hf;
		else if(m)
			q<=q + 1'b1;
		else 
		q<=q-1'b1;
	end
endmodule
```
### Testbench:
```bash
module Async_up_down_counter_tb;
	reg clk,rst,m;
	wire [3:0] q;
	Async_up_down_counter dut (.*);
	always #5 clk=~clk;
	initial
	begin 
     clk=0;rst=1;m=1;#50;
rst=0;#10;
#50;m=1;
#20;m=0;
#200;$finish();	 
	end
	endmodule
```
### RUN
```bash
vlib work 
vlog Async_up_down_counter.v
vlog Async_up_down_counter_tb.v +acc
vsim work.Async_up_down_counter_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1896" height="287" alt="async up down waveform" src="https://github.com/user-attachments/assets/59062809-2621-4c86-bfbd-041d851a8e80" />


<br>

## Moore FSM 1011
### Design Code: `bat`
```bash
module 1011_moore(
input clk,rst,din,
output reg detected
);
localparam idle =3'b000,
			s1=3'b001,
			s10=3'b010,
			s101=3'b011,
			s1011=3'b100;
	reg [2:0] p_state,n_state; 
	assign detected = (p_state == s1011)?1'b1:1'b0;
	always @(posedge clk or negedge rst)
		begin
			if(rst) //rst == 1
				p_staet <= idle;
				else
				p_state <=n_state;
		end
    always @(*)
		begin	
			case(p_state)
    idle: begin
        if(din)    
            n_state = s1;
        else       
            n_state = idle;
    end

    s1 : begin
        if(din)   
            n_state = s1
        else       
            n_state = s10;
    end
	
	s10 : begin
    if(!din)   //din ==0
        n_state = idle;
    else       //din ==1
        n_state = s101;
end

   s101 : begin
    if(din)   
        n_state = s1011;
    else      
        n_state = s10;
end

s101 : begin
    if(din)   
        n_state = s1011;
    else     
        n_state = s10;
end

s1011 : begin
    if(din)   
        n_state = s1;    //overlapping
    else      
        n_state = s10;   //nonoverlapping
end

default:n_state = idle;

endcase
end
endmodule
```
### Testbench:
```bash

```
### RUN
```bash

```
### waveform:


<br>
