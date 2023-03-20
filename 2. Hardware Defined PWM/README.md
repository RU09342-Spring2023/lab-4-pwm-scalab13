Brian Scala
Lab 4 Part2.Hardware Defined PWM

Task:
  Have an RGB LED fade trough the colors.
  
 Hardware:
  A bread board is used with a RGB LED. Use two 750Ω and a 450Ω resistor. Connect the two 750Ω to the red and yellow LED and the 450 to the Blue. ALl connected in series. Use Jumpers to connect the MSP board to the respective resistors. P6.0 is red, P6.1 is blue and P6.2 is Green.
  
 Code:
    The code used the function GPIOInit to configure output pins 6.0-6.2. The code starts at red and fades to green then blue. Todo this timer SMCLK is set to up mode, CCR0 is set to 1000(Period), CCR1 = 30(Brightness) and CCR2 = 999(Red Brightness). ACLK is used in continuous mode to keep track of the timer with a variable count. Every time the timer resets count increments. An if statement is used to break up the different valyes of count. Depending on the value of count CCR1 will increase  by 3 and CCR2 will decrease by 3 or it's reversed. In the second interupt, the outputs are being set to each CCR. The output will change for the CCR based on count. This is because there are only three CCR0-2. For example when we're fading from red to green. CCR1 is set to the red LED, but for blue to green, CCR2 is set to the RED LED. 
  
