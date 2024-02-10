Affected Version:
libming 0.4.8 04aee52363688426eab74f5d6180c149654a6473

Vulnerability Description:
The vulnerability is a memory leak bug located at line 531 of the file /libming/src/actioncompiler/listaction.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

libming download address:
https://github.com/libming/libming.git

1.At line 531 of the printActionRecord function in the file /libming/src/actioncompiler/listaction.c, the printf function is used to output the string returned by the readString function, as shown in the following image:

![image](https://github.com/LuMingYinDetect/libming_defects/blob/main/libming_1.png)

2.At line 93 of the readString function, a string pointer named buf is defined. At line 95, the malloc function is used to allocate a block of dynamic memory for it. Finally, at line 115, this pointer is returned, as shown in the following image:

![image](https://github.com/LuMingYinDetect/libming_defects/blob/main/libming_2.png)

3.After the program outputs the string returned by the readString function at line 531, the dynamic memory area pointed to by the string returned by readString is no longer used and is not released, thereby causing a memory leak vulnerability, as shown in the following image:

![image](https://github.com/LuMingYinDetect/libming_defects/blob/main/libming_3.png)
