# AHB_to_APB_Bridge
OVERVIEW OF THE PROJECT:
The Advanced Microcontroller Bus Architecture (AMBA) specification defines an on-chip communications standard for designing high-performance embedded microcontrollers. It is developed by ARM.
Three distinct buses are defined within the AMBA specification:
•	Advanced High-performance Bus (AHB):
The AMBA AHB is for high-performance, high clock frequency system modules. The AHB acts as the high-performance system backbone bus. AHB supports the efficient connection of processors, on-chip memories and off-chip external memory interfaces with low-power peripheral devices.

•	Advanced System Bus (ASB):
The AMBA ASB is for high-performance system modules. AMBA ASB is an alternative system bus suitable for use where the high-performance features of AHB are not required. ASB also supports the efficient connection of processors, on-chip memories and off-chip external memory interfaces with low-power peripheral devices.

•	Advanced Peripheral Bus (APB):
The AMBA APB is for low-power peripherals like UART, Timer, Keyboard etc;  AMBA APB is optimized for minimal power consumption and reduced interface complexity to support peripheral functions. 

![image](https://github.com/YRanjith19/AHB_to_APB_Bridge/assets/141166050/0a76a910-7357-46e1-94f9-162f7300ea39)
![image](https://github.com/YRanjith19/AHB_to_APB_Bridge/assets/141166050/a174acbb-587c-4326-be57-decdc161f1a8)


BRIEF SUMMARY  OF FUNCTIONAL BLOCKS	
•	AHB MASTER INTERFACE:
	As its name suggests, It acts as an interface to the AHB_to_APB bridge.
	 This block is used to generate the operations  like single read, single write, burst read and burst write.
	It also generate the type of transaction ie, SEQ, NONSEQ, BUSY, IDLE.
•	AHB to APB bridge:
	It basically converts the AHB transaction into corresponding APB transactions.
	There are 2 sub-blocks ie AHB slave interface and APB controller.
	AHB Slave Interface does the pipelining of Hwrite, Haddr, Hwdata signals taken from the Master. It also generate the valid and tempselx signals which are given to the APB controller.
	APB Controller is a FSM (finite state machine) which converts the AHB to APB transactions using the signals from the AHB slave interface .


•	APB INTERFACE:
	It acts as an interface between bridge and the Apb peripheral devices.
	It is a combinational circuit.
AMBA AHB SIGNALS:
Name	Description
HCLK	This clock times all bus transfers. All signal timings are related to the rising edge of HCLK.
HRESETn	The bus reset signal is active LOW and is used to reset the system and the bus.This is the only active LOW signal.
HADDR[31:0]	The 32-bit system address bus.
HTRANS[1:0]	Indicates the type of the current transfer, which can be NONSEQUENTIAL, SEQUENTIAL, IDLE or BUSY.
HWRITE	When HIGH this signal indicates a write transfer and when LOW a read transfer.
HSIZE[2:0]	Indicates the size of the transfer, which is typically byte (8-bit), halfword (16-bit) or word (32-bit). The protocol allows for larger transfer sizes up to a maximum of 1024 bits.
HBURST[2:0]	Indicates if the transfer forms part of a burst. Four, eight and sixteen beat bursts are supported and the burst may be either incrementing or wrapping.
HWDATA[31:0]	The write data bus is used to transfer data from the master to the bus slaves during write operations. A minimum data bus width of 32 bits is recommended.
HSELx	Each AHB slave has its own slave select signal and this signal indicates that the current transfer is intended for the selected slave. This signal is simply a combinatorial decode of the address bus.
HRDATA[31:0]	The read data bus is used to transfer data from bus slaves to the bus master during read operations. A minimum data bus width of 32 bits is recommended.
HREADY	When HIGH the HREADY signal indicates that a transfer has finished on the bus. This signal may be driven LOW to extend a transfer. 
HRESP[1:0]	The transfer response provides additional information on the status of a transfer. Four different responses are provided, OKAY, ERROR, RETRY and SPLIT.

AMBA APB SIGNALS:
Name	Description
PCLK	The rising edge of PCLK is used to time all transfers on the APB.
PRESETn	The APB bus reset signal is active LOW and this signal will normally be connected directly to the system bus reset signal.
PADDR[31:0]	This is the APB address bus, which may be up to 32-bits wide and is driven by the peripheral bus bridge unit.
PSELx	A signal from the secondary decoder, within the peripheral bus bridge unit, to each peripheral bus slave x. This signal indicates that the slave device is selected and a data transfer is required. There is a PSELx signal for each bus slave.
PENABLE	This strobe signal is used to time all accesses on the peripheral bus. The enable signal is used to indicate the second cycle of an APB transfer. The rising edge of PENABLE occurs in the middle of the APB transfer.
PWRITE	When HIGH this signal indicates an APB write access and when LOW a read access.
PRDATA[31:0]	The read data bus is driven by the selected slave during read cycles (when PWRITE is LOW). The read data bus can be up to 32-bits wide.
PWDATA[31:0]	The write data bus is driven by the peripheral bus bridge unit during write cycles (when PWRITE is HIGH). The write data bus can be up to 32-bits wide.


