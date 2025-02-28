# Lichee RV Dock   

A small RISC-V Allwinner D1 board in a special dock.      
Intstructions to get a RISC-V assembly language "hello world" to run.   
Basically a summary of the Licehee RV Dock wiki and Stephen Smith's blog on RISC-V.     

## Lichee RV
From https://wiki.sipeed.com/hardware/en/lichee/RV/RV.html   


>Lichee RV - Nezha CM is a compute module with modular design, equipped with Allwinner D1 chip (based on T-Head XuanTie C906 core), 512MB DDR3 RAM.  
>It can boot from TF card or SD-NAND, uses two sets of M.2 b key 67 pin connectors to route all IO, making it convenient for wide use and easy to replace. 

<p align="center">
  <img src="https://github.com/paulhamsh/Sipeed-LycheeRV-RISC-V/blob/main/D1-4.jpg" width="400">
</p>

## Lichee RV Dock

From https://wiki.sipeed.com/hardware/en/lichee/RV/Dock.html   

>Lichee RV Dock is a RISC-V Linux development kits with high integration, small size and affordable price designed for opensource developer.    
>It's equipped with HDMI interface and it supports many screen by its screen convert board.    
>It's also equipped with many peripherals, including a USB-A port, 2.4G Wifi-BT module, an analog microphone and a speaker jack interface. 
>These means user can use it to develop or test linux application just by display device and input device like mouse and keyboard, which shortens developer's research and development time.

<p align="center">
  <img src="https://github.com/paulhamsh/Sipeed-LycheeRV-RISC-V/blob/main/RV-Dock.jpg" width="400">
</p>


## Debian

### Install   
From here https://wiki.sipeed.com/hardware/en/lichee/RV/flash.html  

Use PhoenixCard and the Debian image linked (also https://mega.nz/folder/lx4CyZBA#PiFhY7oSVQ3gp2ZZ_AnwYA/file/p8owQRaC)    
Use the Start Up option.      

SD card fits in slot on top just opposite the HDMI socket.   

Log in as ```root``` / ```licheepi```        

### Set up wifi   
Use ```connman``` to set up your wifi    

### Fix the apt NO_PUBKEY E852514F5DF312F6 error   
Fixes it but then there is nothing it will apt-get....  

**On another computer** (because wget is not installed) download a vesrion of ```debian-ports-archive-keyring``` (it will have a date after it, like ```debian-ports-archive-keyring_2025.02.01_all.deb```) from http://ftp.uk.debian.org/debian/pool/main/d/debian-ports-archive-keyring/   
I used ```debian-ports-archive-keyring_2025.02.01_all.deb``` because the one mentioned was not there   

Get the latest one, and copy to your SD card (perhaps in ```/home/root/```
Load up Debian then run 
```
sudo dpkg -i debian-ports-archive-keyring_2025.02.01_all.deb
```    


### Set up ssh   
Set up ssh
```
sudo bash
vi /etc/ssh/sshd_config
```
after line 
```
#PermitRootLogin prohibit-password
```
add
```
PermitRootLogin yes
```
then
```
systemctl stop ssh
systemctl start ssh
```

### Add a new user    
Perhaps add a new user
```
useradd paul
passwd paul
```

## Run Hello World from Stephen Smith's blog

From here https://smist08.wordpress.com/2019/09/07/risc-v-assembly-language-hello-world/    

Create ```hello.s```      

```
#
# Risc-V Assembler program to print "Hello World!"
# to stdout.
#
# a0-a2 - parameters to linux function services
# a7 - linux function number
#

.global _start      # Provide program starting address to linker

# Setup the parameters to print hello world
# and then call Linux to do it.

_start: addi  a0, x0, 1      # 1 = StdOut
        la    a1, helloworld # load address of helloworld
        addi  a2, x0, 13     # length of our string
        addi  a7, x0, 64     # linux write system call
        ecall                # Call linux to output the string

# Setup the parameters to exit the program
# and then call Linux to do it.

        addi    a0, x0, 0   # Use 0 return code
        addi    a7, x0, 93  # Service command code 93 terminates
        ecall               # Call linux to terminate the program

.data
helloworld:      .ascii "Hello World!\n"

```

To compile and run

```
riscv64-linux-gnu-as -march=rv64imac -o hello.o hello.s
riscv64-linux-gnu-ld -o hello hello.o
chmod +x hello
./hello
```

Or
```
as -o hello.o hello.s
ld -o hello hello.o
chmod +x hello
./hello

```

## Option: Install Ubuntu

https://wiki.sipeed.com/hardware/en/lichee/RV/ubuntu.html  
https://canonical-ubuntu-boards.readthedocs-hosted.com/en/latest/how-to/sipeed-licheerv-dock/  

https://cdimage.ubuntu.com/releases/oracular/release/ubuntu-24.10-preinstalled-server-riscv64+licheerv.img.xz

Use balenaEtcher which works nicely.   I used a 32MB SD card.   

Booting is very very slow. Eventually you get a login prompt - with v24.10 use ```ubuntu``` / ```ubuntu```   

There is no C or assembler by default.   
No desktop even though Debian has.   

I tried it and reverted to using Debian.   

