##  sum of all elements in the array

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

## Results:
<img width="789" height="543" alt="image" src="https://github.com/user-attachments/assets/4a272eef-2a97-4d8e-af89-07554dbb1933" />


