# Masters_Thesis
as part of my Masters study, I will be using this Repository to work on my final Thesis.
today june 4th, 2023 I have decided to work on Emperical research in area of VPN Server or Cloud Server specific to Raspberry Pi. 
Recent add (12Jun2023)
Open source project area
 bug tracking in Debian.
Currently working on "Linux approach to COTS avionics software offerings" inspired by ELISA (Enabling Linux In Safety Applications). Especially in relation to real-time Linux in embedded applications As opposed to the low-latency Kernel.
 - according to studies, temporal partitioning mechanisms need to be encorporated to linux partition management inorder for it to comply with ARINC 653 SAFETY NEEDS.
Temporal partitioning implementation on Real-Time Linux OS for Embedded Software

- ELISA (Enabling Linux in Safety Applications) is a comprehensive effort in the Linux community to enable Linux qualify for DO-178B/178C. 
- DO-178B/178C a guideline dealing with the safety of safety-critical software used in certain airborne systems.
- So far Linux OS has been used extensively on non-safety Aviation applications such as IFE(In-Flight Entertainment) systems.
- real-time OS is a base line requirement in safety applications related to Medical Devices, Automotive and Aviation because of its deterministic nature. Linux released the preempt-rt patch for programs demanding real-time operation.
- ARINC 653 (vionics Application Software Standard Interface) is a specification for space and time partitioning in safety-critical avionics RTOS(real-time operating systems).
        * in part one of the 3 PART publication of ARINC 653, it states that applications (even with different criticality
        levels) to execute on the same hardware with no undue influence on one another, spatially or temporally.[1]
        * In integrated real-time systems it is important to avoid temporal faults that might occur on the processor as a common computational resource for multiple applications.[2]


        Reference

        1. Aeronautical Radio, Inc., Avionics application software standard interface part 1—Required services, ARINC Specification 653P1–3 (Annapolis, MD:Airlines Electronic Engineering Committee, November 2010).