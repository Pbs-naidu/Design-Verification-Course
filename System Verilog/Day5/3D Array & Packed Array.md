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

##  3 Dimentional array such that --> Size = 3X3X3 with all 10's
```bash
module three_D;
  int ex_array[3][3][3] = '{
                              '{
                                '{10,10,10},
                                '{10,10,10},
                                '{10,10,10}
                              },
    
                             '{
                               '{10,10,10},
                                '{10,10,10},
                                '{10,10,10}
                             },
    
                             '{
                             '{10,10,10},
                                '{10,10,10},
                               '{10,10,10}
                             }
                            };

   initial begin 
     foreach (ex_array[i,j,k])begin
         $display("ex_array[%0d][%0d][%0d] = %0d",
                  i,j,k,ex_array[i][j][k]);
     end
   end
endmodule

```
## Result:
<img width="761" height="742" alt="image" src="https://github.com/user-attachments/assets/e0441cb4-0b3b-4bc2-93f7-2d48147febb5" />




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


## Packed Array with bit [1:0][3:0][7:0] pkt --> Store an random Elements & Display it

```bash
module packed_array();
  
  bit [1:0][3:0][7:0] pkt = '{'{$urandom,$urandom,$urandom,$urandom},
                              '{$urandom,$urandom,$urandom,$urandom}
                             };
  initial begin
    foreach (pkt[i,j,k])
    
      $display("pkt [%0d][%0d][%0d]=%0d",i,j,k,pkt[i][j][k]);
    
    foreach (pkt[i])
      $display("pkt [%0d]=%0d",i,pkt[i]);
    
    foreach (pkt[i,j])
      $display("pkt [%0d][%0d]=%0d",i,j,pkt[i][j]);
    
    foreach (pkt[j,k])
      $display("pkt [%0d][%0d]=%0d",j,k,pkt[j][k]);
  end
endmodule
```

## Result:

<img width="691" height="752" alt="image" src="https://github.com/user-attachments/assets/efc66fab-9c7e-4fcd-96af-4ec701a0508a" />

<img width="547" height="738" alt="image" src="https://github.com/user-attachments/assets/86df3621-9327-4754-9b2e-f928e807490c" />

<img width="746" height="741" alt="image" src="https://github.com/user-attachments/assets/acfcf328-d5b1-4a26-bb4b-5b205cb36871" />



