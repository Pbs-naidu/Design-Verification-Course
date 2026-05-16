## Default Value of Data Types

```bash
 module hw_qg1;
   int a;
   logic b; 
   bit [3:0] c; 
   integer d;
   reg [7:0] e;
   byte f;
   real g;
   initial 
     begin
       $display("a = %0d", a);
       $display("b = %b", b); 
       $display("c = %b", c);
       $display("d = %0d", d); 
       $display("e = %b", e);
       $display("f = %0d", f);
       $display("g = %f", g); 
                                  
      end
 endmodule
```

## Results:
<img width="921" height="347" alt="image" src="https://github.com/user-attachments/assets/54ec99a9-bc83-4ddd-b46d-cf6936e0865a" />
