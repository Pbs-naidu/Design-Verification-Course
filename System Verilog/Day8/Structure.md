## Structure without typedef
### Difference Between Structure and Array is Data Type, you can use different data types in struct but in array you use same data type.
```bash
module struct_example;
  struct {
    string name;
    bit [31:0] salary;
    integer id;
  } employee;

  initial begin
    employee.name   = "Alex";
    employee.salary = 'h10000;
    employee.id     = 'd1234;

    $display("employee: %p", employee);

    // Accessing individual struct member
    $display("employee: name = %s, salary = 0x%0h, id = %0d",
             employee.name, employee.salary, employee.id);
  end
endmodule
```
## Result:
<img width="775" height="266" alt="image" src="https://github.com/user-attachments/assets/a8096314-6b82-416e-bb84-adb7a7dd9dca" />

## Structure without typedef

```bash
module struct_example;
  typedef struct {
    string  name;
    bit [31:0] salary;
    integer id;
  } employee;

  initial begin
    employee e1, e2;

    e1.name   = "Alex";
    e1.salary = 'h10000;
    e1.id     = 'd1234;

    $display("employee e1: %p", e1);

    e2.name   = "Bob";
    e2.salary = 'h20000;
    e2.id     = 'd4321;

    $display("employee e2: %p", e2);

    $display("------------------------------------------------");

    // Accessing individual struct member
    $display("employee e1: name = %s, salary = 0x%0h, id = %0d",
             e1.name, e1.salary, e1.id);

    $display("employee e2: name = %s, salary = 0x%0h, id = %0d",
             e2.name, e2.salary, e2.id);
  end
endmodule
```
## Result:
<img width="761" height="310" alt="image" src="https://github.com/user-attachments/assets/dbdefcf7-38c2-4ae4-b58d-c7327ae2cee3" />

## Struct with packed Array

```bash
module struct_example;
//packed name is used
  typedef struct packed {
    bit [31:0] salary;
    integer id;
  } employee;

  initial begin
    employee emp1, emp2;

    emp1.salary = 'h10000;
    emp1.id     = 'd1234;

    $display("EMP 1: %p", emp1);

    emp2.salary = 'h12000;
    emp2.id     = 'd4321;

    $display("EMP 2: %p", emp2);
  end
endmodule
```

## Result:
<img width="953" height="308" alt="image" src="https://github.com/user-attachments/assets/06fee130-bc17-40b6-923e-5daadb07ff0e" />

## struct with UnPacked Array

```bash
module struct_example;
//used string in unpacked structure
  typedef struct {
    string name;
    bit [31:0] salary;
    integer id;
  } employee;

  initial begin
    employee emp1, emp2;

    emp1.name   = "Alex";
    emp1.salary = 'h10000;
    emp1.id     = 'd1234;

    $display("EMP 1: %p", emp1);

    emp2.name   = "John";
    emp2.salary = 'h12000;
    emp2.id     = 'd4321;

    $display("EMP 2: %p", emp2);
  end
endmodule
```

## Result:
<img width="967" height="310" alt="image" src="https://github.com/user-attachments/assets/e3788db4-f6e4-4248-902c-78806bfdd9e7" />

## Union
### Union vs Structure Both are same only difference is union different Data Types Shares Same Memory

```bash
module union_example;
typedef union {
    bit [15:0] salary;
    integer    id;
} employee;

initial begin
    employee emp;

    emp.salary = 'h800;
    $display("salary updated for EMP: %p", emp);

    emp.id = 'd1234;
    $display("ID updated for EMP: %p", emp); // Note: Salary information will be lost
end

endmodule
```
## Result:
<img width="964" height="320" alt="image" src="https://github.com/user-attachments/assets/71dc982c-32ce-464b-be48-c3118a36c1d9" />
