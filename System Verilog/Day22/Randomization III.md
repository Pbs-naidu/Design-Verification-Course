## Bidirectional Constraint
&rarr; Solve Constraints parallely for all random variables & make sure that no constraint fails.

```bash
class seq_item;

  rand bit [7:0] val1, val2, val3, val4;
  rand bit       t1, t2;

  constraint val_c {
    val2 > val1;
    val3 == (val2 - val1);

    val3 != 0;          // avoid divide-by-zero
    val4 < val3;

    val4 == (val1 / val3);
  }

  constraint imp_c {
    (t1 == 1) -> (t2 == 0);
  }

endclass


module constraint_ex;

  seq_item item;

  initial begin
    item = new();

    repeat (3) begin
      if (item.randomize()) begin
        $display("val1=%0d val2=%0d val3=%0d val4=%0d t1=%0b t2=%0b",
                 item.val1,
                 item.val2,
                 item.val3,
                 item.val4,
                 item.t1,
                 item.t2);
      end
      else
        $display("Randomization Failed");
    end
  end

endmodule
```

## Result:
<img width="852" height="332" alt="image" src="https://github.com/user-attachments/assets/e7628880-8057-421f-8689-f9f26451d282" />

## Solve Before
&rarr;By Default Constraint has an equal probability to solve any constraint
1. Randc is not allowed
2. only integers are allowed

```bash
class seq_item;

  rand bit [7:0] val;
  rand bit       en;

  constraint en_c {
    solve en before val;

    if (en == 1)
      val inside {[0:100]};
  }

endclass


module constraint_ex;

  seq_item item;

  initial begin
    item = new();

    repeat (10) begin
      if (item.randomize()) begin
        $display("en=%0b val=%0d", item.en, item.val);
      end
    end
  end

endmodule
```
## Result:
<img width="966" height="457" alt="image" src="https://github.com/user-attachments/assets/8517ac1d-95c3-4278-99d1-7320e1897d0a" />


