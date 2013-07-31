VirtualBox
----------
Run
```bash
sudo modprobe vboxdrv
```
before running vagrant up
If 

```bash
Progress state: NS_ERROR_FAILURE
VBoxManage: error: Failed to create the host-only adapter
VBoxManage: error: VBoxNetAdpCtl: Error while adding new interface: failed to open /dev/vboxnetctl: No such file or directory

VBoxManage: error: Details: code NS_ERROR_FAILURE (0x80004005), component HostNetworkInterface, interface IHostNetworkInterface
VBoxManage: error: Context: "int handleCreate(HandlerArg*, int, int*)" at line 68 of file VBoxManageHostonly.cpp
```
check what modules are loaded
```bash
spoygg@phoenix /m/d/R/itsmyplay> lsmod | grep vbox
vboxdrv              1823456  0 
```
not good
fix
```bash
spoygg@phoenix /m/d/R/itsmyplay> sudo modprobe -vv vboxnetadp
modprobe: INFO: custom logging function 0x40ab30 registered
insmod /lib/modules/3.10.3-1-ARCH/extramodules/vboxnetadp.ko.gz 
modprobe: INFO: context 0x1b8c1e0 released
spoygg@phoenix /m/d/R/itsmyplay> sudo modprobe -vv vboxnetflt
modprobe: INFO: custom logging function 0x40ab30 registered
insmod /lib/modules/3.10.3-1-ARCH/extramodules/vboxnetflt.ko.gz 
modprobe: INFO: context 0x17e51e0 released
```

check
```bash
spoygg@phoenix /m/d/R/itsmyplay> lsmod | grep vbox
vboxnetflt             17612  0 
vboxnetadp             18323  0 
vboxdrv              1823456  2 vboxnetadp,vboxnetflt
```
nice

Git (temporary here)
--------------------
Do partial git push, push until commit with thelonghash.
```bash
git push origin <thelonghash>:master
```
