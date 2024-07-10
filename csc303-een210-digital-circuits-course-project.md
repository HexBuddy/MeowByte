---
description: Design, Testing, and Implementation of a Light Control System
---

# CSC303/EEN210: Digital Circuits Course Project

## **Step 1: Design the Digital Logic Circuit**

**1.1 Determine the Logic Requirements**

1. **White Lights Control:**
   * All three white lights are controlled by any of the four switches.
   * If any switch is on, all white lights should be on.
   * If all switches are off, the white lights should be off.
2. **Yellow Light Control:**
   * The yellow light should be on if exactly two switches are on.
3. **LED Display:**
   * A 3-LED binary display shows the number of switches that are on.

**1.2 Truth Table Creation**

Create a truth table that defines the system's behavior:

| Switch 1 | Switch 2 | Switch 3 | Switch 4 | White Lights | Yellow Light | LED Display |
| -------- | -------- | -------- | -------- | ------------ | ------------ | ----------- |
| 0        | 0        | 0        | 0        | 0            | 0            | 000         |
| 0        | 0        | 0        | 1        | 1            | 0            | 001         |
| 0        | 0        | 1        | 0        | 1            | 0            | 001         |
| 0        | 0        | 1        | 1        | 1            | 1            | 010         |
| 0        | 1        | 0        | 0        | 1            | 0            | 001         |
| 0        | 1        | 0        | 1        | 1            | 1            | 010         |
| 0        | 1        | 1        | 0        | 1            | 1            | 010         |
| 0        | 1        | 1        | 1        | 1            | 0            | 011         |
| 1        | 0        | 0        | 0        | 1            | 0            | 001         |
| 1        | 0        | 0        | 1        | 1            | 1            | 010         |
| 1        | 0        | 1        | 0        | 1            | 1            | 010         |
| 1        | 0        | 1        | 1        | 1            | 0            | 011         |
| 1        | 1        | 0        | 0        | 1            | 1            | 010         |
| 1        | 1        | 0        | 1        | 1            | 0            | 011         |
| 1        | 1        | 1        | 0        | 1            | 0            | 011         |
| 1        | 1        | 1        | 1        | 1            | 0            | 100         |

**1.3 Karnaugh Map (K-Map) Creation**

Create K-Maps for each output (white lights, yellow light, and each bit of the LED display) to simplify the logic expressions.

* **White Lights (W) K-Map:**
  * The white lights turn on if at least one switch is on.

| S3\S4 | 00 | 01 | 11 | 10 |
| ----- | -- | -- | -- | -- |
| 00    | 0  | 1  | 1  | 1  |
| 01    | 1  | 1  | 1  | 1  |
| 11    | 1  | 1  | 1  | 1  |
| 10    | 1  | 1  | 1  | 1  |

* Simplified Boolean expression:&#x20;

$$
W=S1+S2+S3+S4
$$

* **Yellow Light (Y) K-Map:**
  * The yellow light turns on if exactly two switches are on.

| S3\S4 | 00 | 01 | 11 | 10 |
| ----- | -- | -- | -- | -- |
| 00    | 0  | 0  | 0  | 0  |
| 01    | 0  | 0  | 1  | 1  |
| 11    | 0  | 1  | 0  | 0  |
| 10    | 0  | 1  | 0  | 1  |

* Simplified Boolean expression:&#x20;

$$
( Y = (S1 \cdot S2 \cdot S3' \cdot S4') + (S1 \cdot S2' \cdot S3 \cdot S4') + (S1 \cdot S2' \cdot S3' \cdot S4) + (S1' \cdot S2 \cdot S3 \cdot S4') + (S1' \cdot S2 \cdot S3' \cdot S4) + (S1' \cdot S2' \cdot S3 \cdot S4) )
$$



* **LED Display K-Maps:**
  * For each bit of the LED display, create a K-Map and simplify.

**1.4 Boolean Expressions for LED Display**

* **LED1:** (Least significant bit)

$$
LED1=S1⊕S2⊕S3⊕S4
$$

* **LED2:**

$$
LED2=(S1⋅S2)+(S1⋅S3)+(S1⋅S4)+(S2⋅S3)+(S2⋅S4)+(S3⋅S4)
$$

* **LED3:** (Most significant bit)

$$
LED3=S1⋅S2⋅S3⋅S4
$$

***

## **Step 2: Implement the Circuit in TinkerCad**

**2.1 Setting Up TinkerCad**

1. **Create an Account:**
   * Go to the [TinkerCad](https://www.tinkercad.com) website and create an account if you don’t already have one.
2. **Create a New Project:**
   * Start a new circuit project.

**2.2 Building the Circuit**

1. **Place Components:**
   * Place four switches, three white LEDs, one yellow LED, and a 3-segment LED display on the workspace.
2. **Connect Switches:**
   * Connect each switch to a digital input pin.
3. **Logic Gates:**
   * Use the logic gates according to the simplified Boolean expressions derived earlier.
4. **Connect LEDs:**
   * Connect the outputs of the logic gates to the corresponding LEDs.
5. **Power Supply:**
   * Connect the circuit to a suitable power supply within TinkerCad.

**2.3 Simulating the Circuit**

1. **Test Each Configuration:**
   * Simulate each possible switch configuration to ensure the white lights, yellow light, and LED display respond correctly.

***

## **Step 3: Hardware Implementation**

**3.1 Parts List and Financial Management**

1. **Parts List:**
   * 4 SPST (Single Pole Single Throw) switches
   * 3 white LEDs
   * 1 yellow LED
   * 3-segment LED display
   * Assorted logic gates (AND, OR, NOT, XOR)
   * Breadboard
   * Jumper wires
   * 9V battery or suitable DC power supply
   * Resistors (220 ohms for LEDs)
2. **Budget Management:**
   * Research and list the cost of each component.
   * Consider buying components in bulk or from budget-friendly suppliers.
   * Allocate a budget for each phase of the project.

**3.2 Building the Circuit in the Lab**

1. **Set Up Breadboard:**
   * Place the components on the breadboard.
2. **Connect Switches:**
   * Connect each switch to the inputs of the logic gates.
3. **Connect LEDs:**
   * Connect the outputs of the logic gates to the corresponding LEDs.
4. **Power Supply:**
   * Connect the circuit to a power supply, ensuring correct voltage and current ratings.
5. **Testing:**
   * Test each switch configuration to ensure the circuit works as expected.

***

## **Step 4: Documentation**

**4.1 Create a Full Report**

1. **Introduction:**
   * Describe the project objectives and requirements.
2. **Design Process:**
   * Document the truth table, K-Maps, and Boolean expressions.
3. **Simulation:**
   * Include screenshots and descriptions of the TinkerCad simulation.
4. **Hardware Implementation:**
   * Include photos and descriptions of the hardware setup and testing.
5. **Conclusion:**
   * Summarize the project outcomes and any challenges faced.

***

#### **Submission Deadlines**

* **Phase 1:** Submit the truth tables by 12/7/2024.
* **Phase 2:** Submit K-Maps and Boolean expressions by 17/7/2024.
* **Phase 3:** Submit TinkerCad simulation by 21/7/2024.
* **Phase 4:** Submit hardware implementation and project report by 5/8/2024.

***

#### **Conclusion**

By following this guide, you will be able to design, test, and implement a functional Light Control System for a hospital room. This project will help you apply your knowledge of digital logic circuits and gain hands-on experience with both simulation software and hardware components.

Feel free to reach out if you have any questions or need further assistance. Good luck with your project!
