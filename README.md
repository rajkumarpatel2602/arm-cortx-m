# arm-cortx-m

#inpyjama content

ARM - Acorn risc machine, later, Advanced Risc Machine
A R M -- adnvaced(application), realtime, microcontroller core.

ISA -- instruction set architecture is a contract between software and hardware. cortx-a and cortx-x both rely on same base ISA, which is ARM V9 instruction set.
![image](https://github.com/user-attachments/assets/510ffb72-f92b-4db6-b2b3-5f239339d36f)

![image](https://github.com/user-attachments/assets/9d7ef18f-35f2-4a68-8167-efe5ceef2aa2)

![image](https://github.com/user-attachments/assets/5d01f3f8-ea39-4b01-b29b-3dbc8e0ea8e7)
RISC is load store architecture. 
Can't directly access content of an address, need to Load content in General Purpose Regs, operate on regs, and store value back to address.
Now compilers are powerful and advanced, so RISC is a way to go. 
M1 in apple is RISC based, x86 is based on CISC.

Vectored interrupt: Intrrupt comes to CPU, it gets the number, and directly look at vector table and execute function, [address registered at the address] cortx-m,
cortx-m itself implements its own IV handler, NVIC is there in cortx-m itself, but not in R, so very deterministic interrupt latency. 
TRAP: Interrupt comes to CPU, it goes to some code, code determines the actual address and then jump to that code. cortx-r and cortx-a

R for little heavy application, which can't be handled by M, and a more deterministic than M.
cortx-r virtual adressing concpet is not there, no MMU unlike cortx-M 

cortx-m has within multiple design, based on power, performance and cost.
M0, M23, M0+ are with less gate-count, and basic data processing and I/O. Low power devices.
Floating point, then M3
DSP(register with big number in it, matrix multiplication) instructor + M3 = M4

![image](https://github.com/user-attachments/assets/ebc3d0a0-ec21-4166-8ecb-cfdb35a82d15)

Hiliom core which is an accelerator used with core, for AI, ML chips, M85, M55

Trustzone:

![image](https://github.com/user-attachments/assets/e0f1f2f3-345b-4a41-85dd-fea0e0721ccf)
![image](https://github.com/user-attachments/assets/9ac8e546-6508-4c54-b2ff-1c696e631d79) separate core for secure and non-secure, but trustzone helps to save processor.


