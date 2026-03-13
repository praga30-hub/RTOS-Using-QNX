# Experiment 401: Handling Hardware Interrupts in QNX

## Aim

To demonstrate **hardware interrupt handling in QNX** by attaching to an interrupt and waiting for the interrupt event.

---

## Objective

* To understand **interrupt handling in the QNX Neutrino RTOS**.
* To use the functions **InterruptAttach()** and **InterruptWait()**.
* To detect and respond when an interrupt occurs.

---

## Problem Statement

Develop a QNX program that **attaches to a hardware interrupt (e.g., keyboard interrupt)** and waits for the interrupt to occur.
Whenever the interrupt is triggered, the program should **print a message indicating that the interrupt was received**.

---

# Algorithm

1. Start the program.
2. Declare a variable for the **interrupt number (IRQ)**.
3. Declare a variable to store the **interrupt attachment ID**.
4. Display a message indicating the start of the interrupt example.
5. Attach to the interrupt using `InterruptAttach()`.
6. If interrupt attachment fails:

   * Print the error message.
   * Terminate the program.
7. Display a message indicating successful interrupt attachment.
8. Enter an infinite loop.
9. Wait for the interrupt using `InterruptWait()`.
10. When the interrupt occurs, print **"Interrupt received!"**.
11. Continue waiting for the next interrupt.

---

# Program

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/neutrino.h>
#include <sys/syspage.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    int irq = 1;           // interrupt number (example: keyboard)
    int id;

    printf("Simple Interrupt Example\n");

    /* Attach interrupt */
    id = InterruptAttach(irq, NULL, NULL, 0, 0);
    if (id == -1)
    {
        perror("InterruptAttach");
        return EXIT_FAILURE;
    }

    printf("Attached to interrupt %d\n", irq);

    while (1)
    {
        /* Wait for interrupt */
        InterruptWait(0, NULL);

        printf("Interrupt received!\n");
    }

    return 0;
}
```

---

# Expected Output

```text
Simple Interrupt Example
Attached to interrupt 1
Interrupt received!
Interrupt received!
Interrupt received!
...
```

*(The message appears each time the specified interrupt occurs.)*

---

# Result

Thus, the **hardware interrupt handling mechanism in QNX** was successfully implemented using `InterruptAttach()` and `InterruptWait()`, and the program correctly responded whenever the interrupt occurred.
