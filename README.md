# EXPERIMENT-01-Interfacing-Multiple-Switches-for-LED-Control-Using-MicroPython


 
## NAME: S.VENGADA KRISHNAN

## DEPARTMENT: CSE(IOT)

## ROLL NO: 212223110061

## DATE OF EXPERIMENT: 21.4.2026

## AIM

To interface multiple switches with the Raspberry Pi Pico and control LEDs using MicroPython.

## APPARATUS REQUIRED

1. Raspberry Pi Pico - 1

2. Push Button Switches - 2

3. LEDs (Light Emitting Diodes) -3

4. Buzzer - 1

5. 330Ω Resistors -3

6. Breadboard

7. Jumper Wires

8. USB Cable

## THEORY

<img width="474" height="407" alt="image" src="https://github.com/user-attachments/assets/df0155b7-5b06-4276-aad3-0e114260605d" />

## FIGURE-01: RASPBERRY PI PICO PINOUT DIAGRAM

Raspberry Pi Pico is a microcontroller board based on the RP2040 chip. It supports MicroPython, making it suitable for IoT and embedded applications. The Raspberry Pi Pico is a compact microcontroller board featuring a 40-pin layout, including power, ground, GPIO, and communication interface pins. It operates with a dual-core ARM Cortex-M0+ processor and supports MicroPython and C/C++ programming.

The power pins include VBUS (5V from USB), VSYS (1.8V to 5.5V input), 3V3(OUT) (regulated 3.3V output), and multiple ground (GND) connections. The board offers 26 multi-purpose GPIO pins (GP0 to GP28), which can be used for digital input, output, PWM, and communication interfaces such as I2C, SPI, and UART. It also features three analog-to-digital converter (ADC) pins (GP26, GP27, GP28), used for reading analog sensor values, along with an ADC_VREF pin to set the reference voltage.

For communication, I2C (SDA, SCL), SPI (MOSI, MISO, SCK), and UART (TX, RX) interfaces are mapped across different GPIO pins, allowing seamless connectivity with sensors and peripherals. All GPIO pins support PWM (Pulse Width Modulation), making it useful for motor control, LED brightness adjustment, and sound applications. The BOOTSEL button enables USB mass storage mode for firmware flashing, while the DEBUG pins (SWD interface) provide debugging capabilities. With its low power consumption, flexible GPIO options, and rich interface support, the Raspberry Pi Pico is widely used for IoT, embedded systems, robotics, and automation projects.

## WORKING PRINCIPLE

## Experiment 1A:
1. The LEDs are connected as outputs in any three GPIO pins.

2. The Buzzer connected as output in any one LED connected GPIO pins.

3. A MicroPython script reads the switch states and controls the LEDs accordingly.

## Experiment 1B:

1. The switches are connected as inputs to GPIO pins of the Pico.

2. The LEDs are connected as outputs.

3. A MicroPython script reads the switch states and controls the LEDs accordingly.

### CIRCUIT DIAGRAM
## Experiment 1A

<img width="710" height="507" alt="image" src="https://github.com/user-attachments/assets/6bc88cc6-578c-4c45-a346-17d4804816ae" />

## FIGURE-02:  Circuit Diagram of Digital Output Interface 

1. Connect LED 1 to GPIO 0 via a 330Ω resistor, LED 2 to GPIO 2 via a 330Ω resistor and LED 3 to GPIO 4 via a 330Ω resistor.

2. Connect the Buzzer positive to either one pins GPIO 0 or GPIO 2 or GPIO 4.

3. Connect the other terminals of the LEDs and Buzzer to GND.

## Experiment 1B

<img width="940" height="576" alt="image" src="https://github.com/user-attachments/assets/6fc9a95f-28d4-4793-bf72-f60e34877c33" />

## FIGURE-03:  Circuit Diagram of Digital Input and Output Interface 


1. Connect switch 1 to GPIO 2 and switch 2 to GPIO 3.

2. Connect LED 1 to GPIO 13 via a 330Ω resistor.

3. Connect LED 2 to GPIO 16 via a 330Ω resistor.

4. Connect the other terminals of the switches to GND.

