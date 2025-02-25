# Lichee RV Dock   

A small RISC-V Allwinner D1 board in a special dock.      

## Lichee RV
Fron https://wiki.sipeed.com/hardware/en/lichee/RV/RV.html   

Lichee RV - Nezha CM is a compute module with modular design, equipped with Allwinner D1 chip (based on T-Head XuanTie C906 core), 512MB DDR3 RAM.  
It can boot from TF card or SD-NAND, uses two sets of M.2 b key 67 pin connectors to route all IO, making it convenient for wide use and easy to replace.   

## Lichee RV Dock

From https://wiki.sipeed.com/hardware/en/lichee/RV/Dock.html   


Lichee RV Dock is a RISC-V Linux development kits with high integration, small size and affordable price designed for opensource developer.    
It's equipped with HDMI interface and it supports many screen by its screen convert board.    
It's also equipped with many peripherals, including a USB-A port, 2.4G Wifi-BT module, an analog microphone and a speaker jack interface. 
These means user can use it to develop or test linux application just by display device and input device like mouse and keyboard, which shortens developer's research and development time.   


<p align="center">
  <img src="https://github.com/paulhamsh/Sipeed-LycheeRV-RISC-V/blob/main/RV-Dock.jpg" width="400">
</p>


## Install Debian
https://wiki.sipeed.com/hardware/en/lichee/RV/flash.html  

Use PhoenixCard and the Debian image linked (also https://mega.nz/folder/lx4CyZBA#PiFhY7oSVQ3gp2ZZ_AnwYA/file/p8owQRaC)    
Use the Start Up option.      

SD card fits in slot on top just opposite the HDMI socket.   

Log in as ```root``` / ```licheepi```        

## Install Ubuntu

https://wiki.sipeed.com/hardware/en/lichee/RV/ubuntu.html  
https://canonical-ubuntu-boards.readthedocs-hosted.com/en/latest/how-to/sipeed-licheerv-dock/  

https://cdimage.ubuntu.com/releases/oracular/release/ubuntu-24.10-preinstalled-server-riscv64+licheerv.img.xz

Use balenaEtcher which works nicely.   I used a 32MB SD card.   

Booting is very very slow. Eventually you get a login prompt - with v24.10 use ```ubuntu``` / ```ubuntu```   

There is no C or assembler by default.   
