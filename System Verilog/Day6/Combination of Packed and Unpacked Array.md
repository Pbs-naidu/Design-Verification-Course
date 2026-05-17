## Printing only first row elements
```bash
module array;
  int ex_array [2:0][3:0]='{'{1,2,3,4},'{5,6,7,8},'{9,10,11,12}};
  initial begin 
    foreach(ex_array[2][j])
      $display("Elements of ex_array[2][%0d] : %0d",j,ex_array[2][j]); 
  end  
endmodule
```
## Results:
<img width="832" height="328" alt="image" src="https://github.com/user-attachments/assets/7510f618-fd46-48b6-bc39-27d43203cdbf" />
