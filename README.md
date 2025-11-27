# INTERFACING-OF-STEPPER-MOTOR-WITH-ARM-PROCESSOR.
AIM:
~~~
To interface and control the rotation of a stepper motor using the LPC1768 ARM Cortex-M3 microcontroller
~~~
COMPONENTS REQUIRED:
~~~
Hardware:
LPC1768 Development Board, Stepper Motor (5-wire/4-wire), ULN2003 Driver Module, Connecting Wires, Power Supply.

Software:
Keil µVision 4.0 IDE
~~~
PROCEDURE:
~~~
The experiment is carried out by first opening Keil µVision and creating a new project by selecting the LPC1768 microcontroller. The startup file is added automatically, after which a new C file is created to write the stepper motor control program. The file is saved as main.c and added to Source Group 1 along with other required files like system_LPC17xx.c, gpio.c, and delay.c. The project is then built, and errors are corrected if any. To generate the .bin file, the “Create HEX File” option is enabled under Target Options, and the IROM1 address is set to 0x2000. After rebuilding, the .bin file is generated. The hardware is then connected by interfacing LPC1768 GPIO pins to the ULN2003 driver, which controls the stepper motor. Finally, the program is flashed onto the board, and the stepper motor rotates according to the programmed stepping sequence.
~~~
PIN DIAGRAM:
~~~
<img width="489" height="407" alt="image" src="https://github.com/user-attachments/assets/0031977b-422e-4bd4-83d6-ca64689512aa" />
~~~
CIRCUIT DIAGRAM:
~~~
<img width="750" height="585" alt="image" src="https://github.com/user-attachments/assets/6dc7626a-443c-4681-9be3-11bb872e16bd" />
~~~
PROGRAM:
~~~
#include <LPC17xx.h>

void delay_ms(unsigned int ms) {
    unsigned int i, j;
    for(i = 0; i < ms; i++)
        for(j = 0; j < 5000; j++);
}

int main() {
    LPC_GPIO0->FIODIR |= (1 << 22); 
    LPC_GPIO1->FIODIR |= (1 << 18) | (1 << 20);

    while(1) {
        LPC_GPIO0->FIOSET = (1 << 22);
        LPC_GPIO1->FIOSET = (1 << 18) | (1 << 20);
        delay_ms(500);

        LPC_GPIO0->FIOCLR = (1 << 22);
        LPC_GPIO1->FIOCLR = (1 << 18) | (1 << 20);
        delay_ms(500);
    }
}
~~~
OUTPUT:
~~~
LEDs blink ON and OFF at 500 ms intervals.
~~~
