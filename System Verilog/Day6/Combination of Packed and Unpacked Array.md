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

## Dynamic Array
```bash
module dynamic_array_example;
  int array [];
  initial begin
    array = new[5];
    array = '{5, 10, 15, 20, 25};
    
    // Print elements of an array
    foreach (array[i]) $display("array[%0d] = %0d", i, array[i]);
    
    // size of an array
    $display("size of array = %0d", array.size());
    
    // Resizing of an array and copy old array content
    array = new[8] (array);
    $display("size of array after resizing = %0d", array.size());
    
    // Print elements of an array
    foreach (array[i]) $display("array[%0d] = %0d", i, array[i]);
    
    // Override existing array: Previous array elememt values will be lost
    array = new[6];
    $display("size of array after overriding = %0d", array.size());
    
    // Print elements of an array
    foreach (array[i]) $display("array[%0d] = %0d", i, array[i]);
    
    array.delete();
    $display("size of array after deleting = %0d", array.size());
    
  end
endmodule

```
## Result:
<img width="754" height="675" alt="image" src="https://github.com/user-attachments/assets/a9f2fccd-1999-491f-afc6-eb987984167a" />

## Square of Number using Dynamic Array
```bash
module dynamic_array;
  int d_array[];
  initial begin
    d_array = new[5];
    d_array='{1,2,3,4,5};
    foreach(d_array[i]) begin
      d_array[i] = d_array[i]*d_array[i];
      $display("d_array[%0d] = %0d", i, d_array[i]);
    end
  end
endmodule
```
## Result:
<img width="803" height="353" alt="image" src="https://github.com/user-attachments/assets/8c756f04-efe9-474f-8d90-1196c55db9d1" />

## Duplicate Element Count Using Associative Array
```bash
module dup_array;
  int duplicate_count = 0;
  int ex_array[] = '{101,205,333,101,777,205,999,333,333};
  int dup[int];

  initial begin
    foreach(ex_array[i]) begin

      if(dup.exists(ex_array[i])) begin
        $display("Duplicate %0d found at index %0d",
                  ex_array[i], i);
        duplicate_count++;
      end
        dup[ex_array[i]]++;
    end
    $display("Total duplicates = %0d", duplicate_count);
 end
endmodule
```
## Result:
<img width="977" height="447" alt="image" src="https://github.com/user-attachments/assets/34bf5b7f-7789-4099-a929-384b5bfcf89a" />

