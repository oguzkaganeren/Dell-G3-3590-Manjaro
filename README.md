# Dell-G3-3590-Manjaro
```
Machine:   Type: Laptop System: Dell product: G3 3590 v: N/A serial: <filter> 
           Mobo: Dell model: 0NK0C0 v: A00 serial: <filter> UEFI: Dell v: 1.8.0 date: 11/11/2019 
Battery:   ID-1: BAT0 charge: 51.0 Wh condition: 51.0/51.0 Wh (100%) model: LGC-LGC4.474 DELL 415CG9B status: Full 
CPU:       Topology: 6-Core model: Intel Core i7-9750H bits: 64 type: MT MCP arch: Kaby Lake rev: A L2 cache: 12.0 MiB 
           flags: avx avx2 lm nx pae sse sse2 sse3 sse4_1 sse4_2 ssse3 vmx bogomips: 62431 
           Speed: 900 MHz min/max: 800/4500 MHz Core speeds (MHz): 1: 900 2: 900 3: 900 4: 900 5: 901 6: 900 7: 900 8: 900 
           9: 900 10: 900 11: 900 12: 900 
Graphics:  Device-1: Intel UHD Graphics 630 vendor: Dell driver: i915 v: kernel bus ID: 00:02.0 
           Device-2: NVIDIA vendor: Dell driver: nvidia v: 440.44 bus ID: 01:00.0 
           Display: x11 server: X.Org 1.20.7 driver: modesetting,nvidia resolution: 1920x1080~60Hz 
           OpenGL: renderer: Mesa DRI Intel UHD Graphics 630 (Coffeelake 3x8 GT2) v: 4.6 Mesa 19.3.2 direct render: Yes 
Audio:     Device-1: Intel Cannon Lake PCH cAVS vendor: Dell driver: snd_hda_intel v: kernel bus ID: 00:1f.3 
           Device-2: NVIDIA vendor: Dell driver: snd_hda_intel v: kernel bus ID: 01:00.1 
           Sound Server: ALSA v: k5.4.15-2-MANJARO 
Network:   Device-1: Intel Wireless-AC 9560 [Jefferson Peak] driver: iwlwifi v: kernel port: 5000 bus ID: 00:14.3 
           IF: wlo1 state: up mac: <filter> 
           Device-2: Realtek RTL8111/8168/8411 PCI Express Gigabit Ethernet vendor: Dell driver: r8169 v: kernel port: 3000 
           bus ID: 03:00.0 
           IF: enp3s0 state: down mac: <filter> 
           IF-ID-1: br-43cf34126249 state: up speed: N/A duplex: N/A mac: <filter> 
           IF-ID-2: docker0 state: down mac: <filter> 
           IF-ID-3: veth832222a state: up speed: 10000 Mbps duplex: full mac: <filter> 
           IF-ID-4: vethbf94eb0 state: up speed: 10000 Mbps duplex: full mac: <filter> 
Drives:    Local Storage: total: 1.14 TiB used: 126.06 GiB (10.8%) 
           ID-1: /dev/nvme0n1 vendor: Samsung model: PM991 NVMe 256GB size: 238.47 GiB 
           ID-2: /dev/sda vendor: Western Digital model: WD10SPZX-75Z10T2 size: 931.51 GiB
```

Grub config at `/etc/default/grub`
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet apparmor=1 security=apparmor udev.log_priority=3 acpi_osi=Linux acpi_osi='Windows 2015' acpi_enforce_resources=lax"
```
NVIDIA High Definition Audio Controller with ALSA worked after writting `options snd_hda_intel dmic_detect=0` into `/etc/modprobe.d/hda_fix.conf` and `options snd_hda_intel model=laptop-dmic` into `/etc/modprobe.d/alsa-base.conf`

### Android emulator sound problem
In /etc/pulse/default.pa change load-module module-udev-detect to load-module module-udev-detect tsched=0

and in /etc/pulse/daemon.conf change ; default-sample-rate = 44100 to default-sample-rate = 48000

Finally restart pulseaudio with pulseaudio -k
