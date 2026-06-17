## Static vs Non-Static

```bash
class transaction;

  static int s_id;
  int id;

  function new();
    s_id++;
    id++;
  endfunction

endclass

module class_ex;

  transaction tr[5];

  initial begin

    foreach (tr[i]) begin
      tr[i] = new();
      $display(tr[i].s_id, tr[i].id);

    end

  end

endmodule
```

## Result:
<img width="808" height="328" alt="image" src="https://github.com/user-attachments/assets/b293f672-35c8-44d6-94da-02d8191f4b3c" />

## "this" keyword usage

### 1.Without this keyword
```bash
class transaction;

  bit [31:0] data;
  int id;

  function new(bit [31:0] data, int id);
    data = data;
    id   = id;
  endfunction

endclass


module ex;

  transaction tr;

  initial begin
    tr = new(10, 1);
    $display("data = %0d, id = %0d", tr.data, tr.id);
  end

endmodule
```
## Result:
<img width="840" height="330" alt="image" src="https://github.com/user-attachments/assets/14f4de52-02dd-4820-a36e-13f96ef232c5" />

### 2.with "this" Keyword

```bash
class transaction;

  bit [31:0] data;
  int id;

  function new(bit [31:0] data, int id);
   this. data = data;
   this. id   = id;
  endfunction

endclass


module ex;

  transaction tr;

  initial begin
    tr = new(10, 1);
    $display("data = %0d, id = %0d", tr.data, tr.id);
  end

endmodule

```

## Result:
<img width="870" height="333" alt="image" src="https://github.com/user-attachments/assets/45e44503-711e-4f05-a0fb-7766718a2482" />
