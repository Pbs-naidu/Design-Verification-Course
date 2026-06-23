## if else
```bash

class seq_item;
  rand bit [7:0] value;
  rand enum {LOW, HIGH} scale;

  constraint scale_c { if(scale == LOW) value < 50;
                       else value >= 50;
                     }
endclass

module constraint_example;
  seq_item item;
  
  initial begin
    item = new();
    
    repeat(5) begin
      item.randomize();
      $display("scale = %s, value = %0d", item.scale.name(), item.value);
    end
  end
endmodule

```

## Result:
<img width="656" height="325" alt="image" src="https://github.com/user-attachments/assets/063a5772-8347-4808-9665-d2f07000cc0f" />

## if-else-if

```bash

class seq_item;
  rand bit [7:0] value;
  rand enum {LOW,MEDIUM, HIGH} scale;

  constraint scale_c { if(scale == LOW) value < 50;
                      else if(scale == HIGH) value >= 50;
                      else value==50;
                     }
endclass

module constraint_example;
  seq_item item;
  
  initial begin
    item = new();
    
    repeat(5) begin
      item.randomize();
      $display("scale = %s, value = %0d", item.scale.name(), item.value);
    end
  end
endmodule
```

## Result:
<img width="818" height="332" alt="image" src="https://github.com/user-attachments/assets/f8bdf767-8638-4e5a-bab3-15778f3beda6" />

## Implication Operator Constraint **(->)**

```bash

class seq_item;
  rand bit [7:0] value;
  rand enum {LOW,HIGH} scale;

  constraint scale_c { (scale == LOW)->value < 50;
                     
                     }
endclass

module constraint_example;
  seq_item item;
  
  initial begin
    item = new();
    
    repeat(5) begin
      item.randomize();
      $display("scale = %s, value = %0d", item.scale.name(), item.value);
    end
  end
endmodule
```

## Result:
<img width="772" height="331" alt="image" src="https://github.com/user-attachments/assets/f39f9bc8-4550-418c-9c76-5e6e32d801a0" />

## for-each Constraint

```bash
// foreach loop in constraint

typedef enum {LOW, HIGH} scale;

class seq_items;

  rand bit [7:0] value_a[scale];
  rand bit [3:0] array[];

  function new();
    value_a[LOW]  = 0;
    value_a[HIGH] = 0;
  endfunction

  // Dynamic array size between 2 and 5
  constraint example {
    array.size inside {[2:5]};
  }

  // Array elements must be greater than index
  constraint example_c {
    foreach (array[i])
      array[i] > i;
  }

  // Constraints on associative array elements
  constraint example_c1 {
    foreach (value_a[i]) {
      value_a[i] < 100;

      (i == LOW)  -> value_a[i] < 30;
      (i == HIGH) -> value_a[i] inside {[30:50]};
    }
  }

endclass


module constraint_ex;

  seq_items item;

  initial begin
    item = new();

    repeat (5) begin
      item.randomize();

      $display("---------------------------");
      $display("LOW  = %0d", item.value_a[LOW]);
      $display("HIGH = %0d", item.value_a[HIGH]);

      foreach (item.array[i])
        $display("array[%0d] = %0d", i, item.array[i]);
    end
  end

endmodule
```

## Result:
<img width="713" height="735" alt="image" src="https://github.com/user-attachments/assets/aec9050e-872c-4a86-b538-12901aebce8c" />

## Dist keyword
&rarr; Probability of Random Value Occurance can be Controlled using **Dist** Keyword. <br>
&rarr; Using :/,:= Operator

```bash
class seq_item;
  rand bit [7:0] value1;
  rand bit [7:0] value2;

  constraint value1_c {value1 dist {3:/4, [5:8] :/ 7}; }
  constraint value2_c {value2 dist {3:=4, [5:8] := 7}; }

endclass

module constraint_example;
  seq_item item;
  
  initial begin
    item = new();
    
    repeat(5) begin
      item.randomize();
      $display("value1 (with :/) = %0d, value2 (with :=)= %0d", item.value1, item.value2);
    end
  end
endmodule
```

## Result:
<img width="731" height="251" alt="image" src="https://github.com/user-attachments/assets/7cdb3fbc-f123-49e4-86ad-ce9e4d14343e" />

## Disable Randomization & Disable Constraint
**rand_mode()** function
- If randomization is enabled → solver randomizes the variable → returns 1 <br>
- If randomization is disabled → variable is not randomized → returns 0 <br>

**constraint_mode()** function
- If constraint is enabled →  it solves  → returns 1 <br>
- If constraint is disabled → returns 0

```bash
class seq_item;

  rand bit [7:0] value1;
  rand bit [7:0] value2;

  constraint value1_c {
    value1 inside {[10:30]};
  }

  constraint value2_c {
    value2 inside {40,70,80};
  }

endclass


module tb;

  seq_item item;

  initial begin

    item = new();

    //---------------------------------------------------
    // CASE 1 : Normal Randomization
    //---------------------------------------------------
    $display("\nCASE 1 : Normal Randomization");

    repeat(5) begin
      item.randomize();
      $display("value1=%0d value2=%0d",
                item.value1,item.value2);
    end

    //---------------------------------------------------
    // CASE 2 : rand_mode(0)
    //---------------------------------------------------
    $display("\nCASE 2 : value2.rand_mode(0)");

    item.randomize(); // generate initial value

    item.value2.rand_mode(0);

    repeat(5) begin
      item.randomize();
      $display("value1=%0d value2=%0d",
                item.value1,item.value2);
    end

    //---------------------------------------------------
    // Re-enable randomization
    //---------------------------------------------------
    item.value2.rand_mode(1);

    //---------------------------------------------------
    // CASE 3 : constraint_mode(0)
    //---------------------------------------------------
    $display("\nCASE 3 : value2_c.constraint_mode(0)");

    item.value2_c.constraint_mode(0);

    repeat(5) begin
      item.randomize();
      $display("value1=%0d value2=%0d",
                item.value1,item.value2);
    end

  end

endmodule
```
## Result:
<img width="817" height="617" alt="image" src="https://github.com/user-attachments/assets/bff6a926-ea57-4df4-a206-6310ac965217" />
