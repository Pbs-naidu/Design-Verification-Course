## Inline Constraint
&rarr; Inline Constraint don't overide constraint in another class. <br>
&rarr; When you solve the constraint will be considering both constraint.

```bash
class seq_item;

  rand bit [7:0] val1, val2;

  // Original constraints
  constraint val1_c { val1 > 10; val1 < 100; }
  constraint val2_c { val2 > 5;  val2 < 80; }

endclass


module tb;

  seq_item item;
  bit success;

  initial begin

    item = new();

    //=====================================================
    // Case 1 : Normal randomization (Success)
    //=====================================================
    success = item.randomize();

    if(success)
      $display("CASE1 SUCCESS : val1=%0d val2=%0d", item.val1, item.val2);
    else
      $display("CASE1 FAILED");



    //=====================================================
    // Case 2 : Compatible inline constraint (Success)
    //=====================================================
    success = item.randomize() with {
      val1 > 50;
      val1 < 70;
    };

    if(success)
      $display("CASE2 SUCCESS : val1=%0d val2=%0d", item.val1, item.val2);
    else
      $display("CASE2 FAILED");



    //=====================================================
    // Save old value
    //=====================================================
    $display("\nBefore failed randomization:");
    $display("val1=%0d val2=%0d", item.val1, item.val2);



    //=====================================================
    // Case 3 : Conflicting inline constraint (FAIL)
    //=====================================================
    success = item.randomize() with {
      val1 > 150;
    };

    if(success)
      $display("CASE3 SUCCESS : val1=%0d val2=%0d", item.val1, item.val2);
    else
      $display("CASE3 FAILED");



    //=====================================================
    // Values remain unchanged
    //=====================================================
    $display("\nAfter failed randomization:");
    $display("val1=%0d val2=%0d", item.val1, item.val2);

  end

endmodule
```

## Result:
<img width="1110" height="431" alt="image" src="https://github.com/user-attachments/assets/b38263e9-71e9-4dc3-ae38-185f13078740" />

## Soft Constraint
&rarr; if there is an requirement to change the contraint in such a way it may conflict with constraint in the class.

```bash
class seq_item;

  rand bit [7:0] val1;

  // Soft constraint
  constraint val1_c {
    soft val1 inside {[10:15]};
  }

endclass


module example;

  seq_item item;

  initial begin

    item = new();

    repeat (5) begin

      if (item.randomize() with { val1 inside {[20:30]}; })
        $display("val1 = %0d", item.val1);
      else
        $display("Randomization Failed");

    end

  end

endmodule
```
## Result:
<img width="592" height="327" alt="image" src="https://github.com/user-attachments/assets/0cfa89c4-a2fd-4fed-a4ae-b13b00e8809e" />

## Randomization Methods

 **pre_randomize()**
 
&rarr; It is used to do an activity before randomization. <br>
&rarr; It can be used to disable constraints for a particular variable. <br>

**Common methods used:**
&rarr; rand_mode() <br>
&rarr; constraint_mode() <br>

**post_randomize()**

&rarr; It is used to do an activity after randomization. <br>
&rarr; We can perform operations on the randomized class variables (for example, compute derived values, display results, or update non-rand variables). <br>

```bash
class seq_item;

  rand bit [7:0] val1, val2;

  // Constraints
  constraint val1_c {
    val1 > 100;
    val1 < 200;
  }

  constraint val2_c {
    val2 > 5;
    val2 < 80;
  }

  // Called before randomization
  function void pre_randomize();
    // Disable val2 constraint
    val2_c.constraint_mode(0);
    $display("Inside pre_randomize()");
  endfunction

  // Called after successful randomization
  function void post_randomize();
    $display("Inside post_randomize()");
    $display("val1 = %0d, val2 = %0d", val1, val2);
  endfunction

endclass


module example;

  seq_item item;

  initial begin

    item = new();

    repeat (3) begin
      if (item.randomize())
        $display("Randomization Successful\n");
      else
        $display("Randomization Failed\n");
    end

  end

endmodule

```
## Result:
<img width="757" height="492" alt="image" src="https://github.com/user-attachments/assets/bee4ccc5-8241-4b93-badb-3af2b4799eb2" />

## randcase
&rarr; randcase is an case statement, that randomly selects one
of its branch statement based on probability of each statement <br>
&rarr; randcase is also written inside an module

```bash
class seq_item;

  int cnt_arr[int];   // Associative array
  real i_sum;

  function void randcase_testing();

    repeat (10) begin
      randcase
        2 : begin
              $display("Selected 2");
              cnt_arr[2]++;
            end

        3 : begin
              $display("Selected 3");
              cnt_arr[3]++;
            end

        5 : begin
              $display("Selected 5");
              cnt_arr[5]++;
            end

        7 : begin
              $display("Selected 7");
              cnt_arr[7]++;
            end
      endcase
    end

    // Sum of all weights
    foreach (cnt_arr[i]) begin
      i_sum += i;
    end

    // Display probability
    foreach (cnt_arr[i]) begin
      $display("Weight for %0d = %0f", i, i/i_sum);
      $display("cnt_arr[%0d] = %0d", i, cnt_arr[i]);
      $display("Observed Probability for cnt_arr[%0d] = %0f",
               i, cnt_arr[i]/10.0);
      $display("--------------------------------");
    end

  endfunction

endclass


module example;

  seq_item item;

  initial begin
    item = new();
    item.randcase_testing();
  end

endmodule
```

## Result:
<img width="820" height="747" alt="image" src="https://github.com/user-attachments/assets/68e73631-d658-4c3f-a2e0-4e1b9cafaa86" />
