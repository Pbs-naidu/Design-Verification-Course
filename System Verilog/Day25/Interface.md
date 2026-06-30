## Verilog Interface 
- Modport
- Clocking Block
- Virtual Interface

&rarr; Interface contains Procedural initial and always block and continuous assign statements.

```bash
//---------------- Half Adder ----------------//
module half_adder(
    input  logic a,
    input  logic b,
    output logic so,
    output logic co
);

    assign so = a ^ b;
    assign co = a & b;

endmodule


//---------------- Interface ----------------//
interface fa_if;
    logic a, b, c;
    logic s_out, c_out;
endinterface


//---------------- Full Adder ----------------//
module full_adder(fa_if inf);

    logic s0, c0, c1;

    half_adder HA1 (
        .a (inf.a),
        .b (inf.b),
        .so(s0),
        .co(c0)
    );

    half_adder HA2 (
        .a (s0),
        .b (inf.c),
        .so(inf.s_out),
        .co(c1)
    );

    assign inf.c_out = c0 | c1;

endmodule


//---------------- Testbench ----------------//
module tb_top;

    fa_if inf();

    full_adder fa(inf);

    initial begin

        inf.a = 1'b1;
        inf.b = 1'b0;
        inf.c = 1'b1;

        #5;
        $display("a=%0b b=%0b cin=%0b --> sum=%0b carry=%0b",
                  inf.a, inf.b, inf.c, inf.s_out, inf.c_out);

        #5 $finish;
    end

endmodule

```

## Result:
<img width="822" height="341" alt="image" src="https://github.com/user-attachments/assets/5c5a18db-7ca0-47f2-a0e0-40e517e68c70" />

## Modport
- Within an Interface to declare port direction for signals.
- Modport puts some restriction.

```bash
//---------------- Interface ----------------//
interface mult_if(input logic clk, reset);

    logic [7:0]  a, b;
    logic [15:0] out;
    logic en;
    logic ack;

    modport TB (
        output a, b, en,
        input  out, ack
    );

    modport RTL (
        input  clk, reset, a, b, en,
        output out, ack
    );

endinterface


//---------------- DUT ----------------//
module multiplier(mult_if.RTL inf);

    always_ff @(posedge inf.clk or posedge inf.reset) begin
        if (inf.reset) begin
            inf.out <= 16'd0;
            inf.ack <= 1'b0;
        end
        else if (inf.en) begin
            inf.out <= inf.a * inf.b;
            inf.ack <= 1'b1;
        end
        else begin
            inf.ack <= 1'b0;
        end
    end

endmodule


//---------------- Testbench ----------------//
module tb_top;

    bit clk;
    bit reset;

    always #2 clk = ~clk;

    initial begin
        clk   = 0;
        reset = 1;
        #2;
        reset = 0;
    end

    mult_if inf(clk, reset);

    multiplier DUT(inf);

    initial begin

        // Test Case 1
        #5;
        inf.TB.a  = 8'd5;
        inf.TB.b  = 8'd6;
        inf.TB.en = 1;

        #10;
        inf.TB.en = 0;

        wait(inf.TB.ack);

        $display("time=%0t a=%0d b=%0d out=%0d",
                 $time, inf.TB.a, inf.TB.b, inf.TB.out);

        // Test Case 2
        #25;
        inf.TB.a  = 8'd20;
        inf.TB.b  = 8'd7;

        #5;
        inf.TB.en = 1;

        #6;
        inf.TB.en = 0;

        wait(inf.TB.ack);

        $display("time=%0t a=%0d b=%0d out=%0d",
                 $time, inf.TB.a, inf.TB.b, inf.TB.out);

        // Test Case 3
        #25;
        inf.TB.a  = 8'd10;
        inf.TB.b  = 8'd4;

        #6;
        inf.TB.en = 1;

        #5;
        inf.TB.en = 0;

        wait(inf.TB.ack);

        $display("time=%0t a=%0d b=%0d out=%0d",
                 $time, inf.TB.a, inf.TB.b, inf.TB.out);

        #10;
        $finish;
    end

    initial begin
        $dumpfile("dump.vcd");
        $dumpvars;
    end

endmodule

```

## Result:
<img width="775" height="322" alt="image" src="https://github.com/user-attachments/assets/fdb78c82-8f86-42c0-8ff3-d1ca62283061" />

## Clocking Block
- To do Synchronization and Timing Requirements for an interface

```bash
//---------------- Interface ----------------//
interface mult_if(input logic clk, reset);

    logic [7:0]  a, b;
    logic [15:0] out;
    logic en;
    logic ack;

    // Clocking Block
    clocking cb @(posedge clk);
        default input #1 output #2;
        input  out, ack;
        output a, b, en;
    endclocking

    // Modports
    modport TB  (clocking cb);
    modport RTL (input clk, reset, a, b, en,
                 output out, ack);

endinterface


//---------------- DUT ----------------//
module multiplier(mult_if.RTL inf);

    always @(posedge inf.clk or posedge inf.reset) begin
        if (inf.reset) begin
            inf.out <= 16'd0;
            inf.ack <= 1'b0;
        end
        else if (inf.en) begin
            inf.out <= inf.a * inf.b;
            inf.ack <= 1'b1;
        end
        else begin
            inf.ack <= 1'b0;
        end
    end

endmodule


//---------------- Testbench ----------------//
module tb_top;

    bit clk;
    bit reset;

    always #2 clk = ~clk;

    initial begin
        clk   = 0;
        reset = 1;
        #2;
        reset = 0;
    end

    mult_if inf(clk, reset);

    multiplier DUT(inf);

    initial begin

        // Test 1
        #5;
        inf.cb.a  <= 8'd5;
        inf.cb.b  <= 8'd6;
        inf.cb.en <= 1'b1;

        #10;
        inf.cb.en <= 1'b0;

        wait(inf.cb.ack);

        $display("time=%0t a=%0d b=%0d out=%0d",
                 $time, inf.cb.a, inf.cb.b, inf.cb.out);

        // Test 2
        #25;
        inf.cb.a  <= 8'd20;
        inf.cb.b  <= 8'd7;

        #5;
        inf.cb.en <= 1'b1;

        #6;
        inf.cb.en <= 1'b0;

        wait(inf.cb.ack);

        $display("time=%0t a=%0d b=%0d out=%0d",
                 $time, inf.cb.a, inf.cb.b, inf.cb.out);

        // Test 3
        #25;
        inf.cb.a  <= 8'd10;
        inf.cb.b  <= 8'd4;

        #6;
        inf.cb.en <= 1'b1;

        #5;
        inf.cb.en <= 1'b0;

        wait(inf.cb.ack);

        $display("time=%0t a=%0d b=%0d out=%0d",
                 $time, inf.cb.a, inf.cb.b, inf.cb.out);

        #10;
        $finish;
    end
endmodule
```

## Result:
<img width="775" height="322" alt="image" src="https://github.com/user-attachments/assets/fdb78c82-8f86-42c0-8ff3-d1ca62283061" />

## Virtual Interface
- Represents Signals that are used to connect design modules or Testbench to DUT .
- To Bridge Gap Between World of Static Modules and Dynamic Objects.

