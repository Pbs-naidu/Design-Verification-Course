## Agent:
```bash
class agent;

  driver    drv;
  monitor   mon;
  generator gen;

  mailbox gen_to_drv;
  virtual add_if vif;

  function new(virtual add_if vif, mailbox mon_to_sb);

    gen_to_drv = new();

    drv = new(gen_to_drv, vif);
    mon = new(mon_to_sb, vif);
    gen = new(gen_to_drv);

  endfunction

  task run();

    fork
      drv.run();
      mon.run();
      gen.run();
    join_any

  endtask

endclass
```

## Scoreboard:

```bash
class scoreboard;

  int compare_cnt;
  mailbox mon_to_sb;

  function new(mailbox mon_to_sb);
    this.mon_to_sb = mon_to_sb;
  endfunction

  task run();

    forever begin

      transaction tr;
      tr = new();

      mon_to_sb.get(tr);

      if (tr.ip1 + tr.ip2 == tr.out) begin
        $display("Matched");
      end
      else begin
        $display("Not Matched");
      end

      compare_cnt++;

    end

  endtask

endclass
```
## Environment:
```bash

class env;

  agent      agt;
  scoreboard sb;

  mailbox mon_to_sb;

  function new(virtual add_if vif);

    mon_to_sb = new();

    agt = new(vif, mon_to_sb);
    sb  = new(mon_to_sb);

  endfunction

  task run();

    fork
      agt.run();
      sb.run();
    join_any

    wait (agt.gen.count == sb.compare_cnt);

    $finish;

  endtask

endclass

```

## Test:
```bash
program base_test(add_if vif);

  env env_o;

  initial begin

    env_o = new(vif);

    // Number of transactions to generate
    env_o.agt.gen.count = 5;

    // Start the environment
    env_o.run();

  end

endprogram
```

## Testbench Top
```bash
module tb_top;

  bit clk;
  bit reset;

  // Clock Generation
  always #2 clk = ~clk;

  // Interface Instantiation
  add_if vif(clk, reset);

  // DUT Instantiation
  adder DUT (
    .clk   (vif.clk),
    .reset (vif.reset),
    .in1   (vif.ip1),
    .in2   (vif.ip2),
    .out   (vif.out)
  );

  // Test Instantiation
  base_test t1(vif);

  // Reset Generation
  initial begin
    clk   = 0;
    reset = 1;

    #5;
    reset = 0;
  end

endmodule
```
