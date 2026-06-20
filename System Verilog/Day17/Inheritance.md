## Parent and Child
```bash

class Parent;
  bit [31:0] data = 100;
  int id = 1;

  function void display();
    $display(data, id);
  endfunction
endclass

class child extends Parent;
  bit [31:0] data = 200;
  int id = 2;
 
  function void display();
    $display(data, id);
  endfunction
endclass

module class_ex;
  initial begin
    child child_tr;

    child_tr = new();
 
    child_tr.display();
  end
endmodule

```

## Result:
<img width="962" height="315" alt="image" src="https://github.com/user-attachments/assets/89b67098-a669-4299-b3b6-482ca4895de8" />

## Multi Inheritance

```bash
class ex_parent;

  bit [31:0] data;

  function void display_parent();
    $display(data);
  endfunction

endclass


class c1 extends ex_parent;

  int id;

  function void display_child();
    $display(id);
  endfunction

endclass


class c3 extends c1;

  int addr;
  function void display_subclass();
    $display(addr);
  endfunction

endclass


module example;

  initial begin

    c3 c3_handle;

    c3_handle = new();

    c3_handle.data = 5;
    c3_handle.id   = 1;
    c3_handle.addr = 10;

    c3_handle.display_parent();
    c3_handle.display_child();
    c3_handle.display_subclass();

  end

endmodule
```

## Result:
<img width="802" height="318" alt="image" src="https://github.com/user-attachments/assets/7fe5a1e4-1756-43ce-b549-a26ea7b83be7" />

## Super Keyword

```bash

class Parent;
  bit [31:0] data = 100;
  int id = 1;

  function void display();
    $display(data, id);
  endfunction
endclass

class child extends Parent;
  bit [31:0] data = 200;
  int id = 2;
 
  function void display();
    super.display();
    $display(data, id);
  endfunction
endclass

module class_ex;
  initial begin
    child child_tr;

    child_tr = new();
 

    child_tr.display();
  end
endmodule

```

## Result:
<img width="783" height="308" alt="image" src="https://github.com/user-attachments/assets/0bb0f3bc-ae08-4f6c-9090-421eb5fd38d6" />
