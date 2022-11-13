# Interfacing-Seven-segment-display-with-lpc2148

Name: Evangelin	
Roll no :212221230025
Date of experiment: 12-11-22

 
 

### Aim: 
To configure and display 4 character LED seven segment display and write a c code for displaying number 1 to 9 and A to F 
### Components required: 
Proteus ISIS professional suite, Kiel μ vision 5 Development environment 
 ![image](https://user-images.githubusercontent.com/36288975/201021692-efa39349-1a3c-4737-aadc-1843b954c78d.png)
Figure-01 Internal circuit for seven segment MPX4 display



### Theory: 
	7 Segment Display has seven segments in it and each segment has one LED inside it to display the numbers by lighting up the corresponding segments. Like if you want the 7-segment to display the number "5" then you need to glow segment a,f,g,c, and d by making their corresponding pins high. There are two types of 7-segment displays: Common Cathode and Common Anode, here we are using Common Cathode seven segment display.
   ![image](https://user-images.githubusercontent.com/36288975/201021740-565b47cd-26d8-4e54-a092-eef7a0a85278.png)
 
          Figure-02 Pin configuration for seven segment display  


Below table shows the HEX values and corresponding digit according to LPC2148 pins for common cathode configuration.



Sl no 	Hex code 	Output of LCD
1	0x88	1
2	0xeb	2
3	0x4c	3
4	0x49	4
5	0x2b	5
6	0x19	6
7	0x18	7
8	0xcb	8
9	0x8	9
10	0x9	A
11	0xa	B
12	0x38	C
13	0x9c	D
14	0x68	E
15	0x1c 	F
16	0x1e	0

 

![image](https://user-images.githubusercontent.com/36288975/201021930-7efe2b15-b0de-4d52-b87d-329fe6b91c89.png)
        Figure -3 Circuit diagram of interfacing for LPX4 - CA

## Kiel - Program 

```
#include <LPC214x.H>
unsigned char dig[]= {0x88,0xeb,0x4c,0x49,0x2b,0x19,0x18,0xcb,0x8,0x9,0xa,0x38,0x9c,0x68,0x1c,0x1e};

void delay(unsigned int count)
{
	int j=0,i=0;
	for(j=0;j<count;j++)
	{
		for(i=0;i<120;i++);
	}
}

int main(void)
{
	unsigned char count=0;
	unsigned int i=0;
	IO0DIR |= (1 << 11);
	IO0SET |= (1 << 11);
	IO0DIR |= 0x007F8000;
	while(1)
	{
		count++;
		if(count == 16)count=0;
		for(i=0;i<800;i++)
		{
			IO0CLR = 0x007f8000;
			IO0SET = (dig[count] << 15);
			delay(200);
		}
  }
}
```

### OUTPUT:
## Before Stimulation:
![exper8 off](https://user-images.githubusercontent.com/94219798/201467720-5007abd5-0a9d-4682-b267-3d29acb9fb9f.JPG)


## After Stimulation - Digit:

 ![exper8 num](https://user-images.githubusercontent.com/94219798/201467716-98184df6-36a8-4e15-aa51-15d68d6ae440.JPG)

## After Stimulation - Alphabet:
![exper8 alph](https://user-images.githubusercontent.com/94219798/201467731-9122d1d2-0bc5-4958-8ff1-d4f851f6bda9.JPG)

## Circuit Diagram:
![exper8 cir](https://user-images.githubusercontent.com/94219798/201467841-8319cb4b-d0d8-49c2-a295-504ee63b59a6.JPG)



### Result :
LED seven segment display is interfaced and displayed alpha numeric characters 


