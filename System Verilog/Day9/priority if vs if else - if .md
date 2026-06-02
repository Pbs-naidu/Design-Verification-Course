
<img width="916" height="202" alt="image" src="https://github.com/user-attachments/assets/4bc67f2d-b20a-4400-9989-e84840c0eed8" />

## Priority if
```bash
module priority_if;

initial begin
    int a, b;

    a = 20;
    b = 10;

 priority if (a < b)
        $display("a is greater than b");
  else if (b < 0)
        $display("a is less than b");
  //  else
   //     $display("a is equal to b");
end

endmodule
```
## Result:
<img width="1095" height="331" alt="image" src="https://github.com/user-attachments/assets/b5239134-144d-4a18-9e94-95031d5991b5" />

## if else
```bash
module if_else;

initial begin
    int a, b;

    a = 20;
    b = 10;

  if (a < b)
        $display("a is greater than b");
  else if (b < 0)
        $display("a is less than b");
  //  else
   //     $display("a is equal to b");
end

endmodule
```

## Result:
<img width="968" height="328" alt="image" src="https://github.com/user-attachments/assets/49fbc83f-109e-488a-a1b2-e6356c9a1315" />

## Unique if
```bash
module unique_if;

initial begin
    int a, b;

    a = 20;
    b = 10;

  unique if (a > b)
        $display("a is greater than b");
  else if (b > 0)
        $display("a is less than b");
end
endmodule
```

## Result:
<img width="1059" height="326" alt="image" src="https://github.com/user-attachments/assets/5e52af7f-7fee-46b6-bb69-67535b08a5cf" />

## Print Dynamic Array using while loop
```bash
module dynamic_array_demo;
  int arr[];
  int count;

  initial begin
    arr = new[5];
    arr = '{10, 20, 30, 40, 50};
    count = 0;
    while (count < arr.size()) begin
      $display("arr[%0d] = %0d", count, arr[count]);
      count++;
    end
  end
endmodule
```
## Result:
<img width="759" height="327" alt="image" src="https://github.com/user-attachments/assets/843332cf-a8b7-479c-a89f-d8a733108a75" />
