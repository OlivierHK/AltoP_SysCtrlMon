# AltoP_SysCtrlMon

##Summary

A C#/.Net Application for controlling and monitoring the Alto System.

The communication is using UART, and is between the host computer and the on-board Arduino.

- Real-time Monitoring all powers and temperatures on the board, and from all available sources (Arduino's ADC, FPGA's Sysmon, TPS,...)
- Real-time monitor status and Error from FPGA's Sysmon registers and TPS's registers.
- Protection section let user to set extremum Voltage/Temperature values, and action if triggered.
- Real-time control and monitor of the board power supplies and FPGA's control/boot/status signals.
- Control of the soft-reset of the FPGA's firmware.

=> `nPROGRAM_B_FPGA_x` should never be de-asserted during FGPA's usage in high frequency, as it may lead to power dump and FPGA damage. it will clear the FPGA's firmware.

![screenshot](https://github.com/user-attachments/assets/94f9f95a-acca-43c9-80a7-54678f94ba71)

##usage

1. Press `refresh Port` to list all COM ports available.
2. Select the COM port from the list where the on-board Arduino is connected, and select 500000 as Baud Rate.
3. Press `Connect`.
4. Tick `Enable PMBus monitoring` to read the TPS registers. This will slow down the data refreahing rate.
5. Tick `Enable I2C Sysmon Monitoring` to read the FPGA's Sysmon registers. This will slow down the data refreahing rate.
6. Press any `Reset Min/Max` button to clear latched Min/Max values. This have no effect on the board.
7. If TPS errors are present, those should be fixed and clear first before being able to restart VccINT/VccINTIO_BRAM.
8. Protection values and acion will be stored inside the Arduino and kept, even the Application is disconnected.
9. The Ardiuno firmware is handling automaticaly the board power sequence and FPGA's wake up, but user should still release manually the soft RST_FPGA_x signal before launching a Miner application.
10. `nRST_FPGA_x` is safe to toggle at any time, even during heavy load, as it will trigger FPGA's internal clock ramp-down before puting the FPGA's firmware under reset.
11. To manually power-reset the FPGA, make sure to follow the FPGA's power sequence to avoid damage.
12. Pressing `Disconnect` button will not stop or hang the board/FGPA. it just close the COM port and stop the data transfer between the Arduino and the Application. it can be reconnect at anytime without any side effect.
13. de-asserting the `nPROGRAM_B_FPGA_x` will clear the FPGA's firmware. Re-asserting it will trigger the FPGA programming from its SPI's Flash. it takes ~30 second and is successfully done when `Done` signal go green.

##Code & Project
Please contact the author at olivier.faurie.hk@gmail.com for the C#/.NET project.
