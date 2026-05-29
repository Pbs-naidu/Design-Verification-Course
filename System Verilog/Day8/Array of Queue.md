## without using Array index
```bash
module array_example;

  int array[3][$];

  initial begin
    //array[0] = {2, 4, 6, 8};
    //array[1] = {1, 3, 5, 7};
    //array[2] = {100, 200, 300};

    //or
    array = '{
              {2, 4, 6, 8},
              {1, 3, 5, 7},
              {100, 200, 300}
            };

    // Print array of queues
    foreach (array[i,j])
      $display("array[%0d][%0d] = %0d", i, j, array[i][j]);

    // Print all of your array
    $display("----------------");

    array[0].push_back(10);
    array[1].push_back(9);
    array[2].push_back(400);

    $display("After push_back operation");

    // Print array of queues
    foreach (array[i,j])
      $display("array[%0d][%0d] = %0d", i, j, array[i][j]);

  end

endmodule
```

## Result:
<img width="727" height="751" alt="image" src="https://github.com/user-attachments/assets/a4cd6df4-0aa1-4179-be5b-e92c58c4be53" />
