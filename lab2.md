# Lab 2 - Disk and Network Throughput 
This lab is designed to reinforce the importance of the memory hierarchy and the tools and techniques used to measure the performance of it. It also contains an exploration of the trip cost vs. item cost conundrum. 

Begin by figuring-out the commands you need to complete the chart below, then run the commands, collect the data, do the math, and complete the chart. Use a 1 GB file of random data for each of your tests. Always run a command at least 3 times and then average the results to obtain a given measurement. Calculate the data rate by determining how much was moved in each operation, what the average time per operation was, and then do the division. Beware of excess precision. The two rows I completed contain accurate data, you can test your work by comparing your values with the chart for those two. Notice that my command just copies the same file over itself rather than making lots of files.

| Source (read)        	| Destination (write)  	| Path          	| Command                                                       	| Data rate  	|
|----------------------	|----------------------	|---------------	|---------------------------------------------------------------	|------------	|
| local disk on bowie  	| local disk on bowie  	| internal bus  	| `for x in {1..4}; do time cp 1GB.dat 1GB.dat.copy; done` 	| 293 MB/sec 	|
| local disk on bowie  	| `/dev/null` on bowie   	| internal bus  	| `for x in {1..4}; do time cp 1GB.dat /dev/null ; done`   	| 3.4 GB/sec 	|
| local disk on hopper 	| local disk on hopper 	| internal bus  	|                                                               	|            	|
| local disk on hopper 	| `/dev/null` on hopper  	| internal bus  	|                                                               	|            	|
| local disk on bowie  	| local disk on hopper 	| 1Gb network   	|                                                               	|            	|
| local disk on bowie  	| local disk on hopper 	| 10Gb network  	|                                                               	|            	|
| local disk on hopper 	| `/dev/null` on bowie   	| 1Gb network   	|                                                               	|            	|
| local disk on hopper 	| `/dev/null` on bowie   	| 10Gb network  	|                                                               	|            	|

## Notes: 
- The time for any given transfer should be the average time of 3 or more operations, never fewer than 3.
- Use a 1 GB file for all of these tests.
- 159.28.23.0/24 (cluster subnet) are 1Gb IP interfaces 
- 159.28.22.0/24 (CS subnet) are 1Gb IP interfaces 
- 10.10.10.0/24 (both subnets) are 10Gb IP interfaces 

## Useful commands:
- `time <command>` - Displays the real, user, and system times for <command>. We care about real in this context.
- `dd if=/dev/random of=1GB.dat count=2M` - Makes a 1 GB file out of random data
- `dd if=/dev/random of=1MB.dat bs=1024 count=1024` - thoughts?
- `ip a` - will show you the interfaces to look at, e.g. enp4s0f0 (look for ones with IP numbers in the ranges above)
- `/sbin/ethtool enp4s0f0` - will show you the physical details of the interface, e.g. the speed 

Automation will make this much easier, and help you to produce a much better result; practice it. If you are taking, or have taken [C,D]S-[3,4]88, this is the perfect place for a learning loop. If you haven't, ask about them in class. 

## Deliverables
Assemble a single well formatted document that contains:
1. Your completed version of the chart above.
2. Is there a difference between the internal bus performance of hopper compared to bowie? If there is, why might that be? Explain this in your document including any commands you used to figure it out. 
3. An answer to this question; how much more efficient is it to move a single 10 GB file from local storage on hopper to local storage on bowie over the 1Gb network fabric compared to moving 1,000 files each of which are 10 MB in size? Document the experiment you design and conduct to determine this, that is the commands, timing data, and calculations. 
4. Clean-up after yourself, delete all the data files you create to do this.
5. Work on the extra credit.
6. Put any scripts that you developed for this lab into the document.
7. Upload a PDF of the completed document to the appropriate Moodle assignment. 

$Extra$ $Credit$: Moving a large bunch of files from one machine to another is a common task, and often is made more efficient by the use of a tarpipe. Correctly constructed, a tarpipe can remove the overhead of having to create an archive on the local machine, copy that single big file to the remote machine, and then unpack it, to obtain the trip-item cost efficiency of a single large file transfer. Figure-out what a tarpipe is and how to use it to move a large number of files from one machine to another machine efficiently. 