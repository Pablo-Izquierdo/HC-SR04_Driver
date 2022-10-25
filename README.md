# HC-SR04_Driver

Everything is in assembly code for a raspberry with a HC-SR04 sensor

## Version 1
### d_distancia1

Initially the 'Trig' output will be held at a value of one for a minimum of 10 microseconds.
Then the status of the 'Echo' signal is checked until it takes the value 1 (continuous poll), at which time a measurement of the timer counters is taken. The waiting process is repeated, but now waiting for it to returns to the value 0. The distance can be calculated as D=T(s)*343,2(m/s)/2, but this can be somewhat complicated to implement. A reasonable approximation is to multiply the time (in microseconds) by 11246 and divide by 65536 (shift 16 bits to the right).

### d_distancia2

In order to take advantage of the time that the 'Echo' pulse is at a high value, the interruption management scheme will be used on the rising flank. In this section we will use the GPIO device flank detection system will be used in this section, but we will continue to check for the arrival of the edge by continuous polling.

## Version 2

### d_distancia3

This implementation is based on interruption management.

The first thing to do is to develop an flank detection interrupt care routine. This routine must determine the value of the timer counter. 
The initialization process must take care of the interrupt by means of the attention routine to be developed and the corresponding line must be enabled in the interrupt controller.
The signal reading process function must wait until the interruption has been processed.
