## Virtual keyword
- Used for Virtual functions and Tasks.
- When we have an child class --> Assigned to its Base class
- When we Declare Methods --> Virtual Base Class handle can call Method of its child.

## Without Virtual keyword

```bash
class parent_trans;
   bit [31:0] data;
   int id;

   function void display();
      $display("Base: Value of data = %0h and id = %0h", data, id);
   endfunction
endclass


class child_trans extends parent_trans;

   function void display();
      $display("Child: Value of data = %0h and id = %0h", data, id);
   endfunction

endclass


module class_example;

   initial begin
      parent_trans p_tr;
      child_trans  c_tr;

      c_tr = new();

      p_tr = c_tr;

      p_tr.data = 5;
      p_tr.id   = 1;

      p_tr.display(); 
     c_tr.display();
   end

endmodule

```

## Result:
<img width="790" height="332" alt="image" src="https://github.com/user-attachments/assets/c9684f8a-6e94-4614-ba7a-d5ced8098d26" />
