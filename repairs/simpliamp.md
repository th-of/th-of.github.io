---
layout: default
---

## Applied Biosystems SimpliAmp Thermal Cycler

This thermal cycler ("PCR machine") was found in the E-waste recycling bin and considering its $6000 USD price tag (before VAT) I thought I'd take a look. 

The machine boots to an error message and the touch screen is unresponsive, I am not able to proceed from this error. I immediately suspect a fault with the ribbon cable connecting the 
LCD to the processor so I proceed to disassemble the unit to have a look. My suspicion was correct, the retention bar locking the ribbon cable into the connector was unlocked. 
Simply reseating the ribbon cable and properly locking it in place with the retention bar fixed the issue. The machine now boots properly with working touch input, there is no 
error message and I can make new users and run thermal cycling protocols. However, I am unable to access the administrator account and the service account. 

When taking apart the unit I could see that the main PCB was ideal for debugging/troubleshooting/hacking:

<center>
<div class="container">
  <input type="checkbox" id="zoomCheck">
  <label for="zoomCheck">
    <img src="/repairs/simpliamp_board.jpg" width="600">
  </label>
</div>
</center>

Easy access to the machine is provided over a micro-USB serial port in the lower left of the image by the mounting screw (J18 USB Serial). Connecting to the serial port
at 115200 baud and recording the boot sequence gives the following:

{::options parse_block_html="true" /}

