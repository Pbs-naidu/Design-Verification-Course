## Moore FSM 1011
### Design Code: 
```bash
module moore_1011(

input clk,rst,din,
output detected
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
			if(rst) 
				p_state <= idle;
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
            n_state = s1;
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
module moore_1011_tb;
    reg clk, rst, din;
    wire detected;

    moore_1011 dut (.*);

    always #5 clk = ~clk;

   initial
begin
    clk=0; rst=1; din=1'b1; @(posedge clk);
    rst=0; din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    @(posedge clk);
    @(posedge clk);
    $finish();
end

endmodule
```
### RUN
```bash
vlib work 
vlog moore_1011.v
vlog moore_1011_tb.v +acc
vsim work.moore_1011_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1891" height="385" alt="more 1011 waveform" src="https://github.com/user-attachments/assets/61c03b1a-1f54-4ad1-b58e-cfa8351f30ff" />


<br>

## Mealy FSM 1011
### Design Code: 
```bash
module mealy_1011(

input clk,rst,din,
output detected
);

localparam idle =3'b000,
			s1=3'b001,
			s10=3'b010,
			s101=3'b011,
			
	reg [2:0] p_state,n_state; 
	
	assign detected = (p_state == s101)?1'b1:1'b0;
	
	always @(posedge clk or negedge rst)
		begin
			if(rst) 
				p_state <= idle;
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
            n_state = s1;
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
        n_state = s1;
    else     
        n_state = s10;
end

default:n_state = idle;

endcase
end
endmodule
```
### Testbench:
```bash
module mealy_1011_tb;
    reg clk, rst, din;
    wire detected;

    mealy_1011 dut (.*);

    always #5 clk = ~clk;

   initial
begin
    clk=0; rst=1; din=1'b1; @(posedge clk);
    rst=0; din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b1; @(posedge clk);
    din=1'b0; @(posedge clk);
    @(posedge clk);
    @(posedge clk);
    $finish();
end

endmodule
```
### RUN
```bash
vlib work 
vlog mealy_1011.v
vlog mealy_1011_tb.v +acc
vsim work.mealy_1011_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1897" height="181" alt="mealy 1011 waveform" src="https://github.com/user-attachments/assets/d30e3284-6227-438b-8ea0-023c94e49cff" />


<br>

## Mealy FSM 1011
### Design Code: 
```bash
module mealy_1011(

input clk,rst,din,
output detected
);

localparam idle =3'b000,
			s1=3'b001,
			s10=3'b010,
			s101=3'b011,
			
	reg [2:0] p_state,n_state; 
	
	assign detected = (p_state == s101)?1'b1:1'b0;
	
	always @(posedge clk or negedge rst)
		begin
			if(rst) 
				p_state <= idle;
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
            n_state = s1;
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
        n_state = s1;
    else     
        n_state = s10;
end

default:n_state = idle;

endcase
end
endmodule
```
### Testbench:
```bash
module mealy_1011_tb;
    reg clk, rst, din;
    wire detected;

    mealy_1011 dut (.*);

    always #5 clk = ~clk;

   initial
begin
    clk=0; rst=1; din=1'b1; @(posedge clk);
    rst=0; din=1'b1; @(posedge clk);
	repeat(30)
begin
	din = $random;@(posedge clk);
	end
    @(posedge clk);
    @(posedge clk);
    $finish();
end

endmodule
```
### RUN
```bash
vlib work 
vlog mealy_1011.v
vlog mealy_1011_tb.v +acc
vsim work.mealy_1011_tb +acc
add wave -r * 
run -all
```
### waveform:
<img width="1897" height="181" alt="mealy 1011 waveform" src="https://github.com/user-attachments/assets/d30e3284-6227-438b-8ea0-023c94e49cff" />


<br>

