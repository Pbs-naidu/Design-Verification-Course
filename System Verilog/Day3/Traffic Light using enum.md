##  SIMPLE Traffic Light controller using an enum keyword. 
## Signal Should cycle throught IDLE->RED->YELLOW- >GREEN->RED(Loop)
###  State : IDLE - Duration 0 Sec RED - -//- 30 Sec Yellow -//- 5 Sec Green -//- 25 sec RED -//- 30 Sec (Loop Back)

```bash
// Code your testbench here
// or browse Examples

module sv_data_types_demo;

  // ============================================================
  //  ENUMERATION
  // ============================================================
  typedef enum {IDEAL,RED, YELLOW, GREEN} traffic_t;
  traffic_t    traffic_signal;
  initial begin
     forever begin
   traffic_signal = IDEAL;
  
   $display("  traffic_signal = %s (value = %0d) :time=%0t", traffic_signal.name(), traffic_signal,$time);
  
#30;  traffic_signal = RED;
  
   $display("  traffic_signal = %s (value = %0d) :time=%0t", traffic_signal.name(), traffic_signal,$time);
  
#5;  traffic_signal = YELLOW;
  
   $display("  traffic_signal = %s (value = %0d) : time=%0t", traffic_signal.name(), traffic_signal,$time);

#25;   traffic_signal = GREEN;
  
   $display("  traffic_signal = %s (value = %0d): time=%0t", traffic_signal.name(), traffic_signal,$time);

#30;   traffic_signal = RED;
  
   $display("  traffic_signal = %s (value = %0d) :time=%0t", traffic_signal.name(), traffic_signal,$time);
    end
  end
endmodule

```
## Results:

<img width="698" height="331" alt="image" src="https://github.com/user-attachments/assets/9e7337a4-cac9-4b0f-bc2c-9a258fb46693" />

