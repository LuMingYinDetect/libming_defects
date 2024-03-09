Affected Version:
libming 0.4.8 04aee52363688426eab74f5d6180c149654a6473

Vulnerability Description:
The vulnerability is a memory leak bug located at line 136 of the file /libming/util/makeswf_utils.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

libming download address:
https://github.com/libming/libming.git

Detailed information about the defect:

1.At line 96 of the file /libming/util/makeswf_utils.c, a variable named 'ac' is defined. This variable is allocated a dynamic memory area by the function newSWFAction at line 130, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/libming_defects/blob/main/libming_Memory_Leak_1.png)

2.At line 307 of the newSWFAction function, a variable named 'action' is defined. This variable is allocated a dynamic memory area by the function createEmptyAction and returned at line 311, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/libming_defects/blob/main/libming_Memory_Leak_2.png)

3.At line 270 of the createEmptyAction function, a dynamic memory area is allocated to the variable 'action' using the malloc function, and it is returned at line 280, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/libming_defects/blob/main/libming_Memory_Leak_3.png)

4.After allocating a dynamic memory area for the variable 'ac', it is passed into the SWFAction_compile function within the if statement at line 132, as illustrated in the following figure:

![image](https://github.com/LuMingYinDetect/libming_defects/blob/main/libming_Memory_Leak_4.png)

5.In the SWFAction_compile function, the variable 'ac' is named 'action', and there is no release of the dynamic memory area corresponding to 'ac' within this function, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/libming_defects/blob/main/libming_Memory_Leak_5.png)

6.When the if statement at line 132 returns false, the program returns NULL at line 136. During this process, the memory area pointed to by the variable 'ac' is not released, resulting in a memory leak defect, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/libming_defects/blob/main/libming_Memory_Leak_6.png)
