![Release](https://img.shields.io/badge/release-alpha-red.svg)
![Language](https://img.shields.io/badge/made%20with-bash-brightgreen.svg)
![License](https://img.shields.io/badge/license-GPLv3-blue.svg)
![LastUpdate](https://img.shields.io/badge/last%20update-2018%2F04%2F22-yellow.svg)


<p align="center"><img src="https://" width="80%" height="auto"></p>

## About:
wifibang is a set of security tools which performs the main kinds of wifi attacks.
Its most important feature is the user-friendly CLI which encourages to use the script on mobile device (like smatphone, maybe associate with raspberry).


## Philosophy:
Script is based on five items: (in order of importance)
    1. minimal input 
    2. exception management 
    3. efficienty
    4. modularity
    5. portability
    
#### 1.minimal input
It is not easy insert long commands or several parameters on a mobile device, so the wifibang CLI was inspired from SET (social engineering toolkit) CLI: NOT cryptic parameters are required.  
All you have to do is insert a number or type [y/n]:
    
    <p align="center"><img src="https://" ></p>
    <p align="center"><img src="https://" ></p>
        
#### 2.exception management
Exception management restore the initial situation when an error occurs. It avoid user to exit from script and restore the environment before try the attack again (ex: restore the NIC).

#### 3.efficienty
The script must be fast. Complex (and slow) function should be rewrite.	(Occam's razor)

#### 4.modularity
Bash wasn't borned to do big modulable application. The most important problem with Bash is the absence of a complete return function
which could return a string. This avoid to make a complete modulable application because it's complex, and not elegant, to pass arguments (strings) between functions with more than one "echo".
My solution is a main script file where I put the functions which must communicated each other, while in external files there are the indipendent functions which not return anything (apart the exit status). 
The external scripts are called from main, with relative parameters.

You could add additionaly modules which must be indipendent each other.
**External script changes must not affected the others scripts.**

Maybe the use cases diagram of progect will clarify the idea: (EVIL TWIN AP ATTACK AND SNIFFER ARE NOT YET IMPLEMENTED)

<p align="center"><img src="https://" ></p>

**custom module**
It's simply add new attack modules:

	1.write them into external file
	2.create a new item in switch case
	3.make it executable (sudo chmod +x <module_name>)        
*Remember the policy of the main file and relative functions (see above)*

#### 5.portability
Portability is guaranteed by **bash**.
 
It's also essential use the minor number of not built-in linux utilities.
This provide a thin application, which not required the installation of tens package before running.
    
## Attacks:
    1.catch handshake and sniffing  (based on airodump-ng and aireplay-ng)
    2.process handshake     (based on aircrack-ng) (note)
    3.jammer    (based on aireplay-ng)
    4.router login form attack (based on THC-hydra)
    5.sniffing  (NOT YET IMPLEMENTED::airodump-ng or tcpdump)
    6.evil twin AP attack   (NOT YET IMPLEMENTED::hostapd)
    7.DNS spoofing  (NOT YET IMPLEMENTED::DNS spoof)
    8.clients port scanning (NOT YET IMPLEMENTED::NMAP)
    8.clients vulnerability assessment (NOT YET IMPLEMENTED::openVAS)
    9.clients exploitation (NOT YET IMPLEMENTED::metasploit)
    
**note** *I prefer this one instead hashcat because it's already includes into aircrack-ng suite (5° point). I know hashcat it's faster, but this script wasn't done to process long wordlists (to do this there are GPUs). This script was done to process short wordlist on fly with mobile device.*
      
## Installation:
Use the setup script to make the scripts executable and insert them directory into the PATH variable.
*If you change directory place, remember to update the PATH.*
    
## Future releases:
Next steps are:
	1. code review
	2. implementation of others attacks
	3. implementation of function which check for drivers compatibility
	4. monitor_mode function adjust
	
## Bugs to fix:
	1. Hydra function not work (wrong command parameters)

## Smartphone experiment:
It's very interesting try this script on android smartphone which use meefik's application (Linux Deploy) to emulate linux environment.
In many cases the script won't working for drivers incompatibility, but if you are lucky, you will have a good weapon on your hands!

	**TEST ON:**
	
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
	