<details><summary markdown="span">Show boot sequence...</summary>
```console
Starting kernel ...


Linux version 2.6.35.3-1.0-lt-850-gbc67621-svn847 (cwching@cwching-ubuntu10) (gcc version 4.4.6 (Ubuntu/Linaro 4.4.6-3ubuntu1~ppa3) ) #1 PREEMPT Mon Mar 21 19:00:35 SGT 2016
CPU: ARMv7 Processor [412fc085] revision 5 (ARMv7), cr=10c53c7f
CPU: VIPT nonaliasing data cache, VIPT nonaliasing instruction cache
Machine: Freescale MX53 OCB Flashlight Board
Memory policy: ECC disabled, Data cache writeback
Built 1 zonelists in Zone order, mobility grouping on.  Total pages: 89408
Kernel command line: console=ttymxc1,115200 jtag=on video=mxcdi0fb:RGB666,TM080SDHG02 di0_primary root=/dev/mmcblk0p1 rootwait rw single init=/bin/bash
PID hash table entries: 2048 (order: 1, 8192 bytes)
Dentry cache hash table entries: 65536 (order: 6, 262144 bytes)
Inode-cache hash table entries: 32768 (order: 5, 131072 bytes)
Memory: 352MB = 352MB total
Memory: 347488k/347488k available, 12960k reserved, 0K highmem
Virtual kernel memory layout:
    vector  : 0xffff0000 - 0xffff1000   (   4 kB)
    fixmap  : 0xfff00000 - 0xfffe0000   ( 896 kB)
    DMA     : 0xf9e00000 - 0xffe00000   (  96 MB)
    vmalloc : 0x96800000 - 0xf4000000   (1496 MB)
    lowmem  : 0x80000000 - 0x96000000   ( 352 MB)
    pkmap   : 0x7fe00000 - 0x80000000   (   2 MB)
    modules : 0x7f000000 - 0x7fe00000   (  14 MB)
      .init : 0x80008000 - 0x800a1000   ( 612 kB)
      .text : 0x800a1000 - 0x808e1000   (8448 kB)
      .data : 0x80906000 - 0x8094f480   ( 294 kB)
SLUB: Genslabs=11, HWalign=32, Order=0-3, MinObjects=0, CPUs=1, Nodes=1
Hierarchical RCU implementation.
	RCU-based detection of stalled CPUs is disabled.
	Verbose stalled-CPUs detection is disabled.
NR_IRQS:368
MXC GPIO hardware
MXC IRQ initialized
Time_init Before
system_timer->init:8000d5e4
########## mxc_jtag_enabled:1 MXC_CCM_CCGR0:FFFFFFFF ########## 
########## mxc_jtag_enabled:1 MXC_CCM_CCGR0:150FFFF5 ########## 
########## MXC_CCM_CCGR0:150FFFF5 ########## 
MXC_Early serial console at MMIO 0x53fc0000 (options '115200')
bootconsole [ttymxc1] enabled
Time_init After
start_kernel(): arm_icgc_reg:0
Console: colour dummy device 80x30
Calibrating delay loop... 799.53 BogoMIPS (lpj=3997696)
pid_max: default: 32768 minimum: 301
Mount-cache hash table entries: 512
CPU: Testing write buffer coherency: ok
regulator: core version 0.5
NET: Registered protocol family 16
i.MX IRAM pool: 128 KB@0x96840000
IRAM READY
OCB Board Rev ID=20
IPU Clock Rate:56875000
SPI Clock Rate:56875000
CPU is i.MX53 Revision 2.1
Actual DISP_SHUT=0 DISP_RESB=0
Actual CSI1_RESET=0 CSI1_STROBE=1
i2c-core register boardinfo:mc34708
i2c-core register boardinfo:mt9p031
Using SDMA I.API
MXC DMA API initialized
IMX usb wakeup probe
IMX usb wakeup probe
bio: create slab <bio-0> at 0
SCSI subsystem initialized
CSPI: mxc_spi-3 probed
Freescale USB OTG Driver loaded, $Revision: 1.55 $
usbcore: registered new interface driver usbfs
usbcore: registered new interface driver hub
usbcore: registered new device driver usb
i2c i2c-2: Failed to register i2c client mc34708 at 0x08 (-16)
i2c i2c-2: Can't create device at 0x08
### platform_driver_probe:imx-i2c ret:0
ipu_probe: enter
IPU VDI Regs = 968b2000
IPU CM Regs = 9687e000
IPU IC Regs = 96882000
IPU IDMAC Regs = 96886000
IPU DP Regs = 9688a000
IPU DC Regs = 9688e000
IPU DMFC Regs = 96892000
IPU DI0 Regs = 96896000
IPU DI1 Regs = 9689a000
IPU SMFC Regs = 9689e000
IPU CSI0 Regs = 968a2000
IPU CSI1 Regs = 968a6000
IPU CPMem = 968aa000
IPU TPMem = 968c0000
IPU DC Template Mem = 96900000
IPU Display Region 1 Mem = 968ae000
ipu_clk = 200000000
ipu_probe: exit
Advanced Linux Sound Architecture Driver Version 1.0.23.
Bluetooth: Core ver 2.15
NET: Registered protocol family 31
Bluetooth: HCI device and connection manager initialized
Bluetooth: HCI socket layer initialized
mc34708 - pmic_probe: Enter
mc34708 pmic chip ID=00000014
PMIC MC34708 ID:0x14
regulator: SW1: 650 <--> 1437 mV at 1100 mV 
regulator: SW1B: 650 <--> 1437 mV at 1100 mV 
regulator: SW2: 650 <--> 1437 mV at 1300 mV 
regulator: SW3: 650 <--> 1425 mV at 1200 mV 
regulator: SW4A: 1200 <--> 3300 mV at 1500 mV 
regulator: SW4B: 1200 <--> 3300 mV at 1500 mV 
regulator: SW5: 1200 <--> 1975 mV at 1800 mV 
regulator: SWBST: 
regulator: VPLL: 1200 <--> 1800 mV at 1800 mV 
regulator: VREFDDR: 
regulator: VDAC: 2500 <--> 2775 mV at 2775 mV 
regulator: VUSB: 
regulator: VUSB2: 2500 <--> 3000 mV at 2500 mV 
regulator: VGEN1: 1200 <--> 1550 mV at 1300 mV 
regulator: VGEN2: 2500 <--> 3300 mV at 2500 mV 
mc34708 2-0008: Loaded
Switching to clocksource mxc_timer1
NET: Registered protocol family 2
IP route cache hash table entries: 4096 (order: 2, 16384 bytes)
TCP established hash table entries: 16384 (order: 5, 131072 bytes)
TCP bind hash table entries: 16384 (order: 4, 65536 bytes)
TCP: Hash tables configured (established 16384 bind 16384)
TCP reno registered
UDP hash table entries: 256 (order: 0, 4096 bytes)
UDP-Lite hash table entries: 256 (order: 0, 4096 bytes)
NET: Registered protocol family 1
RPC: Registered udp transport module.
RPC: Registered tcp transport module.
RPC: Registered tcp NFSv4.1 backchannel transport module.
LPMode driver module loaded
Static Power Management for Freescale i.MX5
PM driver module loaded
sdram autogating driver module loaded
Bus freq driver module loaded
DI0 is primary
mxc_dvfs_core_probe
DVFS driver module loaded
i.MXC CPU frequency driver
DVFS PER driver module loaded
Slow work thread pool: Starting up
Slow work thread pool: Ready
NTFS driver 2.1.29 [Flags: R/O].
JFFS2 version 2.2. (NAND) © 2001-2006 Red Hat, Inc.
msgmni has been set to 678
alg: No test for stdrng (krng)
cryptodev: driver loaded.
io scheduler noop registered
io scheduler deadline registered
io scheduler cfq registered (default)
mxcfb_probe: enter
ipu_request_irq: irq:23 mxc_sdc_fb
ipu_request_irq: irq:51 mxc_sdc_fb
Config display port 0
Look for video mode TM080SDHG02 in plat modelist
#### mxcfb_pre_setup[0]:(null)
Reconfiguring framebuffer
mxc_ipu mxc_ipu: Channel already disabled 9
mxc_ipu mxc_ipu: Channel already uninitialized 9
init channel = 9
ipu_init_channel initial IPU_CONF setting 00000000
ipu_init_channel:exiting IPU_CONF setting 00000000
pixclock = 40000000 Hz
ipu_pixel_clk_set_rate DI_BS_CLKGEN0:      50  DI_BS_CLKGEN1   50000
## _ipu_ch_param_init#23# width:800:799 / height:600:599
DMA:23 Info: IPU_CHA_DB_MODE_SEL:00800000 IPU_CHA_CUR_BUF:00800000
************* ipu_init_channel_buffer ******************
ipu_pixel_clk_enable: IPU_DISP_GEN: 1600000
ipu_enable_channel:095FFCFF IDMAC_CHA_EN:00800000
#################### ipu_dump_registers: Start ####################
#################### ipu_dump_registers: Stop ####################
fbcon_init: disable boot-logo (boot-logo bigger than screen).
Console: switching to colour frame buffer device 100x37
mxcfb_probe: show logo
#################### ipu_dump_registers: Start ####################
#################### ipu_dump_registers: Stop ####################
mxcfb_probe: exit
mxcfb_probe: enter
ipu_request_irq: irq:28 mxc_sdc_fb
Config display port 1
Look for video mode 1024x768M-16@60 in plat modelist
fbcvt: 1024x768@60: CVT Name - .786M3
#### mxcfb_pre_setup[1]:(null)
Reconfiguring framebuffer
mxc_ipu mxc_ipu: Channel already disabled 7
mxc_ipu mxc_ipu: Channel already uninitialized 7
allocated fb @ paddr=0x75000000, size=4718592.
mxcfb_probe: show logo
#################### ipu_dump_registers: Start ####################
#################### ipu_dump_registers: Stop ####################
mxcfb_probe: exit
mxcfb_probe: enter
ipu_request_irq: irq:27 mxc_sdc_fb
ipu_request_irq: irq:31 mxc_sdc_fb
pixclock set for 60Hz refresh = 217013 ps
#### mxcfb_pre_setup[-1]:99999999
Reconfiguring framebuffer
mxc_ipu mxc_ipu: Channel already disabled 10
mxc_ipu mxc_ipu: Channel already uninitialized 10
allocated fb @ paddr=0x75480000, size=460800.
mxcfb_probe: show logo
#################### ipu_dump_registers: Start ####################
#################### ipu_dump_registers: Stop ####################
mxcfb_probe: exit
sharp lcd init
sharp lcd spi probe: bus:3 select:4 mode:7
Sharp turning on LCD
sharp_lq043t1dg28_lcd_set_registers
sharp lcd init: exit code:0
Serial: MXC Internal UART driver
mxcintuart.0: ttymxc0 at MMIO 0x53fbc000 (irq = 31) is a Freescale i.MX
mxcintuart.1: ttymxc1 at MMIO 0x53fc0000 (irq = 32) is a Freescale i.MX
console [ttymxc1] enabled, bootconsole disabled

console [ttymxc1] enabled, bootconsole disabled
mxcintuart.2: ttymxc2 at MMIO 0x5000c000 (irq = 33) is a Freescale i.MX

mxcintuart.3: ttymxc3 at MMIO 0x53ff0000 (irq = 13) is a Freescale i.MX

mxcintuart.4: ttymxc4 at MMIO 0x63f90000 (irq = 86) is a Freescale i.MX

loop: module loaded

Wait for CR ACK error!

ahci: probe of ahci.0 failed with error -5

### platform_driver_probe:ahci ret:-19

MXC MTD nand Driver 3.0

vcan: Virtual CAN interface driver

Freescale FlexCAN Driver 

################ res->start:53FC8000 #######################

###### flexcan_set_bitrate: clk_get_rate:66000000

###### flexcan_update_bitrate: src1 / rate:66000000

################ res->start:53FCC000 #######################

###### flexcan_set_bitrate: clk_get_rate:66000000

###### flexcan_update_bitrate: src1 / rate:66000000

FEC Ethernet Driver

fec_enet_mii_bus: probed

ehci_hcd: USB 2.0 'Enhanced' Host Controller (EHCI) Driver

fsl-ehci fsl-ehci.0: Freescale On-Chip EHCI Host Controller

fsl-ehci fsl-ehci.0: new USB bus registered, assigned bus number 1

fsl-ehci fsl-ehci.0: irq 18, io base 0x53f80000

fsl-ehci fsl-ehci.0: USB 2.0 started, EHCI 1.00

usb usb1: New USB device found, idVendor=1d6b, idProduct=0002

usb usb1: New USB device strings: Mfr=3, Product=2, SerialNumber=1

usb usb1: Product: Freescale On-Chip EHCI Host Controller

usb usb1: Manufacturer: Linux 2.6.35.3-1.0-lt-850-gbc67621-svn847 ehci_hcd

usb usb1: SerialNumber: fsl-ehci.0

hub 1-0:1.0: USB hub found

hub 1-0:1.0: 1 port detected

fsl-ehci fsl-ehci.1: Freescale On-Chip EHCI Host Controller

fsl-ehci fsl-ehci.1: new USB bus registered, assigned bus number 2

fsl-ehci fsl-ehci.1: irq 14, io base 0x53f80200

fsl-ehci fsl-ehci.1: USB 2.0 started, EHCI 1.00

usb usb2: New USB device found, idVendor=1d6b, idProduct=0002

usb usb2: New USB device strings: Mfr=3, Product=2, SerialNumber=1

usb usb2: Product: Freescale On-Chip EHCI Host Controller

usb usb2: Manufacturer: Linux 2.6.35.3-1.0-lt-850-gbc67621-svn847 ehci_hcd

usb usb2: SerialNumber: fsl-ehci.1

hub 2-0:1.0: USB hub found

hub 2-0:1.0: 1 port detected

usbcore: registered new interface driver cdc_acm

cdc_acm: v0.26:USB Abstract Control Model driver for USB modems and ISDN adapters

Initializing USB Mass Storage driver...

usbcore: registered new interface driver usb-storage

USB Mass Storage support registered.

ARC USBOTG Device Controller driver (1 August 2005)

mice: PS/2 mouse device common for all mice

MXC keypad loaded

DA9052 TSI Device Driver, v1.0

rtc-m41t80 2-0068: chip found, driver version 0.05

rtc-m41t80 2-0068: rtc core: registered m41t83 as rtc0

rtc-m41t80 2-0068: HT bit was set!

rtc-m41t80 2-0068: Power Down at 2070-01-01 21:23:15

i2c /dev entries driver

IR NEC protocol handler initialized

IR RC5(x) protocol handler initialized

IR RC6 protocol handler initialized

IR JVC protocol handler initialized

IR Sony protocol handler initialized

Linux video capture interface: v2.00

mxc_v4l2_output mxc_v4l2_output.0: Registered device video0

usbcore: registered new interface driver uvcvideo

USB Video Class driver (v0.1.0)

APM Battery Driver

### platform_driver_probe:da9052-adc ret:-19

add mma8450 i2c driver

add mma8451 i2c driver

MXC WatchDog Driver 2.0

MXC Watchdog # 0 Timer: initial timeout 60 sec

Bluetooth: Virtual HCI driver ver 1.3

Bluetooth: HCI UART driver ver 2.2

Bluetooth: HCIATH protocol initialized

Bluetooth: Generic Bluetooth USB driver ver 0.6

usbcore: registered new interface driver btusb

MC34708 PMIC ADC driver loading...

PMIC ADC start probe

Event:0 Subscribe

Event:1 Subscribe

Event:2 Subscribe

PMIC ADC successfully probed

VPU initialized

mxsdhci: MXC Secure Digital Host Controller Interface driver

mxsdhci: MXC SDHCI Controller Driver. 

mmc0: SDHCI detect irq 0 irq 2 INTERNAL DMA

mxsdhci: MXC SDHCI Controller Driver. 

mmc1: SDHCI detect irq 0 irq 3 INTERNAL DMA

usbcore: registered new interface driver usbhid

usbhid: USB HID core driver

Cirrus Logic CS42888 ALSA SoC Codec Driver

No device for DAI imx-ssi-1-0

No device for DAI imx-ssi-1-1

No device for DAI imx-ssi-2-0

No device for DAI imx-ssi-2-1

ALSA device list:

  No soundcards found.

TCP cubic registered

NET: Registered protocol family 10

lo: Disabled Privacy Extensions

NET: Registered protocol family 17

can: controller area network core (rev 20090105 abi 8)

NET: Registered protocol family 29

can: raw protocol (rev 20090105)

can: broadcast manager protocol (rev 20090105 t)

Bluetooth: L2CAP ver 2.14

Bluetooth: L2CAP socket layer initialized

Bluetooth: SCO (Voice Link) ver 0.6

Bluetooth: SCO socket layer initialized

Bluetooth: RFCOMM TTY layer initialized

Bluetooth: RFCOMM socket layer initialized

Bluetooth: RFCOMM ver 1.11

Bluetooth: BNEP (Ethernet Emulation) ver 1.3

Bluetooth: BNEP filters: protocol multicast

Bluetooth: HIDP (Human Interface Emulation) ver 1.2

VFP support v0.3: implementor 41 architecture 3 part 30 variant c rev 2

input: mxc_ts as /devices/virtual/input/input0

mxc input touchscreen loaded

rtc-m41t80 2-0068: setting system clock to 2070-01-01 21:24:18 UTC (3155837058)

Waiting for root device /dev/mmcblk0p1...

mmc1: new high speed MMC card at address 0001

mmcblk0: mmc1:0001 008G4B 7.28 GiB 

 mmcblk0: p1

EXT3-fs: barriers not enabled

EXT3-fs (mmcblk0p1): warning: maximal mount count reached, running e2fsck is recommended

kjournald starting.  Commit interval 5 seconds

EXT3-fs (mmcblk0p1): using internal journal

EXT3-fs (mmcblk0p1): recovery complete

EXT3-fs (mmcblk0p1): mounted filesystem with writeback data mode

VFS: Mounted root (ext3 filesystem) on device 179:1.

Freeing init memory: 612K

bash: cannot set terminal process group (-1): Inappropriate ioctl for device
bash: no job control in this shell
root@(none):/#
```
</details>

