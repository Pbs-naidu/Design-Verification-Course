##  - Print an array elements from 100 to 500 with each space differnce of 100.

```bash
module elements();
int i;
int arr[5]='{100,200,300,400,500};
initial begin
  foreach(arr[i])
  $display("Element array[%0d] is : %0d",i,arr[i]);
end
endmodule
```
## Results
<img width="792" height="340" alt="image" src="https://github.com/user-attachments/assets/2dadcf99-baee-4470-a656-7e0947631c38" />
