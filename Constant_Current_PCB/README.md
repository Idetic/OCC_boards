# Constant Current PCB

This PCB design functions as a constant current circuit, driving an LED with high accuracy. The input of the board requires a voltage source and a voltage reference to set the intensity of the LED. Depending on the chosen resistance values, this circuit can drive an LED with a wide range of intensity levels.

## Parameters

The input of the circuit is a voltage level (output of microcontroller for example), while the output is a current level for driving the LED. The parameters of the circuit are as follows:

1. $R_{\text{sense}} $: The current through this resistance is "copied" to the LED. 
2. $R_{1}$, $R_{2}$: These resistors form a voltage divider for conditioning the input voltage.

## Diagram

![Circuit Diagram](https://github.com/Idetic/OCC_boards/blob/main/Constant_Current_PCB/img/circuit.png?raw=true)

![3d View](https://github.com/Idetic/OCC_boards/blob/main/Constant_Current_PCB/img/View_1.png?raw=true)

## Components

1. OPAMP: The $-V_{supply}$ needs to be 0V.

## Formulas

Assuming $V_{cc}$ is fixed (typically 5V, 9V, or 12V), to drive an LED between 0 [A] and  $I_{\text{LED max}}$ [A], we know (from the datasheet) that we need to apply 0 [V] and $V_{\text{LED max}}$ [V], respectively. From the circuit, we have the following relationship:

$$
V_{cc} = V_{LED} + V_{CE} + V_{R_{\text{sense}}}
$$

Typical $V_{CE}$ values range from 0.3 to 1.0 [V]. We know that $I_{R_{\text{sense}}} = I_{\text{LED}}$. Rearranging the first equation, we have:

$$
R_{\text{sense}} \times I_{\text{LED}} = V_{cc} - V_{CE} - V_{LED}
$$

Additionally, the voltage applied to $R_{\text{sense}}$ is given by $V_{in} \cdot \frac{R_{1}}{R_{1}+R_{2}}$. Thus, to drive the LED at $I_{\text{max}}$ [A], we have the following equation:

$$
I_{\text{LED max}} = \frac{V_{in}}{R_{\text{sense}}} \cdot \frac{R_{1}}{R_{1}+R_{2}}
$$

From this, we can determine the value of $R_{\text{sense}}$:

$$
R_{\text{sense}} = \frac{V_{in}}{I_{\text{LED max}}} \cdot \frac{R_{1}}{R_{1}+R_{2}}
$$

### Why Do We Need a Voltage Divider?

It is important to note that depending on $V_{cc}$, it may not be possible to drive the LED at $I_{\text{LED max}}$ due to the voltage drop across $R_{\text{sense}}$ being too high (as indicated by the first equation). Therefore, the voltage divider ($R_{1}$ and $R_{2}$) can help us control the voltage drop across $R_{\text{sense}}$.

### Microcontroller

We recommend using the STM32L43KC, which features a DAC output that can be easily controlled via the Arduino IDE.

