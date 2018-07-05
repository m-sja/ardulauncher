#########################################################
#		Welcome to Ardulauncher			#
#  With Ardulauncher you can use one single Arduino-IDE #
#  while having separate Environments like for ESP,	#
#  nRF... etc.						#
#  You can create multiple Links with start-parameter   #
#  to launch your desired configuration.		#
#							#
#  Usage:						#
#  ./ardulauncher -port_yourdirectory			#
#							#
#  You can also start ardulauncher without parameter	#
#  and select the desired directory via GUI		#
#							#
#########################################################


#!/bin/bash

clear

#checks if the portable-folder is a link or directory
if [ -d ./portable ] && [ ! -h ./portable ]
then
	>&2 echo -e "\e[31m./portable is not a link -> canceled\e[0m"
	exit
elif [[ ! $1 ]]
then
	echo "Please select Arduino-Environment:"
	dir="$(zenity --file-selection --directory --file-filter=port_* --title="Please select Arduino-Environment" 2>/dev/null)"
elif [ -d ./$1 ]
then
	dir=$1
else
	>&2 echo -e "\e[31m./$1 does not exist -> canceled\e[0m"
	exit
fi

if [[ ! $dir == *port_* ]]
then
	>&2 echo -e "\e[31minvalid directory -> canceled\e[0m"
	exit
fi

echo "$dir selected"

echo "deleting old link: ./portable"
find . -type l -iname "portable" | xargs rm 2>/dev/null

echo "creating new symlink: ./portable -> $dir"
ln -s $dir ./portable

echo -e "\e[32mlaunching Arduino IDE\e[0m"
