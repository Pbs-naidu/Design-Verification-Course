## Class Assignment

```bash
class sandbox;
    bit [31:0] silicon;
endclass

module ex;

    sandbox data1, data2;

    initial begin
        data1 = new();

        data1.silicon = 5;
        data2 = data1;

        $display(data1.silicon, data2.silicon); 

        data2.silicon = 10;

        $display(data1.silicon, data2.silicon);
    end

endmodule
```

## Result:
<img width="938" height="337" alt="image" src="https://github.com/user-attachments/assets/99d64256-cc71-4350-a666-77f42d654b5b" />
