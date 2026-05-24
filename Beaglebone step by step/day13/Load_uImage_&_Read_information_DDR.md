Load uImage from Memory Device in to the DDR Memory of the board

use Memory Display read information load into DDR memory

=> load mmc 0<INTERRUPT>                                                        
** Bad device specification mmc 0<INTERRUPT> **                                 
** Bad device specification mmc 0<INTERRUPT> **                                 
=> help load                                                                    
load - load binary file from a filesystem                                       
                                                                                
Usage:                                                                          
load <interface> [<dev[:part]> [<addr> [<filename> [bytes [pos]]]]]             
    - Load binary file 'filename' from partition 'part' on device               
       type 'interface' instance 'dev' to address 'addr' in memory.             
      'bytes' gives the size to load in bytes.                                  
      If 'bytes' is 0 or omitted, the file is read until the end.               
      'pos' gives the file byte position to start reading from.                 
      If 'pos' is 0 or omitted, the file is read from the start.                
=> load mmc 0:2 0x82000000 /boot/uImage                                         
4002080 bytes read in 290 ms (13.2 MiB/s)                                       
=> help md                                                                      
md - memory display                                                             
                                                                                
Usage:                                                                          
md [.b, .w, .l] address [# of objects]                                          
=> md 0x82000000 4                                                              
82000000: 56190527 62153da1 50d07e51 e0103d00    '..V.=.bQ~.P.=..               
=> md 0x82000000 10                                                             
82000000: 56190527 62153da1 50d07e51 e0103d00    '..V.=.bQ~.P.=..               
82000010: 00800080 00800080 d58b5329 00020205    ........)S......               
82000020: 73676e41 6d6f7274 382e332f 2f30312e    Angstrom/3.8.10/               
82000030: 67616562 6f62656c 0000656e 00000000    beaglebone......               
=> help imi                                                                     
iminfo - print header information for application image                         
                                                                                
Usage:                                                                          
iminfo addr [addr ...]                                                          
    - print header information for application image starting at                
      address 'addr' in memory; this includes verification of the               
      image contents (magic number, header and payload checksums)               
=> imi 0x82000000                                                               
                                                                                
## Checking Image at 82000000 ...                                               
   Legacy image found                                                           
   Image Name:   Angstrom/3.8.10/beaglebone                                     
   Created:      2013-04-29  19:56:00 UTC                                       
   Image Type:   ARM Linux Kernel Image (uncompressed)                          
   Data Size:    4002016 Bytes = 3.8 MiB                                        
   Load Address: 80008000                                                       
   Entry Point:  80008000                                                       
   Verifying Checksum ... OK                                                    
=> 
