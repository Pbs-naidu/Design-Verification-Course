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
     
   end

endmodule

```

## Result:
<img width="798" height="317" alt="image" src="https://github.com/user-attachments/assets/c8faeb03-a521-4ded-84cf-0322f66135b5" />


## With Virtual Class
- if Base has Virtual function then Child will Override the Base.
```bash
class parent_trans;

   bit [31:0] data;
   int id;

   virtual function void display();
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

      c_tr.data = 10;
      c_tr.id   = 2;

      p_tr.data = 5;
      p_tr.id   = 1;

      p_tr.display(); 
   end

endmodule
```

## Result:
<img width="842" height="318" alt="image" src="https://github.com/user-attachments/assets/79991f7d-0bdd-46b4-9fcc-9fa42c65d674" />

