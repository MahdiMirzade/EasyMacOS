![alt text](https://raw.githubusercontent.com/msxtm/ScreenShots/master/EasyMacOS_LockScreen.png "Mojave's Screen Lock")

<center><h1> EasyMacOS-KVM </h1></center>
Read this documentation to set up a simple macOS VM in QEMU, accelerated by [KVM](https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine).

New to macOS and KVM? Check [the FAQs.](docs/FAQs.md)

Want Installation Toturials? 🇦🇺 [English(Global)](https://www.youtube.com/watch?v=6ZihYY6YMxM) | 🇮🇷 Persian : ❌

### Getting Started
You'll need a Linux system with `qemu` _`(3.1 or later)`_, `python3`, `pip` and the KVM modules enabled. A Mac is **not** required. Some examples for different distributions:

![alt text](https://raw.githubusercontent.com/msxtm/ScreenShots/master/EasyMacOS_InstallNeeded.png "Install Requirements for your linux pc.")

### How To Install
To Install your own MacOS, You have to follow these steps.

#### Step 1
Run `jumpstart.sh` to download installation media for MacOS (internet required). The default installation uses Catalina, but you can choose which version to get by adding either `--high-sierra`, `--mojave`, or `--catalina`. For example:
```
./jumpstart.sh --mojave
```
![alt text](https://raw.githubusercontent.com/msxtm/ScreenShots/master/EasyMacOS_JumpStart.png "Jumpstart's Help Instructions")
> Note: You can skip this if you already have `BaseSystem.img` downloaded, But if you have `BaseSystem.dmg`, you will need to convert it with the `dmg2img` tool.

#### Step 2
Create an empty hard disk using `qemu-img`, changing the name and size to preference:
```
qemu-img create -f qcow2 MyDisk.qcow2 32G
```

and add it to the end of `basic.sh`:
```
    -drive id=SystemDisk,if=none,file=MyDisk.qcow2 \
    -device ide-hd,bus=sata.4,drive=SystemDisk \
```
![alt text](https://raw.githubusercontent.com/msxtm/ScreenShots/master/EasyMacOS_Basic.png "Basic's Added Lines")
> Note: If you're running on a headless system (such as on Cloud providers), you will need `-nographic` and `-vnc :0 -k en-us` for VNC support.

Then run `basic.sh` to start the machine and install macOS. Remember to partition in Disk Utility first!

##### Step 2.a (Virtual Machine Manager)
1. If instead of QEMU, you'd like to import the setup into Virt-Manager for further configuration, just run `sudo ./make.sh --add`.
2. After running the above command, add `MyDisk.qcow2` as storage in the properties of the newly added entry for VM.

##### Step 2.b (Headless Systems)
If you're using a cloud-based/headless system, you can use `headless.sh` to set up a quick VNC instance. Settings are defined through variables as seen in the following example. VNC will start on port `5900` by default.
```
HEADLESS=1 MEM=2G CPUS=2 SYSTEM_DISK=MyDisk.qcow2 ./headless.sh
```

#### Step 3

You're done!

To fine-tune the system and improve performance, look in the `docs` folder for more information on [adding memory](docs/guide-performance.md), setting up [bridged networking](docs/guide-networking.md), adding [passthrough hardware (for GPUs)](docs/guide-passthrough.md), tweaking [screen resolution](docs/guide-screen-resolution.md), and enabling sound features.
<br />
**This code is By** [@Foxlet](https://github.com/foxlet), <b>and the help of many others, 
    But MSX have developed a cleaner version of it, so you can enjoy ! </b>
    
    ![alt text](https://raw.githubusercontent.com/msxtm/ScreenShots/master/EasyMacOS_AboutThisMac.png "About This Mac's Screen Shoot")