## PROGRAM (MicroPython)
```

## Experiment 1A:

from machine import Pin
import time
print("Pi Pico")
led1 = Pin(0, Pin.OUT)
led2 = Pin(2, Pin.OUT)
led3 = Pin(4, Pin.OUT)
buzzer=Pin(4,Pin.OUT)
while True:
    led1.value(1) 
    print("LED is ON")
    time.sleep(1) 
    led1.value(0)  
    print("LED is OFF")
    time.sleep(1)
    led2.value(1) 
    print("LED is ON")
    time.sleep(1) 
    led2.value(0)  
    print("LED is OFF")
    time.sleep(1)
    led3.value(1) 
    print("LED is ON")
    time.sleep(1) 
    led3.value(0)  
    print("LED is OFF")
    time.sleep(1)
    buzzer.value(1) 
    print("Buzzer is ON")
    time.sleep(1) 
    buzzer.value(0)  
    print("Buzzer is OFF")
    time.sleep(1)




## Experiment 1B:


from machine import Pin
from time import sleep

switch1 = Pin(2, Pin.IN, Pin.PULL_DOWN)
switch2 = Pin(28, Pin.IN, Pin.PULL_DOWN)

led1 = Pin(13, Pin.OUT)
led2 = Pin(18, Pin.OUT)

prev = None

print("AND Gate Started\n")

while True:
    s1 = switch1.value()
    s2 = switch2.value()

    result = s1 and s2

    led1.value(result)
    led2.value(result)

    state = (s1, s2, result)

    if state != prev:
        print(
            f"S1: {s1} | S2: {s2} | OUT: {result} -> "
            f"{'ON' if result else 'OFF'}"
        )
        prev = state

    sleep(0.05)

 ```

## OUTPUT


## Experiment 1A:



## FIGURE-04: CIRCUIT CONNECTION

<img width="1107" height="605" alt="Screenshot 2026-04-21 134753" src="https://github.com/user-attachments/assets/7af6c44a-9656-4782-a6e8-7f132588b16e" />


## FIGURE-05: CODE EXECUTION OUTPUT


<img width="990" height="819" alt="Screenshot 2026-04-21 135155" src="https://github.com/user-attachments/assets/7a5b0c94-92c3-4314-8932-fb2de1079a1c" />


## FIGURE-06: LED AND BUZZER STATUS


<img width="990" height="819" alt="Screenshot 2026-04-21 135155" src="https://github.com/user-attachments/assets/b1219eb8-dc22-4cd3-b946-3f79067a5b07" />

<img width="1088" height="865" alt="Screenshot 2026-04-21 135211" src="https://github.com/user-attachments/assets/99efd4d5-7838-4de2-afa7-398df74d64d0" />


<img width="1093" height="860" alt="Screenshot 2026-04-21 135223" src="https://github.com/user-attachments/assets/ea0fd45a-6555-45e3-98dc-50ea01fc5bec" />


<img width="1105" height="882" alt="Screenshot 2026-04-21 135233" src="https://github.com/user-attachments/assets/64f59b9b-b86f-4c6f-922c-6dd3f385451c" />





## Experiment 1B:


## FIGURE-07: CIRCUIT CONNECTION


<img width="401" height="366" alt="image" src="https://github.com/user-attachments/assets/f4a90b7a-5454-4a5f-b78c-41bd69d6b3fc" />


## FIGURE-08: CODE EXECUTION OUTPUT


<img width="358" height="192" alt="image" src="https://github.com/user-attachments/assets/62393740-929e-4291-9ce1-78be932865e2" />


## FIGURE-09: LED STATUS BASED ON SWITCH INPUTS

<img width="534" height="467" alt="image" src="https://github.com/user-attachments/assets/2d4b29a9-b2b5-4071-bf7b-bf493e3d514d" />

<img width="556" height="500" alt="image" src="https://github.com/user-attachments/assets/1794b5fe-ddcb-4e55-a409-cba1770c991f" />


<img width="567" height="486" alt="image" src="https://github.com/user-attachments/assets/dac98497-d71a-4533-a062-4f1e16e09a19" />

<img width="566" height="561" alt="image" src="https://github.com/user-attachments/assets/dea50fae-4916-40e8-a311-0c2b266e7594" />

## RESULTS

The multiple switches connected to the Raspberry Pi Pico successfully controlled the LEDs based on their states, confirming the proper interfacing of digital inputs and outputs.

