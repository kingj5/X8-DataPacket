# PowerBoard CAN Communication

Main Micro -> PowerBoard Micro (Packet 1)
-----------------------------------------
Byte # |   Description   | Type
-------|-----------------|------
  00   |   Packet Type   |  0x01
  01   |       X-1       |	Signed int (2 bytes), High order
  02   |       X-2       |  Signed int (2 bytes), Low order
  03   |       X-1       |	Signed int (2 bytes), High order
  04   |       X-2       |  Signed int (2 bytes), Low order
  05   |       X-1       |	Signed int (2 bytes), High order
  06   |       X-2       |  Signed int (2 bytes), Low order
  07   |     Pump ESC    |  1 byte (0 to 255 PWM Val)
  
Main Micro -> PowerBoard Micro (Packet 2)
-----------------------------------------
Byte # |   Description   | Type
-------|-----------------|------
  00   |   Packet Type   |  0x02
  01   |     Roll-1      |	Signed int (2 bytes), High order
  02   |     Roll-2      |  Signed int (2 bytes), Low order
  03   |     Pitch-1     |	Signed int (2 bytes), High order
  04   |     Pitch-2     |  Signed int (2 bytes), Low order
  05   |      Yaw-1      |	Signed int (2 bytes), High order
  06   |      Yaw-2      |  Signed int (2 bytes), Low order
  07   |   PID Control   |  1 byte - bool for pid / manual control
  
Main Micro -> PowerBoard Micro (Packet 3)
-----------------------------------------
Byte # |  Description  | Type
-------|---------------|------
  00   |  Packet Type  |  'T'
  01   |  Low order    | Unsigned int (1 byte)
  02   |  Middle order | Unsigned int (1 byte)
  03   |  High Order   | Unsigned int (1 byte)
  04   |  Unused       | N/A
  05   |  Unused       | N/A
  06   |  Unused       | N/A
  07   |  Unused       | N/A
  
Reassigning motor methodology:
The 8 motors are each represented by 3 bits spread among 3 bytes.  To retrieve the values of the motors to be reassigned, the following code is used:
val = 4 * (high && 1 << i) + 2 * (mid && 1 << i) + (low && 1 << i);
