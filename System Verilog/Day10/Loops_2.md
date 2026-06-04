## Behave "for loop" as "while Loop"

```bash
module ex_array;
  int count;
  initial begin
  for(;;)
    begin
      count++;
      $display(count);
      if(count == 10)
        break;
    end
  end
endmodule
```

## Result:
<img width="799" height="427" alt="image" src="https://github.com/user-attachments/assets/60f485db-8af3-4b0f-8e5c-bc66cfb3dc83" />

## Repeat

```bash
module ex_repeat;
  int ex_array[5] = '{100,200,300,400,500};
  int i;

    initial begin
    repeat ($size(ex_array)) begin   // Based on Variable
    $display(i, ex_array[i]);
    i++;
    end
    
    repeat (3)                       // Based on Number
    $display("Welcome here");
    end
endmodule
```
## Result:
<img width="788" height="423" alt="image" src="https://github.com/user-attachments/assets/db3092da-f2d0-42c8-af2f-f9ae427baafb" />

## Clock Generator 10 Mhz and 20 Mhz

```bash
module clk_Gen;
  bit clk_20Mhz = 0;
  bit clk_10Mhz = 0;

  always #50 clk_20Mhz = ~clk_20Mhz;
  always #100 clk_10Mhz = ~clk_10Mhz;

  initial begin
   $monitor("Time=%0t | clk_10Mhz=%0b | clk_20Mhz=%0b",
             $time, clk_10Mhz, clk_20Mhz);
   #500 $finish;
  end
endmodule
```

## Result:

<img width="800" height="421" alt="image" src="https://github.com/user-attachments/assets/f872b268-0fe3-4e5a-b43d-8c65f1a2dfcf" />

## Using Foreach Loop Finding max and min from Fixed array

```bash
module max_min;

  int max, min;
  int ex_array[4] = '{4,6,2,7};

  initial begin

    max = ex_array[0];
    min = ex_array[0];

    foreach(ex_array[i]) begin

      if(ex_array[i] > max)
        max = ex_array[i];

      if(ex_array[i] < min)
        min = ex_array[i];

    end

    $display("max = %0d", max);
    $display("min = %0d", min);

  end

endmodule
```
## Result:

<img width="716" height="300" alt="image" src="https://github.com/user-attachments/assets/2cdd6098-f375-4d18-8195-5369551d138c" />
