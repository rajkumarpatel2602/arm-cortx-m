# arm-cortx-m

#inpyjama content.

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

M4F arch
WIC to make processor wake up from deep sleep, it runs on RTC or WatchDog.
![image](https://github.com/user-attachments/assets/025da75d-bf23-46bc-afab-318167a79423)
Pinkish shade things are optional [at implementation level, it's upto vendor if they want to expose or not?].

ETM - embedded trace macrocell, used for tracing, If we want to trace, what's getting executed and when, and used for coverage analysis, or which function run most time.
it's used for debug and trace.

Debug Access Port is for debugging, JTAG or SWD // serial wired debugger. 

MMU for segrate memroy based on privilege level. RTOS kernel wants higher priviledge memory. MPU is essenstially a table, which has start and end address of mem region, and set attributes as WO, RO, WRE, etc. // these are priviledge levels. If monolithic, means no kernel, then no such privilege settings requried.

Cortx-M has thread mode and handler mode. Thread mode, some HW features are disabled, and limited instruction. Handler mode has full access.

Systick, is 24bit down counter. used for OS perspective. OS needs timer base, putting it on core, helps vendors (STM, NXP, Microchip) to not need to provide interface and use on-core systick.

![image](https://github.com/user-attachments/assets/80b26be4-40bd-4d7a-8d00-fc4852acf4e2)

Endian ness. 0xabcdef00 ... 00 is LSB here, so it will go to lower address, and ab is MSB so it will go to higher address.
00  | 01 | 02 | 03
00    ef   cd   ab
easy to snatch a LSB or a short, or whole integer, just by having a pointer at 0x00 location. 

big endian // LSB goes in higher address. easy to read for human. so all protocol uses big endian in transmission. even if we bundle header in MSB, it's good for signaling to receiver.

00 | 01 | 02 | 03
ab   bc   ef   00 
![image](https://github.com/user-attachments/assets/40aaa37b-1a1c-496b-8344-24b30aa9de01)

Instruction set
Thumb - 16bit -- limited register set access
ARM - 32bit
User need to switch modes.
Thumb2 support both Inst. set. HW automatically detects type of instructor and chagnes accordingly.
![image](https://github.com/user-attachments/assets/3016d9b6-3832-4e6f-be3b-04a469a8b8bf)

cortx-m4 has 16 regs, 13 General purpose. 3 special purpose [programmer doesn't have access to it. R0-R12 have all access to user, CPU can modify 3 for it's usage.]
R13 SP -- stack pointer
R14 LR -- Link register
R15 PC -- program counter

Thread and handler, SP has Main sp, and process sp.
main sp (msp): Handler mode can also use psp
process sp (psp): Thread mode
control register desides which sp to use. It's upto kernel to set bit in control register, and based on that msp or psp will be used.
If there's no kernel user concept then, keep on using MSP and just keep on going with PSP. CPU always use R13, SP.

PSR (Program status register): status of registers, ALU, INTR


![image](https://github.com/user-attachments/assets/e1b2d1ac-5feb-4de4-b096-3597383fdf95)

![image](https://github.com/user-attachments/assets/15fd6bd4-9fba-4467-9675-0bc4d35eff4c)

![image](https://github.com/user-attachments/assets/f44ba0e0-d685-4f50-b7d7-7e46238d60eb)

4 regs -- PSR , it's made up of APSR, IPSR, EPSR.

Purpose of SP

![image](https://github.com/user-attachments/assets/5bf0afff-124f-4f9b-95dd-d0c10cf2a3b8)

