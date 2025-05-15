In this project, you'll implement a program that reads the content from one regular hard disk drive and writes it to an array with N hard disk drives arranged in a RAID 5. You must read the input and write the output to pre-specified files that simulate the content of a disk. Please follow the format precisely, otherwise your solution will not be considered correct.

Task description
You must create a program that receives N+4 command-line arguments:

The first argument indicates the block size B in bytes for all disks (1 <= B <= 2^12).
The second argument is the number of bytes J stored in the regular hard disk (1 <= J <= B*10^4). J is always a multiple of B.
The third argument is the path to the file with the content of the regular hard disk.
The fourth argument is the number of bytes K that can be stored in each disk in the RAID 5 array (1 <= K <= B*10^4, K*(N-1) >= J). K is always a multiple of B.
The next N arguments indicate the path to the files that will store the content of the disks in the RAID 5 array, sorted by disk index.
All files will have content in hexadecimal, where a byte is represented by two characters in the set {0-9,a-f}. Your program must create the files representing the content of the disks in the RAID 5 array from the content of the regular hard disk. This is how blocks are organized in a RAID 5 array with 4 disks:
<img width="211" alt="image" src="https://github.com/user-attachments/assets/dd68aa02-405c-444b-bf4e-49d9aa516680" />
P represents parity block, which must be computed by the XOR of the other blocks in the same row of the table above. Numbers represent indices of blocks from the regular hard disk, with block 0 containing the first B bytes, block 1 containing the next B bytes, and so on. If K*(N-1) > J, fill the remaining non-parity blocks with zeros.

Code will be tested in a machine with 1 CPU core and 1.5GB of RAM.

TEST CASES:
Command: $ ./raid5 1 4 reg_disk.txt 3 disk0.txt disk1.txt disk2.txt disk3.txt
Input: 
reg_disk.txt
--
01020304
Output:
disk0.txt
--
010000

disk1.txt
--
020000

disk2.txt
--
030400

disk3.txt
--
000400

Command: $ ./raid5 1 4 reg_disk.txt 3 disk0.txt disk1.txt disk2.txt
Input:
reg_disk.txt
--
01020304
Output:
disk0.txt
--
010400

disk1.txt
--
020700

disk2.txt
--
030300

Command: $ ./raid5 2 8 reg_disk.txt 6 disk0.txt disk1.txt disk2.txt
Input:
reg_disk.txt
--
0102030450607080
Output:
disk0.txt
--
010270800000

disk1.txt
--
030420e00000

disk2.txt
--
020650600000
