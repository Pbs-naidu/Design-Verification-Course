## Call by value
```bash
module ex_func;

  int a,b;
  int out;

  function int ex_mul (int a=5, b=6);
    a = a*b;   // updates local copy of a
    return a;
  endfunction

  initial begin
    out = ex_mul(a,b);
    $display("out=%0d a=%0d b=%0d", out, a, b);

    a = 2;
    b = 4;

    out = ex_mul(a,b);
    $display("out=%0d a=%0d b=%0d", out, a, b);
  end

endmodule
```

## Result:
<img width="996" height="309" alt="image" src="https://github.com/user-attachments/assets/fcd4923d-f16a-4ad2-8839-aba8adb70742" />

## Call by name

```bash
module ex_func_name;

  function void ex_name(string name, int val);
    $display("name=%s val=%0d", name, val);
  endfunction

  initial begin
    ex_name(.val(100), .name("Silicon"));
  end

endmodule

```

## Result:
<img width="968" height="308" alt="image" src="https://github.com/user-attachments/assets/61a48510-362a-4e80-87fb-f1586b11a404" />

## Call by Reference

```bash
module ex_func_ref;

  int a, b;
  int out;

  function automatic int ex_mul(ref int a, b);
    a = a * b;
    return a;
  endfunction

  initial begin
    a = 5;
    b = 6;

    out = ex_mul(a, b);

    $display("out=%0d a=%0d b=%0d", out, a, b);
  end

endmodule

```
## Result:
<img width="984" height="308" alt="image" src="https://github.com/user-attachments/assets/e7e8e4ce-554e-4a07-b63b-c02d4e2fe6da" />
