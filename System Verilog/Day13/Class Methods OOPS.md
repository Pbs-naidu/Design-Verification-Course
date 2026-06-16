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
