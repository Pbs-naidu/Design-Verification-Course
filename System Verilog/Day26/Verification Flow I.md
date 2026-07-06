## Verification Flow 
1. Generate input stimulus
2. Driving an input stimulus
3. Monitor an Design Activity at O/P and I/P
4. Compare output Transaction correctness based on I/P
5. Sampling an Coverage and assertions.

## SV Testbench Architecture
<img width="913" height="435" alt="image" src="https://github.com/user-attachments/assets/bbbd3a16-b538-466d-91a9-9f320a05e418" />

## Agents : Container that Holds Generator, Driver, Monitor.
## 1. Transaction:
- Class that Holds an Structure which talks with DUT
```bash
class transaction;

  rand bit [7:0] ip1, ip2;
  bit  [8:0] out;

  constraint ip_c {
    ip1 < 100;
    ip2 < 100;
  }

endclass
```
## 2. Generator:
- Generates or creates Randomized Transaction to Pass to Driver.
```bash
class generator;

  int count;
  mailbox gen_to_drv;
  transaction tr;

  function new(mailbox gen_to_drv);
    this.gen_to_drv = gen_to_drv;
  endfunction

  task run();

    repeat(count) begin

      tr = new();

      if(!tr.randomize())
        $display("Randomization Failed");

      gen_to_drv.put(tr);

      $display("[GEN] ip1=%0d ip2=%0d",
               tr.ip1, tr.ip2);

    end

  endtask

endclass
```

## 3.Driver:
- Receives Randomized Transaction from Generator.
```bash
class driver;

  virtual add_if vif;
  mailbox gen_to_drv;
  transaction tr;

  function new(mailbox gen_to_drv,
               virtual add_if vif);

    this.gen_to_drv = gen_to_drv;
    this.vif = vif;

  endfunction

  task run();

    forever begin

      tr = new();

      gen_to_drv.get(tr);

      @(posedge vif.clk);

      vif.ip1 <= tr.ip1;
      vif.ip2 <= tr.ip2;

      @(posedge vif.clk);

      tr.out = vif.out;

      $display("[DRV] ip1=%0d ip2=%0d out=%0d",
               tr.ip1, tr.ip2, tr.out);

    end

  endtask

endclass

```

## 4. Monitor:
- It Observes Transaction from interface and send the Output to Scoreboard.
```bash
class monitor;

  virtual add_if vif;
  mailbox mon_to_sb;

  transaction mon_tr;

  function new(mailbox mon_to_sb,
               virtual add_if vif);

    this.mon_to_sb = mon_to_sb;
    this.vif = vif;

  endfunction

  task run();

    forever begin

      wait(!vif.reset);

      @(posedge vif.clk);

      mon_tr = new();

      mon_tr.ip1 = vif.ip1;
      mon_tr.ip2 = vif.ip2;

      @(posedge vif.clk);

      mon_tr.out = vif.out;

      mon_to_sb.put(mon_tr);

      $display("[MON] ip1=%0d ip2=%0d out=%0d",
               mon_tr.ip1,
               mon_tr.ip2,
               mon_tr.out);

    end

  endtask

endclass
```
## 5. Scoreboard:
- Receives Transaction from `Monitor` and Compares it with Reference (Golden Data).

## Environment:
- It Manages well-mannered hierarcy and container for `Agent` and `Scoreboard`.
## Testbench Top:
- Includes Test + DUT + Interface.

## Test:
- it will initiates an Environment component and Connection Between them- also Responcible for configs and Stimulus generation.
