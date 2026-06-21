## Extern Method in Class
&rarr; Provides Facility for class methods to define outside an class Body.
```bash
class example;

   bit [31:0] data;
   int id;

   extern function void display();
   extern task delay();

endclass


function void example::display();
   $display("time=%0t,data = %0d, id = %0d",$time, data, id);
endfunction


task example::delay();
   #30;
  $display("time=%0t,data = %0d, id = %0d",$time, data, id);
endtask


module ex_class;

   example ex;

   initial begin

      ex = new();

      ex.data = 100;
      ex.id   = 1;

      ex.display(); // 100, 1
      ex.delay();   // after 30 time units: 100, 1

   end

endmodule
```
## Result:
<img width="787" height="273" alt="image" src="https://github.com/user-attachments/assets/5975ae01-b819-4ef9-aa02-cefa74c88a2f" />

## Parameterized

```bash
class err_trans;
   bit [31:0] err_data;
   bit error;
endclass


class transaction #(parameter WIDTH = 32,
                    type D_TYPE = err_trans);

   bit [WIDTH-1:0] data;
   D_TYPE err_tr;

   function void display();
      $display("data=%0d, err_data=%0h, error=%0b",
               data, err_tr.err_data, err_tr.error);
   endfunction

endclass


module example;

   transaction tr;

   initial begin

      tr = new();
      tr.err_tr = new();

      tr.data = 100;
      tr.err_tr.err_data = 32'hFFFF_FFFF;
      tr.err_tr.error = 1;

      tr.display();

   end

endmodule
```

## Result:
<img width="978" height="275" alt="image" src="https://github.com/user-attachments/assets/1211a004-b99a-42b0-8d38-03342bb31db4" />

## Typedef 
&rarr; In Certain Cases, Class Handle of another Class is Required if that class is not yet Declared.

### Without Typedef

```bash
class transaction_A;

   bit [31:0] data;
   bit id;

   transaction_b tr_B = new(); // ERROR: transaction_b not defined yet

   function void display();
      $display("data=%0d id=%0d addr=%0d",
               data, id, tr_B.addr);
   endfunction

endclass


class transaction_b;
   bit [31:0] addr = 100;
endclass


module class_ex;

   transaction_A tr_A;

   initial begin
      tr_A = new();
      tr_A.data = 100;
      tr_A.id   = 1;
      tr_A.display();
   end

endmodule
```
## Result: 
### **Error**
<img width="907" height="246" alt="image" src="https://github.com/user-attachments/assets/eaa8b599-bd82-4834-8946-fab84db55f5c" />

## With Typedef

```bash
typedef transaction_b;
class transaction_A;

   bit [31:0] data;
   bit id;

   transaction_b tr_B = new(); 

   function void display();
      $display("data=%0d id=%0d addr=%0d",
               data, id, tr_B.addr);
   endfunction

endclass


class transaction_b;
   bit [31:0] addr = 100;
endclass


module class_ex;

   transaction_A tr_A;

   initial begin
      tr_A = new();
      tr_A.data = 100;
      tr_A.id   = 1;
      tr_A.display();
   end

endmodule
```
## Result:
<img width="847" height="270" alt="image" src="https://github.com/user-attachments/assets/a24766ff-6d5d-491b-ab19-986c3272cbae" />
