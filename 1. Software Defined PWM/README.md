Brian Scala
Lab 4 Part 1.Software Defined PWM

Task - Increase the red and green LED by 10% everytime there respective button is pressed. When at the brightest point, the brightness is set to the lowest brightness.

Code: The code consist of two functiond and 3 interupts. In the main function we call our GPIOInit function. This is where all the pins and buttons are configured. The code uses SMCLK in Upmode and interupts are enabled. CCR0 is setting the period for the LED's. CCR1 and CCR2 are controling the brightness of the LED's. CCR1 is set to P1.0 and CCR2 is set to P6.6. The first interupt is the timer Interupt.  This is where the CCR1 and CCR2 are asssignned. It also turns the outputs P1.0 and P6.6 on. The second and third interupt work the same. They wait for there respective button to be pressed(P2.3 and P4.3). When the button is pressed the CCR is incremneted by 100 because the period is 1000. This is a 10% increase in brightness. When it gets to 1000, the brightness is set to 30.