{::options parse_block_html="false" /}

The machine is running Linux version 2.6.35 with U-Boot boot loader. In the console output you can see that I have gained root access (root@(none):/#) to the machine, normally
you will be prompted with the user password here (that we don't have). In order to gain root access send an escape character (Esc) 1-3 seconds after turning on the machine, this 
will enter the boot loader. In the boot loader we can temporarily change boot arguments, the one we want to change is bootargs_mmc by appending "init=/bin/bash" to it:

```console
MX53-Hawk U-Boot > setenv bootargs_mmc 'setenv bootargs ${bootargs} root=/dev/mmcblk0p1 rootwait rw single init=/bin/bash'
```
When that is set, simply type

```console
MX53-Hawk U-Boot > boot
```

The machine will now reboot with root access to the operating system. Now we need to find out where the user account information is stored:

```console
root@(none):/# find / -name *user*
```

Looking through the long list of hits from this search, one file and directory stands out:

```console
/etc/abi/config/user.ini
```

As I assume "abi" means Applied Biosystems, Inc. or Applied Biosystems & Invitrogen. Opening the file with nano:

```console
[Service]
password2 = tE9kqpy3ND5TONBMF2T3GA==
level = SERVICE
fullname = Service
phone =
folder =
password = CHBRnIuxpHdZCFIA9rP8pw==
email =
[Administrator]
password2 = s33zFgpE78VbI2n9q040Xw==
level = ADMIN
fullname = Administrator
phone =
folder =
password = bOX4d4s9feAKdTsj9QB2yA==
email =
[THOMAS]
folder = PROTOCOLS
password = WGodXmMnTrjzdVp3RIGKng==
clouduserid = None
level = USER
[Guest]
level = GUEST
fullname = Guest
```
This is exactly what we are looking for, these are all the users on the machine and the corresponding passwords. The passwords are hashed by an unknown algorithm, it's not
a hash format that I recognize. Assuming the keys are generated properly we won't be able to get them in plain text no matter what. Thankfully we won't need that. 

The [THOMAS] user is one I
created on the machine before taking it apart, so I know the password used to generate my hash. Let's just copy the hash and paste it in the password field for the Administrator user and the 
Service user. Now the file will look like this:

```console
[Service]
password2 = WGodXmMnTrjzdVp3RIGKng==
level = SERVICE
fullname = Service
phone =
folder =
password = WGodXmMnTrjzdVp3RIGKng==
email =
[Administrator]
password2 = WGodXmMnTrjzdVp3RIGKng==
level = ADMIN
fullname = Administrator
phone =
folder =
password = WGodXmMnTrjzdVp3RIGKng==
email =
[THOMAS]
folder = PROTOCOLS
password = WGodXmMnTrjzdVp3RIGKng==
clouduserid = None
level = USER
[Guest]
level = GUEST
fullname = Guest
```
The password I used to create my own user now works both for the administrator account and service account.

Done!



