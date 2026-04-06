## USR (Universal Shift Register) (06/04/2026)
### Design Code:
```bash
//universal shift register
module usr(
input clk,rst,
input [1:0] sel,
input [3:0] pin,
output reg [3:0] q
);

always @(posedge clk)
	begin
		if(rst)
			q <= 4'b0000;
		else if(s == 2'b11)
		begin
			q[3]<=pin[3];
			q[2]<=pin[2];
			q[1]<=pin[1];
			q[0]<=pin[0];
		end
		else if(s == 2'b10)
		begin
			q[0] <=1'b1;
			q[1] <= q[0];
			q[2] <= q[1];
			q[3] <= q[2];
		end
		else if (s == 2'b01)
		begin
		    q[0] <=q[1];
			q[1] <= q[2];
			q[2] <= q[3];
			q[3] <= 1'b1;
		end
		else
		q<=q;
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
