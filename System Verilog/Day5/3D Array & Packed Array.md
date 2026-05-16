##  Sum of all elements in the array

```bash
module three_D;
 int i,j,k;
int sum =0;
  int ex_array[1][3][3] = '{
                              '{
                                 '{1,11,111},
                                 '{2,22,222},
                                 '{3,33,333}
                               }
                            };

   initial begin 
     foreach (ex_array[i,j,k])begin
       
         sum = sum+ex_array[i][j][k];
       
         $display("ex_array[%0d][%0d][%0d] = %0d",
                  i,j,k,ex_array[i][j][k]);
     
     $display("total sum = %0d",sum);
     end
    
   end

endmodule

````

## Result:
<img width="789" height="543" alt="image" src="https://github.com/user-attachments/assets/4a272eef-2a97-4d8e-af89-07554dbb1933" />

## Print the Packed Array

```bash
module packed_array();

 bit [2:0][3:0] ex_array = '{4'h2,4'h6,4'h5};

  initial begin
  foreach (ex_array[i,j])
    
 $display("ex_array [%0d][%0d]=%0d",i,j,ex_array[i][j]);
    
 foreach (ex_array[i])

 $display("ex_array [%0d]=%0d",i,ex_array[i]);
    
  end
endmodule
```
## Result:
<img width="758" height="487" alt="image" src="https://github.com/user-attachments/assets/1bd4f5fd-e610-4868-a90b-9225668d5625" />

