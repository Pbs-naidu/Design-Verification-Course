## Function
```bash
module ex_function;

  function compare(input int a, b);
    if (a > b)
      $display("a is greater than b");
    else if (a < b)
      $display("a is less than b");
    else
      $display("a is equal to b");
  endfunction

  initial begin
    compare(10, 5);
    compare(5, 9);
    compare(6, 6);
  end

endmodule
```

## Result:
<img width="796" height="333" alt="image" src="https://github.com/user-attachments/assets/1f9ce035-ed28-4bc3-b5ba-b458c619a5cb" />

