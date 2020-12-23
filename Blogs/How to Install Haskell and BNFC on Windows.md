### **How to Install Haskell on Windows using Chocolatey package manager**

1. Go to haskell.org and click on Downloads
![Screenshot 2020-10-12 144357](https://user-images.githubusercontent.com/47368101/95799228-dc993800-0ca8-11eb-8387-ba330b3cc12f.png)


2. Scroll down to Minimal Installers and click on Windows
![2](https://user-images.githubusercontent.com/47368101/95803365-c2fded80-0cb4-11eb-849e-1838be349af8.png)

3. Click on Configure Chocolatey if you don't already have it installed
![3](https://user-images.githubusercontent.com/47368101/95803397-d9a44480-0cb4-11eb-80a7-7bfd44aac927.png)

![4](https://user-images.githubusercontent.com/47368101/95803415-ea54ba80-0cb4-11eb-9a46-5897007775cf.png)

4. Open up Windows Powershell as an Administrator
![5](https://user-images.githubusercontent.com/47368101/95803453-0193a800-0cb5-11eb-910c-669377992cbf.png)

5. Run 'Get-ExecutionPolicy'
	-If it returns 'Restricted':
		Run 'Set-ExecutionPolicy AllSigned' or 'Set-ExecutionPolicy Bypass -Scope Process'

6. Run  

		Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
		

7. When the command is complete, if there are no errors, Chocolatey is set-up

8. Return to the Haskell Windows Install page
![3](https://user-images.githubusercontent.com/47368101/95803397-d9a44480-0cb4-11eb-80a7-7bfd44aac927.png)

9. Run 'cabal user-config init -f '

10. Run 'choco install haskell-dev
	 refreshenv'
	 
	 
*******


### **Install BNFC from source on Windows**

Option 1

1. If Haskell is not installed, go to Haskell.org and follow the instructions under Downloads -> Minimal Installers -> Windows

2. Open Windows Powershell as an Administrator

3. Run  'cabal update', then  'cabal install BNFC'
	
		If shown the message  'The program 'ghc' version >=7.0.1 is required but it could not be found.':
		-Force an older install with chocolately:
		
			choco install ghc --version 7.10.2 --force
			refreshenv
			
		-Then try and install BNFC again

Option 2
	
1. If you have git installed, open the Windows Powershell or the command line, where ever git is recognized and run:

		git clone https://github.com/BNFC/bnfc
		cd bnfc  
		make
