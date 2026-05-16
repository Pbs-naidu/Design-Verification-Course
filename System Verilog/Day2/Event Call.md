 # Verilog Event to call Task A after Task B completion
 ```bash
module event_demo;

 event done;

 task taskB;
 begin
 $display("Task B Started");
  #10;
 -> done;
 $display("Task B Completed");
  end
 endtask

task taskA;
begin
   @done;
 $display("Task A Started after Task B");
   end
 endtask

 initial
begin
   fork
 taskA();
 taskB();
 join
 end
endmodule

```
