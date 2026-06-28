## Inter-process Communication
&rarr; Semaphores <br>
&rarr; Mailbox

## Semaphores:
&rarr; Semaphores are used to control the access of the shared resources. <br>
&rarr; If you create a semaphore with only 1 key, it acts as a mutual exclusion (mutex) lock, 
meaning only one process can access the bucket (and thereby the shared resource) at any given time.

<img width="887" height="321" alt="image" src="https://github.com/user-attachments/assets/9dcdfb9e-5092-4f1a-ac63-ee4b431c2b25" />

```bash
module semaphore_example();

  // Create a semaphore with one key
  semaphore sem = new(1);

  // Task to write into memory
  task write_mem();
    sem.get();   // Acquire semaphore

    $display("[%0t] Before writing into memory", $time);
    #5ns;         // Assume 5 ns is required to write
    $display("[%0t] Write completed into memory", $time);

    sem.put();   // Release semaphore
  endtask

  // Task to read from memory
  task read_mem();
    sem.get();   // Acquire semaphore

    $display("[%0t] Before reading from memory", $time);
    #4ns;         // Assume 4 ns is required to read
    $display("[%0t] Read completed from memory", $time);

    sem.put();   // Release semaphore
  endtask

  // Execute both tasks in parallel
  initial begin
    fork
      write_mem();
      read_mem();
    join
  end

endmodule

```

## Result:
<img width="808" height="332" alt="image" src="https://github.com/user-attachments/assets/27fa3bd8-180d-4547-af5b-c20a52c62ca2" />

### **try_get() :**
  
```bash
module semaphore_example();

  // Create a semaphore with one key
  semaphore sem = new(1);

  // Process A
  task process_A();
    if (sem.try_get())
      $display("[%0t] process_A: Key received", $time);
    else
      $display("[%0t] process_A: Key is not available", $time);

    $display("[%0t] process_A started", $time);
    #5ns;
    $display("[%0t] process_A completed", $time);

    sem.put();
  endtask

  // Process B
  task process_B();
    if (sem.try_get())
      $display("[%0t] process_B: Key received", $time);
    else
      $display("[%0t] process_B: Key is not available", $time);

    $display("[%0t] process_B started", $time);
    #4ns;
    $display("[%0t] process_B completed", $time);

    sem.put();
  endtask

  initial begin
    fork
      process_A();
      process_B();
    join
  end

endmodule
```

## Result:
<img width="773" height="330" alt="image" src="https://github.com/user-attachments/assets/d46f4dde-752c-4b03-8dd7-d1130595a3fd" />

## Mailbox
- one process can put Data into Mailbox : that stores data internally & retrieved by another process
### 2 Types of Mailbox
1. Generic (Default mailbox) <br>
   &rarr; can put and get data of any data type like int,bit,byte,string etc..
   
3. Parameterized <br>
   &rarr; put or get data of Particular type.
5. Bounded <br>
   &rarr; size of mailbox is defined.
7. Unbounded <br>
   &rarr; size is not defined.

### Mailbox Methods:
<img width="1536" height="1024" alt="ChatGPT Image Jun 28, 2026, 12_13_24 PM" src="https://github.com/user-attachments/assets/bfaca703-4692-4dbc-a1e6-39966bf73f58" />

```bash
module mailbox_example();

  mailbox mb = new(3);

  // Producer
  task process_A();
    int value;

    for (value = 1; value <= 5; value++) begin
      $display("[%0t] Trying to put %0d", $time, value);

      mb.put(value);

      $display("[%0t] Successfully put %0d", $time, value);
    end
  endtask

  // Consumer
  task process_B();
    int value;

    #20;    // Delay consumer so mailbox becomes full

    repeat (5) begin
      mb.get(value);
      $display("[%0t] Retrieved data = %0d", $time, value);

      #10;
    end
  endtask

  initial begin
    fork
      process_A();
      process_B();
    join
  end

endmodule
```

## Result:
<img width="812" height="516" alt="image" src="https://github.com/user-attachments/assets/151177ad-5dc9-44b7-8b08-bb669a84439e" />
