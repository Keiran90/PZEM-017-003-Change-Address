# change_address_PZEM.py
Python3 script for changing the Modbus address of a PZEM-017 or 003
# check_settings_PZEM.py
Python3 script for reading the configuration of PZEM-017 or 003
<pre>
PZEM-003
PEZM-017


Specifications :

Voltage Rating:          0,05V* to 300V
  Resolution :                0,01V
  Measuring accuracy :             1%
* Under 7V, an external power supply must be used

Current Rating: PZEM-003     0,01A to 10A
        PZEM-017    0,02A to 300A*
  Resolution :                0,01A
  Measuring Accuracy :             1%

Wattage Rating:  PZEM-003  0,1kW to 3kW
                 PZEM-017 0,2kW to 90KW*
  Resolution :                0,01W
  Measuring Accuracy :             1%           
* Depending on the shunt used (50, 100, 200, 300A)

Consumption measurement:        0-9999kWh
  Resolution :                   1Wh
  Measuring Accuracy :             1%



A HIGH and a LOW alarm can be defined for the voltage.
 LOW     1V to 350V     (in 0,01V Steps)
 HIGH    5V to 350V     (in 0,01V Steps)
 Default value for LOW is 7V and for HIGH 300V

The interface is
 RS485 / MODBUS-RTU
 Baudrate :                   9600
 Data Bits :                     8
 Stopbit :                       2
 Parity :                    none

The PZEM supports the following function codes:
 0x03(3)   Reading the Configuration Registers
 0x04(4)   Reading the Measured Register
 0x06(6)   Writing the Configuration Registers 
 0x41(65)  Calibration (can only be used via address 0xF8 (248))
 0x42(66)  Reset Consumption Meter

The address can be exchanged between
 0x01(1) and 0xF7(247).
 0x00(0) is the broadcast address and
 0xF8(248) can be used to address the PZEM if only ONE device is connected to the bus. Useful to configure devices or if there is only one device anyway.

The registers that can be read out with function code 0x03 or written with 0x06:
  
 Register  |   Description                 |  Resolution
 ----------|--------------------------------|----------------------
 0x0000    |   High voltage alarm threshold |  1LSB correspond
           |   (5-350V), default is 300V    |  to 0.01V
 ----------|--------------------------------|----------------------
 0x0001    |   Low voltage alarm threshold  |  1LSB correspond
           |   (1-350V) , defalut is 7V     |  to 0.01V
 ----------|--------------------------------|----------------------
 0x0002    |   ModBus-RTU Address           |  Range is
           |                                |  0x0001 - 0x00F7
 ----------|--------------------------------|----------------------
 0x0003    |   The current range            |  0x0001  100A
           |   (only PZEM-017)              |  0x0002   50A
           |                                |  0x0003  200A
           |                                |  0x0004  300A 
           
The registers which can be read out with function code 0x04:

 Register  |   Description                 |  Resolution
 ----------|--------------------------------|-----------------------------------------
 0x0000    |   Voltage value                |  1LSB correspond to O.O1V
 -------------------------------------------------------------------------------------
 0x0001    |   Current value                |  1LSB correspond to O.O1A
 -------------------------------------------------------------------------------------
 0x0002    |   Power value low 16bits       |  1LSB correspond to O. 1W
 0x0003    |   Power value high 16 bits     |
 -------------------------------------------------------------------------------------
 0x0004    |   Energy value low 16 bits     |  1LSB correspond to 1 Wh
 0x0005    |   Energy value high 16 bits    |
 -------------------------------------------------------------------------------------
 0x0006    |   High voltage alarm status    |  0xFFFF is alarm, 0x0000 is not alarm
 -------------------------------------------------------------------------------------
 0x0007    |   Low voltage alarm status     |  0xFFFF is alarm, 0x0000 is not alarm
</pre>
 
 

