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

## Abstract (Virtual class)
&rarr; A Virtual Class exists only to be inherited - it can't be instantiated.<br>
&rarr; A Virtual Class (only) may have **pure** Virtual Methods.<br>
&rarr; Subclasses must Provide implementation

```bash
virtual class parent_trans;

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

      child_trans  c_tr;
      parent_trans p_tr;

      c_tr = new();

      p_tr = c_tr;

      c_tr.data = 5;
      c_tr.id   = 1;

      p_tr.display();   
	  
   end

endmodule
```
## Result:
<img width="822" height="323" alt="image" src="https://github.com/user-attachments/assets/7a477207-1407-44d6-aa0e-d2bec1153a4c" />

## Polymorphism
&rarr; Parent Class Handle can invoke Child class Method

```bash
class parent;

   bit [31:0] data;
   int id;

   virtual function void display();
      $display("Base: Value of data = %0d, id = %0d", data, id);
   endfunction

endclass


class child_A extends parent;

   function void display();
      $display("Child_A: Value of data = %0d, id = %0d", data, id);
   endfunction

endclass


class child_B extends parent;

   function void display();
      $display("Child_B: Value of data = %0d, id = %0d", data, id);
   endfunction

endclass


class child_C extends parent;

   function void display();
      $display("Child_C: Value of data = %0d, id = %0d", data, id);
   endfunction

endclass


module class_example;

   initial begin

      parent  p_A, p_B, p_C;
      child_A c_A = new();
      child_B c_B = new();
      child_C c_C = new();

      c_A.data = 200;
      c_A.id   = 2;

      c_B.data = 300;
      c_B.id   = 3;

      c_C.data = 400;
      c_C.id   = 4;

      p_A = c_A;
      p_B = c_B;
      p_C = c_C;

      p_A.data = 100;
      p_A.id   = 1;

      p_A.display();
      p_B.display();
      p_C.display();

   end

endmodule

```

## Result:
<img width="882" height="335" alt="image" src="https://github.com/user-attachments/assets/a53f92a3-02ca-4aac-adf9-404413857a0a" />

## Scope Resolution Opertor (::)
&rarr; This refers to static class members without its handle

```bash
class transaction;

   bit [31:0] data;
   static int id;

   static function void disp(int id);
      $display("Value of id = %0h", id);
   endfunction

   function void auto_disp(int id);
      $display("Value of id = %0h", id);
   endfunction

endclass


module class_example;

   initial begin

      transaction::id = 5;

      transaction::disp(transaction::id); 

 

   end

endmodule

```
## Result:
<img width="926" height="331" alt="image" src="https://github.com/user-attachments/assets/70901460-3f2e-4e6f-aabe-209f8f95b2b7" />
