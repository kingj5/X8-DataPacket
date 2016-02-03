# X8-DataPacket
Repository for keeping track of data packets needed.

Battlestation -> Main Micro Packet
----------------------------------
Byte # |   Description  | Type
-------|----------------|-------------------
  00   |     Header     | 0x12 - 18 decimal
  01   |     Control    | 0x01 == Control
  02   |       X-1      | Signed int (2 bytes), High order
  03   |       X-2      | Signed int (2 bytes), Low  order
  04   |       Y-1      | Signed int (2 bytes), High order
  05   |       Y-2      | Signed int (2 bytes), Low  order
  06   |       Z-1      | Signed int (2 bytes), High order
  07   |       Z-2      | Signed int (2 bytes), Low  order
  08   |     Roll-1     | Signed int (2 bytes), High order
  09   |     Roll-2     | Signed int (2 bytes), Low  order
  10   |     Pitch-1    | Signed int (2 bytes), High order
  11   |     Pitch-2    | Signed int (2 bytes), Low  order
  12   |      Yaw-1     | Signed int (2 bytes), High order
  13   |      Yaw-2     | Signed int (2 bytes), Low  order
  14   |    Solenoids   | 1 byte (2 bits per solonoid)
  15   | Hydaulics Pump | 1 byte (0 to 255 PWM Val)  
  16   |     LEDs       | 1 byte (0 to 255 PWM Val)  
  17   |   Thrusters    | 1 byte - Controls thruster's on status
  18   |  PID Control   | 1 byte - bool for pid / manual control
  19   | PID Tuning A-1 | Signed int (2 bytes), High order
  20   | PID Tuning A-2 | Signed int (2 bytes), Low  order
  21   | PID Tuning B-1 | Signed int (2 bytes), High order
  22   | PID Tuning B-2 | Signed int (2 bytes), Low  order
  23   | PID Tuning C-1 | Signed int (2 bytes), High order
  24   | PID Tuning C-2 | Signed int (2 bytes), Low  order
  25   |  PID Pivot X   | Signed int (1 byte)
  26   |  PID Pivot Y   | Signed int (1 byte)
  27   |  PID Pivot Z   | Signed int (1 byte)
  28   |   CRC8 Check   | Use 0xD5 as polynomial
  29   |   Tail Byte    | 0x13 - 19 decimal  
  
Always set command to 0x01. In the future, there will be further options to program options are ask for certain data using this byte, but nothing is set yet.  
  
  
C :: CRC-8 Checksum Code
------------------------
```c
//loops over array of bytes and returns checksum
//skips first and last two bytes (header, checksum, tail)
char crc8(char bytes[], int size) {
  char crc = 0;
  char val;
  char mix;
  for (int i = 1; i < size - 2; ++i) {
    val = bytes[i];
    for (int j = 8; j; --j) {
      mix = (crc ^ val) & 0x01;
      crc >>= 1;
      if (mix) {
        crc ^= 0xD5;
      }
      val >>= 1;
    }
  }
  return crc;
}
```
