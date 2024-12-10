#!/bin/bash

#function checking is the 
checking(){
    koreksi=`chronyc activity | grep unknown | awk '{ print $1 }'`
    if [[ $koreksi -gt 0 ]]
    then
        sed -i "/$source/d" /etc/chrony.conf 
        echo adress not woriking, pls try again
    else echo success
    fi
}

if [[ $EUID -ne 0 ]]; then
    echo "This script must be run as \"root\". Please switch to user \"root\"."
    sleep 2
    exit
fi

echo ====================================================
echo " .______. .__. .__. .____."  
echo " |_    _| |  |_|  | |  __|" 
echo "   |  |   |   _   | |  __|  Chrony Killer"
echo "   |__|   |__| |__| |____|  no more chrony config"
echo ====================================================

chronyc sources
chronyc makestep
date
echo -e "\nInput source? \nex: id.pool.bto.org or ip address"
read source

echo "NTP Mode (1/2)"
echo "1. Server"
echo "2. Pool"
read input


# the doing
case $input in
    1) sed -i "4i server $source iburst" /etc/chrony.conf
       echo configurating...
       systemctl restart chronyd
       sleep 2
       checking;;
    2) sed -i "4i pool $source iburst" /etc/chrony.conf
       echo configurating...
       systemctl restart chronyd
       sleep 2
       checking
esac

