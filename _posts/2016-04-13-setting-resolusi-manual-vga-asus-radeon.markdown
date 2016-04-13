---
layout: post
title:  "Setting Manual resolusi VGA Asus Radeon"
date:   2016-04-13 07:24:00 +0700
categories: catatan
---

Satu hari yang lalu VGA NVDIA saya rusak, sepertinya ada yang konslet, dan sekarang masih di tukang serveris, get well soon yah :(. Berhubung dengan hal tersebut, saya akhirnya memakai VGA cadangan, yang masih baru kinyis2 belum pernah di pakai bertahun tahun, Merknya ASUS tipe EAH5450 DDR2 512Mb. VGA Card tersebut menggunakan driver amd radeon. Karena saya mau pakai dual monitor di vga tersebut sudah tersedia port D-SUB dan DVI serta HDMI (Gak terpakai). Seperti biasa, karena monitor saya hanya punya port D-SUB maka butuh konverter dari DVI ke D-SUB (VGA).

Di VGA Card yang sebelumnya malah kedua portnya adalah DVI, jadi dua duanya menggunakan konverter ke port VGA. Masalahnya, jika menggunakan konverter, resolusi yang terdeteksi otomatis oleh komputer hanya mentok sampai 1024*768 saja. Oleh sebab itu, saya harus membuat konfigurasi manual di file `xorg.conf` nya.

Sebelumnya sudah saya utak atik file xorg.conf tapi belum ketemu juga caranya, saya terapkan cara yang pernah saya pakai di vga card nvidia ternyata tidak manjur. Dan akhirnya hari ini ketemu dan monitor saya sudah memiliki resolusi maksimal sesuai kemampuanya :D.

Sebelumnya pakai cara ini di terminal.

## 1. Cara sementara
Generate mode
```
cvt 1600 900 60
```
Output

```
# 1600x900 59.95 Hz (CVT 1.44M9) hsync: 55.99 kHz; pclk: 118.25 MHz
Modeline "1600x900_60.00"  118.25  1600 1696 1856 2112  900 903 908 934 -hsync +vsync
```
Kemudian jalankan beberapa perintah xrandr ini
```
xrandr --newmode "1600x900_60.00"  118.25  1600 1696 1856 2112  900 903 908 934 -hsync +vsync
xrandr --addmode DVI-0 1600x900_60.00
xrandr --output DVI-0 --mode 1600x900_60.00
```

Tapi cara di atas akan hilang pada saat komputer di restart / log out session.

## 2. Cara permanen
Sedangkan cara permanent adalah menulis konfigurasi di file `xorg.conf` yang terletak di `/etc/X11/xorg.conf`. Untuk menggenerate file tersebut saya menemukan di artikel [ini](http://ubuntuforums.org/showthread.php?t=1850578), caranya jalankan perintah sebagai berikut :
```
sudo X :1 -configure
```
Output file di `/root/xorg.conf.new`
Backup dulu file xorg.conf yang sudah ada, contoh:
```
sudo cp /etc/X11/xorg.conf /etc/X11/xorg.conf.nvidia
```
Lalu timpa xorg.conf lama dengan yang baru

```
sudo cp /root/xorg.conf.new /etc/X11/xorg.conf
```

File hasil generate 

```
Section "ServerLayout"
	Identifier     "X.org Configured"
	Screen      0  "Screen0" 0 0
	InputDevice    "Mouse0" "CorePointer"
	InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

Section "Files"
	ModulePath   "/usr/lib64/xorg/modules"
	FontPath     "catalogue:/etc/X11/fontpath.d"
	FontPath     "built-ins"
EndSection

Section "Module"
	Load  "glx"
EndSection

Section "InputDevice"
	Identifier  "Keyboard0"
	Driver      "kbd"
EndSection

Section "InputDevice"
	Identifier  "Mouse0"
	Driver      "mouse"
	Option	    "Protocol" "auto"
	Option	    "Device" "/dev/input/mice"
	Option	    "ZAxisMapping" "4 5 6 7"
EndSection

Section "Monitor"
	Identifier   "Monitor0"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
EndSection

Section "Device"
        ### Available Driver options are:-
        ### Values: <i>: integer, <f>: float, <bool>: "True"/"False",
        ### <string>: "String", <freq>: "<f> Hz/kHz/MHz",
        ### <percent>: "<f>%"
        ### [arg]: arg optional
        #Option     "Accel"              	# [<bool>]
        #Option     "SWcursor"           	# [<bool>]
        #Option     "EnablePageFlip"     	# [<bool>]
        #Option     "ColorTiling"        	# [<bool>]
        #Option     "ColorTiling2D"      	# [<bool>]
        #Option     "RenderAccel"        	# [<bool>]
        #Option     "SubPixelOrder"      	# [<str>]
        #Option     "AccelMethod"        	# <str>
        #Option     "ShadowPrimary"      	# [<bool>]
        #Option     "EXAVSync"           	# [<bool>]
        #Option     "EXAPixmaps"         	# [<bool>]
        #Option     "ZaphodHeads"        	# <str>
        #Option     "SwapbuffersWait"    	# [<bool>]
        #Option     "DeleteUnusedDP12Displays" 	# [<bool>]
        #Option     "DRI3"               	# [<bool>]
        #Option     "DRI"                	# <i>
        #Option     "TearFree"           	# [<bool>]
	Identifier  "Card0"
	Driver      "radeon"
	BusID       "PCI:1:0:0"
EndSection

Section "Screen"
	Identifier "Screen0"
	Device     "Card0"
	Monitor    "Monitor0"
	SubSection "Display"
		Viewport   0 0
		Depth     1
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     4
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     8
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     15
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     16
	EndSubSection
	SubSection "Display"
		Viewport   0 0
		Depth     24
	EndSubSection
EndSection

```

dan kemudian saya edit seperti ini 

```
Section "ServerLayout"
	Identifier     "X.org Configured"
	Screen      0  "Screen0" 0 0
	InputDevice    "Mouse0" "CorePointer"
	InputDevice    "Keyboard0" "CoreKeyboard"
EndSection

Section "Files"
	ModulePath   "/usr/lib64/xorg/modules"
	FontPath     "catalogue:/etc/X11/fontpath.d"
	FontPath     "built-ins"
EndSection

Section "Module"
	Load  "glx"
EndSection

Section "InputDevice"
	Identifier  "Keyboard0"
	Driver      "kbd"
EndSection

Section "InputDevice"
	Identifier  "Mouse0"
	Driver      "mouse"
	Option	    "Protocol" "auto"
	Option	    "Device" "/dev/input/mice"
	Option	    "ZAxisMapping" "4 5 6 7"
EndSection

Section "Monitor"
	Identifier   "Monitor0"
	VendorName   "Monitor Vendor"
	ModelName    "Monitor Model"
	
	# 1600x900 59.95 Hz (CVT 1.44M9) hsync: 55.99 kHz; pclk: 118.25 MHz
    Modeline "1600x900_60.00"  118.25  1600 1696 1856 2112  900 903 908 934 -hsync +vsync
    Option  "PreferredMode" "1600x900_60.00"
EndSection

Section "Device"
        ### Available Driver options are:-
        ### Values: <i>: integer, <f>: float, <bool>: "True"/"False",
        ### <string>: "String", <freq>: "<f> Hz/kHz/MHz",
        ### <percent>: "<f>%"
        ### [arg]: arg optional
        #Option     "Accel"              	# [<bool>]
        #Option     "SWcursor"           	# [<bool>]
        #Option     "EnablePageFlip"     	# [<bool>]
        #Option     "ColorTiling"        	# [<bool>]
        #Option     "ColorTiling2D"      	# [<bool>]
        #Option     "RenderAccel"        	# [<bool>]
        #Option     "SubPixelOrder"      	# [<str>]
        #Option     "AccelMethod"        	# <str>
        #Option     "ShadowPrimary"      	# [<bool>]
        #Option     "EXAVSync"           	# [<bool>]
        #Option     "EXAPixmaps"         	# [<bool>]
        #Option     "ZaphodHeads"        	# <str>
        #Option     "SwapbuffersWait"    	# [<bool>]
        #Option     "DeleteUnusedDP12Displays" 	# [<bool>]
        #Option     "DRI3"               	# [<bool>]
        #Option     "DRI"                	# <i>
        #Option     "TearFree"           	# [<bool>]
	Identifier  "Card0"
	Driver      "radeon"
	BusID       "PCI:1:0:0"
	Option      "Monitor-DVI-0" "Monitor0"
EndSection

Section "Screen"
	Identifier "Screen0"
	Device     "Card0"
	Monitor    "Monitor0"
    DefaultDepth  24
	SubSection "Display"
		Depth     24
		Modes   "1600x900_60.00" "1600x900_60.00"
	EndSubSection
EndSection

```
Dan setelah saya restart, huwala monitor saya yang memakai converter DVI to VGA akhirnya bisa menggunakan resolusi sesuai kemampuan maksimalnya :D.

Sekalian saya copykan contoh konfigurasi xorg.conf VGA Card NVIDIA

```
# nvidia-xconfig: X configuration file generated by nvidia-xconfig
# nvidia-xconfig:  version 361.28  (buildmeister@swio-display-x64-rhel04-04)  Wed Feb  3 16:27:53 PST 2016

Section "ServerLayout"
    Identifier     "Layout0"
    Screen      0  "Screen0"
    InputDevice    "Keyboard0" "CoreKeyboard"
    InputDevice    "Mouse0" "CorePointer"
EndSection

Section "Files"
    FontPath        "/usr/share/fonts/default/Type1"
EndSection

Section "InputDevice"
    # generated from default
    Identifier     "Mouse0"
    Driver         "mouse"
    Option         "Protocol" "auto"
    Option         "Device" "/dev/input/mice"
    Option         "Emulate3Buttons" "no"
    Option         "ZAxisMapping" "4 5"
EndSection

Section "InputDevice"
    # generated from default
    Identifier     "Keyboard0"
    Driver         "kbd"
EndSection

#Section "Monitor"
#    Identifier     "Monitor0"
#    VendorName     "Unknown"
#    ModelName      "Unknown"
#    HorizSync       28.0 - 33.0
#    VertRefresh     43.0 - 72.0
#    Option         "DPMS"
#EndSection

Section "Monitor"
    Identifier     "Monitor0"
    VendorName     "Philips"
    ModelName      "Pilips 203V5LSB26"
    HorizSync       30.00 - 83.00
    VertRefresh     56.00 - 75.00
    Option         "DPMS"
    Option         "UseEdidDpi" "FALSE"
    Option         "DPI" "96 x 96"
    # PHILIPS
    Mode "1600x900"
      DotClock 97.75
      HTimings 1600 1648 1680 1760
      VTimings 900 903 908 926
      Flags "+HSync" "+VSync"
    EndMode   
    # Inforce
    # 1360x768 59.80 Hz (CVT) hsync: 47.72 kHz; pclk: 84.75 MHz
    Modeline "1360x768_60.00"   84.75  1360 1432 1568 1776  768 771 781 798 -hsync +vsync
EndSection

Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "GeForce GTX 550 Ti"
EndSection

Section "Screen"
    Identifier     "Screen0"
    Device         "Device0"
    Monitor        "Monitor0"
    DefaultDepth    24
    Option "IgnoreEDID"	"true"
    Option "nvidiaXineramaInfoOrder" "DVI-I-0"
    Option "metamodes" "1600x900+0+0"
    SubSection     "Display"
        Depth       24
    EndSubSection
EndSection

```

### Link Refrensi
1. [Wiki Ubuntu](https://wiki.ubuntu.com/X/Config/Resolution)
2. [Ubuntu Forum](http://ubuntuforums.org/showthread.php?t=1850578)