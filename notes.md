* Empirical Research in Software Engineering
    Introduction
        Main Points
            Empirical studies such as surveys, systematic reviews and experimental studies, help software practitioners to scientifically assess and validate the tools and techniques in software development.

            Empirical study is an attempt to compare the theories and observations using real-life data for analysis.

                    The empirical studies involve the following steps

                            formation of research question
                                * what are COTS avionics offerings?
                                * what are linux's approach been in the past?
                                * what similarities do linux's approach & COTS avionics offerings have in common?
                                * what differences do linux's approach & COTS avionics have between them?
                            formation of research hypothesis
                                * a recurring statement that has been coming is the importance of Data Coupling and Control Coupling in avionics Software.[10]
                                * what is the system requirement and what are the types of system requirements
                                    - a coupling experiment performed on Software coupling and software performance states that "relative performace of systems implemented using different software coupling is platform dependent.(i.e Windows Vs Linux Vs Mac)
                                * Is Linux reliable interms of CyberSecurity? 
                                    - Linux is considered to be more secure than other operating systems, such as windows, becuase it is less susceptable to viruses and other forms of malware. this makes it an attractive option for cybersecurity experts who need to protect sensitive information and networks from cyber threats.[1] 
                                * what are the challenges involved in running Linux in Safety-critical systems and building products based on Linux?
                                    - The primary challenge is selecting Linux components and features that can be evaluated for safety and identifying gaps where more work is needed to evaluate safety sufficiently[4]
                                * what are Basic Operating System Concepts of Linux?
                                    - the most important program in the set is called the kernel. It is loaded into RAM when the system boots and contains many critical procedures that are needed for the system to operate.[6]
                                    - To ensure safe protection mechanisms, operating systems must use the hardware protection associated with the CPU privileged mode. Otherwise, a user program would be able to directly access the system circuitry and overcome the imposed bounds. Unix is a multiuser system that enforces the hardware protection of system resources.[7]
                                    - Kernel Architecture
                                    As stated before, most Unix kernels are monolithic: each kernel layer is integrated into the whole kernel program and runs in Kernel Mode on behalf of the current process. In contrast, microkernel operating systems demand a very small set of functions from the kernel, generally including a few synchronization primitives, a simple scheduler, and an interprocess communication mechanism. Several system processes that run on top of the microkernel implement other operating system–layer functions, like memory allocators, device drivers, and system call handlers. [8]

                                        # The first approach, similar to a monolithic kernel architecture, involves constructing the entire house as one solid structure. You start with the foundation, then build the walls, floors, and roof all together. Everything is tightly integrated and functions as a single unit. In this case, you don't have separate rooms or sections; instead, every part of the house is interconnected. If you want to change or fix something in one room, you need to modify the entire structure. Similarly, in a monolithic kernel, all the kernel layers are tightly integrated into a single program that runs in Kernel Mode.

                                        # Now, let's consider the second approach, which is analogous to a microkernel architecture. Instead of building the entire house as one unit, you divide it into smaller components or modules. You have a foundation module, wall modules, floor modules, and roof modules. Each module has its specific function and can be modified or replaced independently. For example, if you want to change the flooring material in one room, you can remove and replace the floor module without affecting the rest of the house. In a microkernel operating system, the kernel provides only a minimal set of functions, such as synchronization, scheduling, and interprocess communication. Other operating system functions, like memory allocation, device drivers, and system call handling, are implemented as separate processes that run on top of the microkernel.

                                        # In summary, a monolithic kernel architecture is like building a house as a single integrated structure, where all the components are tightly connected. On the other hand, a microkernel architecture is like building a house with modular components, allowing for greater flexibility and independence in modifying or replacing specific parts of the system without affecting the entire structure.

                                            * To achieve many of the theoretical advantages of microkernels without introducing performance penalties, the Linux kernel offers modules. A module is an object file whose code can be linked to (and unlinked from) the kernel at runtime. The object code usually consists of a set of functions that implements a filesystem, a device
                                            - Platform independence Even if it may rely on some specific hardware features, a module doesn’t depend
                                            on a fixed hardware platform. For example, a disk driver module that relies on the SCSI standard works as well on an IBM-compatible PC as it does on Hewlett-Packard’s Alpha.


                                * what is a COTS Avionics Software?
                                    - formal term for commercial items, including services, available in the commercial marketplace that can be bought and used under government contract.[2] For example, Microsoft is a COTS software provider. Goods and construction materials may qualify as COTS but bulk cargo does not. Services associated with the commercial items may also qualify as COTS, including installation services, training services, and cloud services.[3]

                                * why is COTS Software important in Avionics?
                                    - COTS’ appeal is strong. Although the price can run into millions of dollars for a complex project, proponents say COTS cuts development costs and time to market, focusing engineering talent on applications development. Quality is maintained, they say, because the certification material is consistent for customers building different applications.


                                * how are COTS avionics Software Regulated?
                                    - In January 1993, the FAA distributed Advisory Circular 20-115B recognizing DO-178B as the preferred guideline
                                    document to be used for software development activities for embedded software on avionics systems.

                                    - the SANS Institute published a survey of 700 IT and security professionals in December 2012 that found that only 14% of companies perform security reviews on every commercial application brought in house, and over half of other companies do not perform security assessments. Instead companies either rely on vendor reputation (25%) and legal liability agreements (14%) or they have no policies for dealing with COTS at all and therefore have limited visibility into the risks introduced into their software supply chain by COTS.[5]

                                    software as safety-critical if at least one of the following criteria is satisfied [9]:
                                        1. It resides in a safety-critical system (as determined by a hazard analysis) AND at least one of the following: 
                                            & Causes or contributes to a hazard.
                                            & Provides control or mitigation for hazards.
                                            & Controls safety-critical functions. 
                                            & Processes safety-critical commands or data. 
                                            & Detects and reports, or takes corrective action, if the system reaches a specific hazardous state.
                                            & Mitigates damage if a hazard occurs.
                                            & Resides on the same system (processor) as safety-critical software.
                                        2. It processes data or analyzes trends that lead directly to safety decisions.
                                        3. It provides full or partial verification or validation of safety-critical systems, including hardware or software systems.


                                [1] https://link.springer.com/chapter/10.1007/978-3-030-02683-7_25
                                [2] https://www.acquisition.gov/far/2.101
                                [3] https://web.archive.org/web/20170130041945/https://www.acquisition.gov/far/html/Subpart%202_1.html#wp1158534
                                [4] https://elisa.tech/advancing-open-source-safety-critical-systems-whitepaper
                                [5] https://www.qualys.com/docs/sans-enterprise-application-security-policy-survey-report.pdf
                                [6] Daniel P. Bovet, Marco Cesati Ph.D. - Understanding the Linux Kernel, Third Edition-O'Reilly Media (2005) p.9 (27 of 944)
                                [7] Daniel P. Bovet, Marco Cesati Ph.D. - Understanding the Linux Kernel, Third Edition-O'Reilly Media (2005) p.9 (27 of 944)
                                [8] Daniel P. Bovet, Marco Cesati Ph.D. - Understanding the Linux Kernel, Third Edition-O'Reilly Media (2005) p.11 (29 of 944)
                                [9] Leanna Rierson - Developing Safety-Critical Software_ A Practical Guide for Aviation Software and DO-178C Compliance-CRC Press (2013) p.32 of 728
                                [10] https://www.rapitasystems.com/files/MC-WP-011%20DO-178C%20Verification_5 p.17 (20 of 70)