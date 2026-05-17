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
## Combination of Packed Array & UnPacked Array
```bash
module array;
  bit [4:0] ex_array [2:0][1:0]='{'{1,2},'{3,4},'{5,6}};
  initial begin   
    foreach(ex_array[i,j])
      $display("Elements of ex_array[%0d][%0d] : %0d",i,j,ex_array[i][j]);  
  end
endmodule
```
## Results:
<img width="567" height="335" alt="image" src="https://github.com/user-attachments/assets/4651ea60-dff4-406a-b1d1-ccfd246aca6a" />
