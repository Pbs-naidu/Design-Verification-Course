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

## Array of Objects
## Fixed Array

```bash
class ex_fixed;
    bit [31:0] data;
    int id;
endclass

module example;

    ex_fixed tr[5];

    initial begin
      
        foreach (tr[i]) begin
          	tr[i] = new();
            tr[i].data = i * i;
            tr[i].id   = i + 1;
        end

        foreach (tr[i])
            $display("data=%0d id=%0d", tr[i].data, tr[i].id);

    end

endmodule
```

## Result:
<img width="796" height="332" alt="image" src="https://github.com/user-attachments/assets/9ad848b0-135c-46fa-8f34-1ca8f2b5aa78" />

## Dynamic Array

```bash
class ex_dynamic;
    bit [31:0] data;
    int id;
endclass

module example;

    ex_dynamic tr[];
  	
    initial begin
      tr=new[6];
        foreach (tr[i]) begin
          	tr[i] = new();
            tr[i].data = i * i;
            tr[i].id   = i + 1;
        end

        foreach (tr[i])
            $display("data=%0d id=%0d", tr[i].data, tr[i].id);

    end

endmodule

```

## Result:
<img width="802" height="335" alt="image" src="https://github.com/user-attachments/assets/0874d792-8a8b-46a0-80d3-a9aea899dd74" />
