## insert, Delete, Push, Pop with queue

```bash
module SV_queue();
  
int elements[$];
int removed;
  
initial begin

elements = '{1,5,11,17,21};
foreach(elements[i]) $display("elements[%0d] = %d", i, elements[i]);

elements.insert(2,777) ;
foreach(elements[i]) $display("elements[%0d] = %d", i, elements[i]);

elements.delete(4);
foreach(elements[i]) $display("elements[%0d] = %d", i, elements[i]);

elements.push_front(888);
foreach(elements[i]) $display("elements[%0d] = %d", i, elements[i]);

removed = elements.pop_back();
$display("Removed = %0d", removed);
foreach(elements[i])
$display("elements[%0d] = %0d", i, elements[i]);

removed = elements.pop_front();
$display("Removed = %0d", removed);
foreach(elements[i])
$display("elements[%0d] = %0d", i, elements[i]);
    
 end 
endmodule
```

## Results:
<img width="766" height="741" alt="image" src="https://github.com/user-attachments/assets/96b86062-d3f9-436c-8cff-b3794cd23ff2" />
<img width="743" height="192" alt="image" src="https://github.com/user-attachments/assets/efffc6d9-3ff5-4d5a-9768-ab17b6153af5" />
