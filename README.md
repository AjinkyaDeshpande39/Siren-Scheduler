# Siren-Scheduler
Simulated 8085,8255,8253 to create a scheduled siren


# Circuit diagram
![](https://github.com/AjinkyaDeshpande39/Siren-Scheduler/blob/main/siren_scheduler.png)

In the above circuit, you can see 2 8253 and 1 8255 are used.
The circuit was conctructed with following assumptions :

1> addresses:
1) 8253 1 : FFH
2) 8255 : EFH
3) 82533 2 : DFH

2> Modes:

- 8253 1 is used to generate proper usable clock signal and to trigger uP after 1 hr.
- 8253 2 is used to run alarm for 30 sec.
- CTR0 and CTR1 of 8253-1 IC are setup in mode3 and CTR2 in mode 2
- CTR0  of 8253-2 IC is setup in mode 1 and GATE0 will be provided by uP.

3> Working:
        In 8253-1, give CTR0 count of 10^4 such that OUT0 = CLK1 has freq 200Hz CTR1 is CTR1 is given count of 20 such that OUT1 = CLK2 has freq 10Hz.
        CTR2 is given count of 36000 such that OUT2 generates strobe after 1Hz
        In 8253-2 CLK0=10Hz, CTR0 is given count of 300 so that strobe after 30 sec generated.
        This CTR0 will be setup after after 1hr. i.e. after uP gets triggered by 8253-1. Then siren will blow up for 30sec. When counter 2 finishes and gives back strobe, siren stops...
        
        
 ### It is assumed that strobes are capable of interrupting 8085
 
 4> Calculations:
        (10,000) = 2710 H
        (20) = 14 H
        (36,000) = 8CA0 H
        (300) = 012C H
        
        - For CTR0, CW -> (00110110)2 = 36H
        - For CTR1, CW -> (01010110)2 = 56H
        - For CTR2, CW -> (10110100)2 = B4H
        - For 8255 Port A, CW -> (10001000)2 = 88H
        

Due to covid 19 situation, we were unable to perform this task on hardware :(
