## Class object | Class Handles | Class Constructor
```bash

class example;
    bit [31:0] data;
    int id;

    task update(bit [31:0] u_data, int u_id);
        data = u_data;
        id   = u_id;
    endtask

    function display(example ex);
      $display("data=%0d id=%0h", ex.data, ex.id); 
    endfunction
endclass

module ex_class;
    initial begin
        example ex = new();

        ex.update(11,12);
        ex.display(ex);
    end
endmodule
```

## result:
<img width="977" height="330" alt="image" src="https://github.com/user-attachments/assets/a9d362a9-fee7-4d33-a531-47827ebd7151" />

## When Memory is not allocated for object ex2

```bash
class example;
    bit [31:0] data;
    int id;
endclass
module ex_class;
    initial begin
        example ex1,ex2;
        ex1= new();
		ex1.data = 11;
      	ex1.id=10;
      $display(ex1.data,ex1.id);
      
      if(ex2!== null) begin
      		ex2.data = 14;
      	ex2.id=15;
        $display(ex2.data,ex2.id);
      end
      else
        $display("Object is not declared");
        
    end
endmodule
```

## Result:
<img width="891" height="330" alt="image" src="https://github.com/user-attachments/assets/4e5cef51-52f6-4064-95f5-85de250e8543" />

