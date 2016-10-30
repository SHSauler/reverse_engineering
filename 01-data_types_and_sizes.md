
Decimal, Binary, Hex
---------------------

|b10|b2|b16|
|---|-----|----|
|01|0001b|0x01|
|02|0010b|0x02|
|03|0011b|0x03|
|04|0100b|0x04|
|05|0101b|0x05|
|06|0110b|0x06|
|07|0111b|0x07|
|08|1000b|0x08|
|09|1001b|0x09|
|10|1010b|0x0A|
|11|1011b|0x0B|
|12|1100b|0x0C|
|13|1101b|0x0D|
|14|1110b|0x0E|
|15|1111b|0x0F|

Word sizes (x86)
-------------

size|type|register|
|---|---|---|
|4 bit|nibble|no register|
|8 bit|byte|AL|
|16 bit|word|AX|
|32 bit|double word|EAX|
|64 bit|quadruple word|MM0|
|128 bit|double quadruple word|XMM0|

Integer representation
----------------------

|kind|representation|
|---|---|
|signed|integer representing positive and negative values|
|unsigned|integer only representing positive values|


|size|names|signed|unsigned|
|---|---|---|---|
|8 bit|byte, octet, char|-128 to +127|0 to 255|
|16 bit|word, short int|-32,768 to +32,767|0 to 65,535|
|32 bit|double word, int|-2,147,483,648 to +2,147,483,647|0 to 4,294,967,295|
|64 bit|quadruple word, long int|−9,223,372,036,854,775,808 to +9,223,372,036,854,775,807|0 to 18,446,744,073,709,551,615|
