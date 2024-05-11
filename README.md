## 3.5 The stack and the heap

Let us briefly explain what the stack and the heap are.

Both are parts of memory that are available to the program at runtime. The stack is simpler: when a new value (e.g., of a variable) is to be added, it is always added at the “top” of the stack. 

The address of the current “top” of the stack is always available at runtime: actually, there is a special register of the processor dedicated only to store information on the current location of the top of the stack. In particular, no “looking for enough room in memory” is involved.

Whenever we create a new variable inside a block of code (e.g., inside a function), its value is pushed onto the stack. Then every time the flow of control leaves the block of code (e.g., a function exits), all the variables pushed onto the stack in this block are freed (deleted) in the reverse order as they were pushed, and stack is, as we say, rewound — the top of the stack is again at the position it had before entering the block. 

This means that all variables declared inside a block are lost forever when we leave it: they are all _local_. The process of removing values from the stack is called “popping off the stack”.

The advantage of using the stack to store variables is that memory is managed for you automatically. We don’t have to allocate memory by hand, or free it once we don’t need it any more. Also, the CPU organizes stack memory very efficiently: reading from and writing to stack is very fast.

The heap is a region of memory that is _not_ managed automatically. When the program asks the system to store some data on the heap, the system searches for a free space there, writes this data in this location, marks this region as occupied and return its address — this address can be stored in a variable of a reference type (which itself may be on the stack).

Note that if the value of this variable is lost, for example, because it was a local variable in a block, the data on the heap it referred to is no longer available, as we have lost its address! In Java, such unavailable object on the heap may be eventually freed automatically by the process of the so called _garbage collector_.

Unlike the stack, variables created on the heap are accessible not only locally, but wherever their address is known. Heap memory is slower to be read from and written to, because one has to use pointers (which contain addresses) and follow them to access memory on the heap. Also, the process of allocating memory on the heap is rather complicated and time consuming.
