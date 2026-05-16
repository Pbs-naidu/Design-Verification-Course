## Print 2 dimensional Array
```bash
module mul_array();
 int ex_array [6][2] = '{{1,100},{2,200},{3,300},{4,400},{5,500},{6,600}};
 int i,j;
  initial begin
    for(i=0;i<6;i=i+1)
      begin
        for(j=0;j<2;j=j+1)
          	begin
              $display("ex_array[%0d][%0d] : %0d",i,j,ex_array[i][j]); 
            end
    end

````
## Results:
<img width="782" height="415" alt="image" src="https://github.com/user-attachments/assets/eaff5fc9-52f2-4801-8953-2e981606efe3" />
