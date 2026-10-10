# Lab 2 - Disk and Network Throughput 
| Source (read)        	| Destination (write)  	| Path          	| Command                                                       	| Data rate  	|
|----------------------	|----------------------	|---------------	|---------------------------------------------------------------	|------------	|
| local disk on bowie  	| local disk on bowie  	| internal bus  	| `for x in {1..4}; do time cp 1GB.dat 1GB.dat.copy; done` 	| 293 MB/sec 	|
| local disk on bowie  	| `/dev/null` on bowie   	| internal bus  	| `for x in {1..4}; do time cp 1GB.dat /dev/null ; done`   	| 3.4 GB/sec 	|
| local disk on hopper 	| local disk on hopper 	| internal bus  	|                    `for x in {1..4}; do time cp 1GB.dat 1GB.dat.copy; done`  	|   295.159 MB/sec   	|
| local disk on hopper 	| `/dev/null` on hopper  	| internal bus  	|                       `for x in {1..4}; do time cp 1GB.dat /dev/null ; done`|2.257 GB/sec	|
| local disk on bowie  	| local disk on hopper 	| 1Gb network   	|                         `for c in {1..4}; do time scp 1GB.dat hopper:~/gig; done`| 16.75 MB/sec |
| local disk on bowie  	| local disk on hopper 	| 10Gb network  	|                      `for c in {1..4}; do time scp 1GB.dat 10.10.10.1:~/gig; done`|125.443 MB/sec|
| local disk on hopper 	| `/dev/null` on bowie   	| 1Gb network   	|`for c in {1..4}; do time scp 1GB.dat bowie:/dev/null; done` | 16.940 MB/sec           	|
| local disk on hopper 	| `/dev/null` on bowie   	| 10Gb network  	|`for c in {1..4}; do time scp 1GB.dat 10.10.10.15:/dev/null; done`|            	|
