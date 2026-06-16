Q)  Create a class named Book with Title and Price as its properties. Write a SystemVerilog program to 
    create and initialize an array of three book objects, assign appropriate titles and prices to each book, 
    and then display only those books whose price is greater than 1000.

```bash
class book;
  bit [10:0] price;
  string Title;
  
endclass

module ex;
  
  book b [2:0];
  
  initial begin  
    b[0]=new();
    b[1]=new();
    b[2]=new();
    
    b[0].price = 1200;
    b[1].price = 900;
    b[2].price = 1001;
    
    b[0].Title = " DV Verification ";
    b[1].Title = " RTL Design ";
    b[2].Title = " Physical Design ";

    foreach(b[i])
      if (b[i].price > 1000)
        $display(b[i].Title,"is more than 1000 Ruppes");
    else
      $display(b[i].Title,"is Less than 1000 Ruppes");
  end
endmodule
```

## Result:
<img width="952" height="333" alt="image" src="https://github.com/user-attachments/assets/69459cc1-ed5a-4103-8165-b54293444cc1" />
