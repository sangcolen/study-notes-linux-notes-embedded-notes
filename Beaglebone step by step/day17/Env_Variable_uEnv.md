help
printenv
setenv
setenv serverip 192.168.27.1
setenv mmc_list 'run mmc list'
mmc rescan
quet the sd 
mmc dev 0
mmc rescan
quet the mmc
mmc dev 1
mmc rescan

mmc list