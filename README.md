# Born2beRoot_42
Born2beRoot_Installation_and_setup
#!/bin/bash
ar=$(uname -a)
CPUp=$(lscpu | grep CPU'(s)' | head -n 1 | awk '{print $2}')
vCPU=$(cat /proc/cpuinfo | grep processor | wc -l)
MU=$(free -m | head -n 2 | tail -n 1 | awk '{print $2 "MB"}')
USED=$(free -m | head -n 2 | tail -n 1 | awk '{print $3}')
PERC=$(free -m | head -n 2 | tail -n 1 | awk '{printf ("%.2f", $3/$2 * 100.0)}' && echo "%")
DU=$(df -h /dev/sda1 | tail -1 | awk '{print $3 "/" $2 " ("$5")"}')
CPUl=$(top -bn1 | grep load | awk '{print $11}' | cut -c -4)
LB=$(who -b | awk '{print $3 " " $4}')
LVMu=$(lsblk | grep lvm | awk '{if ($1) {print "yes";exit;} else {print "no"}}')
CTCP=$(netstat -an | grep ESTABLISHED | wc -l)
CTCPl=$(netstat -an | grep ESTABLISHED | awk '{print $6}')
Userl=$(who | awk '{print $1}' | sort -u | wc -l)
IP=$(ip a | tail -n 4 | head -n 1 | awk '{print $2}' | cut -c -13)
Mac=$(ip a | tail -n 5 | awk '{print $2}' | head -n 1)
Sudo=$(journalctl _COMM=sudo | grep COMMAND | wc -l)
wall "
#Architecture : $ar
#CPU physical : $CPUp
#vCPU : $vCPU
#Memory Usage : $USED/$MU ($PERC)
#Disk Usage : $DU
#CPU load : $CPUl
#Last boot : $LB
#LVM use : $LVMu
#Connexions TCP : $CTCP $CTCPl
#User log : $Userl
#Network : IP $IP ($Mac)
#Sudo : $Sudo cmd"
