![Release](https://img.shields.io/badge/release-alpha-red.svg)
![Language](https://img.shields.io/badge/made%20with-bash-brightgreen.svg)
![License](https://img.shields.io/badge/license-GPLv3-blue.svg)
![LastUpdate](https://img.shields.io/badge/last%20update-2018%2F04%2F22-yellow.svg)


<p align="center"><img src="https://github.com/Leviathan36/wifibang/blob/master/wifibang%20images/cover_image.png" width="80%" height="auto"></p>

## About:
wifibang is a set of security tools which perform the main kinds of wifi attacks.
Its most important feature is the user-friendly CLI which encourages users to use the script on mobile devices (like a smartphone, maybe associated with a raspberry).


## Philosophy:
Script is based on five concepts: (in order of importance)

1. minimal input 
2. exception management 
3. efficiency
4. modularity
5. portability
    
#### 1.minimal input
It is not convenient insert long commands or several parameters on a mobile device, so the wifibang CLI was inspired from SET (social engineering toolkit) CLI: NO cryptic parameters are required.  
All you have to do is insert a number or type [y/n]:
    
<p align="center"><img src="https://github.com/Leviathan36/wifibang/blob/master/wifibang%20images/Screenshots/menu.png" height="300" width="auto"></p>
    
<p align="center"><img src="https://github.com/Leviathan36/wifibang/blob/master/wifibang%20images/Screenshots/ap_list.png" height="300" width="auto"></p>
        
#### 2.exception management
Exception management restores the initial situation when an error occurs. It avoids the user to exit the script and restoring the environment before trying the attack again (ex: restore the NIC).

#### 3.efficiency
The script must be fast. Complex (and slow) function should be rewritten. (Occam's razor)

#### 4.modularity
Bash wasn't designed for big modular applications. The most important problem with Bash is the absence of a complete return function that returns a string. This prevents the creation of complete modular application because it's complex, and not elegant, to pass arguments (strings) between functions with more than one "echo".
My solution is a main script file where I put the functions which must communicate with each other, while in external files I put the indipendent functions which do not return anything (apart from the exit status). 
The external scripts are called from main, with relative parameters.

You could add additional modules which must be indipendent from each other.
**External script changes must not affect the others scripts.**

Maybe the use cases diagram of the project will clarify the idea: (EVIL TWIN AP ATTACK AND SNIFFER ARE NOT YET IMPLEMENTED)



<p align="center"><img src="https://github.com/Leviathan36/wifibang/blob/master/wifibang%20images/use_cases_diagram.jpg" ></p>



**custom module**

It's simple to add new attack modules:

1. write them into external file
2. create a new item in switch case
3. make it executable (sudo chmod +x <module_name>)  

*Remember the policy of the main file and relative functions (see above)*

#### 5.portability
Portability is guaranteed by **bash**.
 
It's also essential use the least number of non built-in linux utilities.
This provides a thin application, which does not require the installation of tens of packages before running.
    
## Attacks:

1. catch handshake and sniffing  (based on airodump-ng and aireplay-ng)
2. process handshake     (based on aircrack-ng) (note)
3. jammer    (based on aireplay-ng)
4. router login form attack (based on THC-hydra)
5. sniffing  (NOT YET IMPLEMENTED::airodump-ng or tcpdump)
6. evil twin AP attack   (NOT YET IMPLEMENTED::hostapd)
7. DNS spoofing  (NOT YET IMPLEMENTED::DNS spoof)
8. clients port scanning (NOT YET IMPLEMENTED::NMAP)
9. clients vulnerability assessment (NOT YET IMPLEMENTED::openVAS)
10. clients exploitation (NOT YET IMPLEMENTED::metasploit)
    
**note** *I prefer this one instead hashcat because its already included into aircrack-ng suite (5° point). I know hashcat it's faster, but this script isn't supposed to process long wordlists (there are GPUs for this task). This script was created to process short wordlists on the fly with mobile devices.*
      
## Installation:
Use the setup script to make the scripts executable and insert their directory into the PATH variable.
*If you change directory location, remember to update the PATH.*
    
## Future releases:

Next steps are:

1. code review
2. implementation of others attacks
3. implementation of functions which check for drivers compatibility
4. monitor_mode function adjust

## Common Errors:

Sometimes you could stumble across this error:

	read failed: Network is down
	ioctl(SIOCSIWMODE) failed: Device or resource busy

	ARP linktype is set to 1 (Ethernet) - expected ARPHRD_IEEE80211,
	ARPHRD_IEEE80211_FULL or ARPHRD_IEEE80211_PRISM instead.  Make
	sure RFMON is enabled: run 'airmon-ng start <interface> <#>'
	Sysfs injection support was not found either.

	Can't reopen <interface>


It's probably due to a conflict between network manager and aircrack-ng-suite tools (aireplay-ng, airodump-ng) since they both try to connect to an AP using the same interface.

The error disappears if you disconnect from the hotspot and try again.
Maybe I will add a conditional statement to forcibly disconnect before using network manager (nmcli).

## Bugs to fix:

<a href="https://github.com/Leviathan36/wifibang/blob/master/BUGS_TO_FIX.md">here</a>

## Smartphone experiment:
It's very interesting try this script on android smartphone using meefik's application (Linux Deploy) to run a chrooted linux environment.
In many cases the script won't work for drivers incompatibility, but if you are lucky, you will have a good weapon in your hands!

**TESTED ON:**
	
1. Samsung Galaxy S2 Plus NFC (Android Lollipop)

*RESULT:* testing phase
	
## Disclaimer:
**Using this software to crack wifi network is illegal.**
**Author assume no liability and are not responsible for any misuse or damage caused by this program.**

**wifibang is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.**

## License:
wifi-bang is released under GPLv3 license. See [LICENSE](LICENSE) for more details.

## Credits:
The script is based from an idea by Leviathan36.
	








