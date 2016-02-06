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
  07   |       N/A       |  Empty
