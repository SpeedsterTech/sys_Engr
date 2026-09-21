# Lab 2 - Disk and Network Throughput 

| Source (read)        	| Destination (write)  	| Path          	| Command                                                       	| Data rate  	|
|----------------------	|----------------------	|---------------	|---------------------------------------------------------------	|------------	|
| local disk on bowie  	| local disk on bowie  	| internal bus  	| `for x in {1..4}; do time cp 1GB.dat 1GB.dat.copy; done` 	| 293 MB/sec 	|
| local disk on bowie  	| `/dev/null` on bowie   	| internal bus  	| `for x in {1..4}; do time cp 1GB.dat /dev/null ; done`   	| 3.4 GB/sec 	|
| local disk on hopper 	| local disk on hopper 	| internal bus  	|                                                               	|        6g/b    	|
| local disk on hopper 	| `/dev/null` on hopper  	| internal bus  	|                                                               	|            	|
| local disk on bowie  	| local disk on hopper 	| 1Gb network   	|                                                               	|            	|
| local disk on bowie  	| local disk on hopper 	| 10Gb network  	|                                                               	|            	|
| local disk on hopper 	| `/dev/null` on bowie   	| 1Gb network   	|                                                               	|            	|
| local disk on hopper 	| `/dev/null` on bowie   	| 10Gb network  	|                                                               	|            	|
