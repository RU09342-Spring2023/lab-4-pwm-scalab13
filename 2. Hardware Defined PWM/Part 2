/*
 * Part2.1.c
 *
 *  Created on: Feb 26, 2023
 *      Author: Brian Scala
 */

#include <msp430.h>
unsigned int count = 1;  //keep track of loop
void gpioInit();
int main(void)
{
    gpioInit();
    PM5CTL0 &= ~LOCKLPM5;
  WDTCTL = WDTPW | WDTHOLD;                    // Stop WDT
 TB0CTL = TBSSEL__SMCLK | MC__UP | TBIE;               // SMCLK, UP mode, enable interupt
  TB0CCTL1 |= CCIE;                             // Enable TB0 CCR1 Interrupt
  TB0CCTL2 |= CCIE;                             //Enable TB0 CCR2 Interupt
  TB0CCR0 = 1000;
  TB0CCR1 = 30;                          // Set CCR1 to the value to set the duty cycle
  TB0CCR2  = 999;

 // Setup Timer Compare IRQ
          TB1CCTL0 |= CCIE;             //Enable TB1 CCR0 Overflow IRQ
          TB1CCR0 = 1000;              //Set Compare Timer Cycle Time
          TB1CTL = TBSSEL_1 | MC_2 | ID_3;      //ACLK, Continuous Mode




    __bis_SR_register(LPM3_bits | GIE);           // Enter LPM3, enable interrupts
    __no_operation();                             // For debugger
}



//Timer B1 interrupt service routine
#pragma vector = TIMER1_B0_VECTOR
__interrupt void Timer1_B0_ISR(void) {

    if(count <= 323) {
        TB0CCR1 += 3; //decrease Blue led brightness
        TB0CCR2 -= 3; //Increase red LED brightness
    }
    else if (count > 323 && count <= 646){
        TB0CCR1 -= 3;  //Increase green Led Brightness
        TB0CCR2 += 3;  //decrease Red Led brightness
    }
    else if (count > 646 && count <= 969){
        TB0CCR1 += 3;     //decrease green Led brightness
        TB0CCR2 -= 3;    // Increase Blue Led Brightness
    }
    else if (count > 969 && count <= 1292) {
        TB0CCR1 -= 3; //Decrease blue LED Brightness
        TB0CCR2 += 3;//Increase Red LED
    }
    else if (count > 1292 && count <= 1615) {
        TB0CCR1 += 3;     //Decrease Red LED Brightness
        TB0CCR2 -= 3;   //Increase green led brightness
    }
    else if (count > 1615 && count <= 1938){
        TB0CCR1 -= 3;      //Increase Blue Led Brightness
        TB0CCR2 += 3;     //Decrease Green Led Brightness
    }

    if(count >= 1938){
        count = 1; //reset count
    }
    else {
        ++count;  //Increment Count
    }
    TB1CCR0 += 50;                   //increase timer
}
// Timer0_B3 Interrupt Vector (TBIV) handler
#if defined(__TI_COMPILER_VERSION__) || defined(__IAR_SYSTEMS_ICC__)
#pragma vector=TIMER0_B1_VECTOR
__interrupt void TIMER0_B1_ISR(void)
#elif defined(__GNUC__)
void __attribute__ ((interrupt(TIMER0_B1_VECTOR))) TIMER0_B1_ISR (void)
#else
#error Compiler not supported!
#endif
{
    switch(__even_in_range(TB0IV,TB0IV_TBIFG))
    {
        case TB0IV_NONE:
            break;                               // No interrupt
        case TB0IV_TBCCR1:
            if(count <= 323){
                P6OUT |= BIT1;      //Fade Blue LED
            }
            else if(count > 323 && count <= 969){
                P6OUT |= BIT2;      //Fade Green LED
            }
            else if(count > 969 && count <= 1615){
                P6OUT |= BIT0;      //Fade Red LED
            }
            else if(count > 1615 && count <= 1938){
                P6OUT |= BIT1;      //Fade Blue LED
            }

            break;                               // CCR1 Set the pin to a 0
        case TB0IV_TBCCR2:
            if(count <= 626){
                P6OUT |= BIT0;      //Fade Red LED
            }
            else if(count > 626 && count <= 1292){
                P6OUT |= BIT1;      //Fade Blue LED
            }
            else if(count > 1292 && count <= 1938){
                P6OUT |= BIT2;      //Fade Green LED
            }
            break;                               // CCR2 not used
        case TB0IV_TBIFG:   // Turn off LED
            P6OUT &= ~BIT0;
            P6OUT &= ~BIT1;
            P6OUT &= ~BIT2;
            break;
        default:
            break;
    }
}


void gpioInit(){


    P6DIR |= BIT0;  //P6.0 Output Direction
    P6DIR |= BIT1; //P6.1 Output Direction
    P6DIR |= BIT2; //P6.2 Output Direction
}

