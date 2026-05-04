run embedded linux board need minimum of 4 software components:
RBL (Runs out of ROM) --> SPL/MLO (Runs out of Internal SRAM) --> U-Boot (Runs out of DDR) --> Linux kernel (Runs out of DDR) --> RFS (SD/Flash/Network/RAM/e-MMC)
- the RBL stands for the ROM Boot Loader (this boot loader very tiny(176kb) & has limited functionalities): Load & excute the second stage boot loader
form internal of SOC Create by TI can not change this boot loader
- the SPL stands for the Secondary Program Loader sometime it's also call MLO (Memory loader): Load & excute the third stage boot loader (boot from DDR of the board)
- U-Boot load & excute the Linux kernel from DDR memory
