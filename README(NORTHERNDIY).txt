SmarterPortSD
	(SmartPortSD Adapter With modifications by NorthernDIY)

Acknowledgements:

  This project is based upon the work of many people including:
	Robert Justice - The original SmartPortCFA project 
		http://www.users.on.net/~rjustice/SmartportCFA/SmartportCFA.htm

	Andrea Ottaviani - The Arduino/SD port of Robert's project
		http://www.users.on.net/~rjustice/SmartportCFA/SmartportSD.htm

	Katherine Stark - Added FAT support to Andrea's project
		https://gitlab.com/nyankat/smartportsd

	Chris Tersteeg - Provided the initial PCB layout for the project
		https://github.com/djtersteegc/smartportsd-nano-shield


The PCB files in this repository are meant to be imported into EasyEDA.


Tested on IIGS ROM03, should work with ROM01 and IIC.

This is supposed to work as a set of drives after a 3.5 drive, but
in my experience this adapter does not boot if placed after the
disk drive in the smart port chain.
(I have no bootable 3.5" disks to test with)

You can emulate up to 5 32mb prodos partitions/devices.  The original
SmartPortSD firmware may have allowed larger partitions if formatted
as HFS but I have not verified this.  I have modified the code to reduce
memory consumption on the AVR, but there is not much room to add more features

For V1.18 (without debug output):
Number of disks presented directly influences free memory (RAM).
1 Disk : 1524/2048 Bytes used.
2 Disks: 1571/2048 Bytes used.
3 Disks: 1618/2048 Bytes used.
4 Disks: 1665/2048 Bytes used.
5 Disks: 1712/2048 Bytes used.  //This might actually be too many! Not thoroughly tested!

Can't present more than 5 disks as stack crashes into heap.
	
More features could be added if the number of emulated devices is reduced.

Debug output is made optional as it does slow things down and it does consume
additional memory.

Very much a work in progress project.

Disk transfer rates aren't spectacular, but I assume roughly comparable to what a smartport based
HD is capable of.

SmartPort.cfg information:
  First Digit	-	Boot Partition Selection (0-4)
  Second Digit	-	Maximum # of partitions to present to the IIGS. (1-5)

  example contents (no quotes): "12"  - Boots from second drive, presents 2 drives to computer.

Assembly Information:

Wiring guide available here: https://djtersteegc.github.io/smartportsd-nano-shield/assembly.html

*NOTE* DB19 connectors don't really exist anymore!  I recommend modifying a DB25 as follows:

	1)Either drill the rivets that hold the metal shell, or bend the tabs back and forth till
	  the metal fatigues and snaps off.
	2)Pull out pins 11,12,13 & 23, 24, 25.
	3)Cut the plastic diagonally from the pin holes of 22 through 11.  Be careful,
	  it is easy to shave off some extra with a razor blade, but the plastic will crack if you
	  aren't careful.  Tool Recommendations: Aviation tin snips or a dremel with cutting disk.
	4)Solder your wires.

Recommended Wiring pattern if using a 9pin flat ribbon (old serial cable):
Wire		Connector Pin #		J2 Pin #
1		10			9	(Top of board if leds are on the right)
2		1			8
3		6			7
4		19			6
5		14			5
6		13			4
7		12			3
8		11			2
9		18			1	Square Hole - Bottom of board if leds are on the right

Component values are listed on the board's silk screen - otherwise see the schematic
Uses an arduino NANO oriented such that the usb port faces the bottom of the board (leds on the Right side of board)
SD card adapter as discussed https://djtersteegc.github.io/smartportsd-nano-shield/assembly.html
LED resistor values have been increased as we really don't need full 20ma into each led to indicate things.

Don't forget to install JP1!  Your arduino will light up without it (sort of), but that is due to power flowing
into the arduino through the IO ports.  It won't work though!