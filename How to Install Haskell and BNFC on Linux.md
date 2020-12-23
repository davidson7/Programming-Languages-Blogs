# How to Install Haskell and BNFC on Linux
**Works on Windows 10 Home and Windows 10 Education** <br>
*(Windows 10 Education is provided by Chapman for free for students)*

1. Install Ubuntu onto your PC from the Microsoft Store. Here is the link below: <br>
https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6?activetab=pivot:overviewtab

2. After installing Ubuntu onto your PC, the Ubuntu window will prompt you to enter a username and password. 
If successful, the Ubuntu window will prompt a *"Installation successful!"* message and your Linux command line will be displayed.

3. On your Linux command line, type *sudo apt update* and after type in your passsword. 
The update command is used to resynochronize the package index files from their sources on Ubuntu Linux through the internet.

4. On your Linux command line, type *sudo apt upgrade* and after type in your password. This
The upgrade command is used to install the newest versions of all packages currently installed on the Ubuntu system. <br>
*Note: Update and upgrade often to get the lastest versions of your packages installed to your Ubuntu.*

5. Navigate through the Window System on Ubuntu <br>
After the update and upgrade, <br>
   1. On your Linux command line type ***cd ..*** <br>
      michelle@DESKTOP-CMCCIPC:~$ cd ..
           
   2. Type ***cd ..*** again <br>
      michelle@DESKTOP-CMCCIPC:/home$ cd ..
           
   3. Type ***ls*** <br>
      michelle@DESKTOP-CMCCIPC:/$ ls <br>
      <pre>
      bin   dev  home  lib    lib64   media  opt   root  sbin  srv  tmp  var
      boot  etc  init  lib32  libx32  mnt    proc  run   snap  sys  usr
      </pre> 
   4. Type ***cd mnt*** <br>
           michelle@DESKTOP-CMCCIPC:/$ cd mnt
          
   5. Type ***ls*** (This will display your C: drive in your Window System) <br>
           michelle@DESKTOP-CMCCIPC:/mnt$ ls <br>
           <pre>
           c
           </pre>
        
   6. Type ***cd c*** <br>
           michelle@DESKTOP-CMCCIPC:/mnt$ cd c
           
   7. Type ***ls*** <br>
           michelle@DESKTOP-CMCCIPC:/mnt/c$ ls <br>
           <pre>
           '$Recycle.Bin'             PerfLogs                     Xilinx
            Apps                     'Program Files'               cygwin64
            Autodesk                 'Program Files (x86)'         hiberfil.sys
            Config.Msi                ProgramData                  mfg.sdr
            Dell                      Recovery                     pagefile.sys
           'Documents and Settings'  'System Volume Information'   swapfile.sys
            Intel                     Users                        tools
            IntelOptaneData           Windows                      windows-version.txt
            </pre>
   8. Type ***cd Users*** <br>
            michelle@DESKTOP-CMCCIPC:/mnt/c$ cd Users
            
   9. Type ***ls***, (This is display your folder in your Window System) <br>
             <pre>
            'All Users'   Default  'Default User'   Michelle    Public   desktop.ini
             </pre>
   10. From here, navigate to your Programming Languages folder

6. In your Programming Languages folder, 
   1. Type ***sudo apt install haskell-platform*** and after type in your password
   2. Type ***sudo apt install haskell-stack*** and after type in your password <br>
   Note: Ubuntu package for Ubuntu 16.10 and up, the Stack version might lag so type *stack upgrade* after you finish install it.

7. To download BNFC <br>
In your Programming Languages folder,
     1. Type ***stack install BNFC*** or ***cabal install BNFC***
     2. Type ***sudo apt install make***
 
     
Cited Resources: <br>
https://www.cyberciti.biz/faq/how-do-i-update-ubuntu-linux-softwares/ <br>
https://www.haskell.org/platform/#linux-ubuntu <br>
https://docs.haskellstack.org/en/stable/install_and_upgrade/
