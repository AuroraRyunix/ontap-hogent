
## Prerequisites:
1. ONTAPsimulator version: 9.16.1
2. Proxmox version: Virtual Environment 9.0.0 (should work fine for any newer releases)
3. DHCP is a nice to have, however not mandatory
4. COFFEE, LOTS OF IT!
5. patience
6. goat.png for when all goes wrong
7. Whatever, yes.

## Info:
- Modified version of ontap. Minor changes for proxmox, comes preloaded with working virtual disks of 9gb, i think 14, however don't shoot the piano player, he's doing his best.
- Kernel-Panic-Proof, kidding.


## Instruction:
1. Download the ONTAPsimulator .ova file: from github releases, or: https://fastapi.zerotwo.cloud/ontap and a .txt file with license keys. (note: this is a modified premade version, with 0 warranty, includes a goat).
2. Unzip the .ova file
3. Upload to the working directory on the Proxmox server all .vmdk files (hint: scp is da wae): 

![image](https://user-images.githubusercontent.com/115875629/208489743-128dddcb-e640-4a71-80e4-edeb286c296b.png)

4. Create a virtual machine with settings shown on screenshots:

![image](https://user-images.githubusercontent.com/115875629/208490420-a41dff11-6433-460a-aee2-617cef774f6b.png)

![image](https://user-images.githubusercontent.com/115875629/208490618-1e65522a-b466-4a83-a28d-ebf5bb651a85.png)

![image](https://user-images.githubusercontent.com/115875629/208490733-813ddad6-8b17-498f-b8e9-9a80914868d4.png)

5. Delete created by default disk and leave it without disks:
  
![image](https://user-images.githubusercontent.com/115875629/208490976-3a62d297-328d-48ca-a764-2b48887753a8.png)

6. Change the amount of the Cores to four and set the Type to SandyBridge (important!):

![image](https://user-images.githubusercontent.com/115875629/208504451-8a6c0601-beca-45c9-ae2f-72b0576fab0d.png)

7. Set the size of the Memory to **16** **GB** (needed by this version ONTAPsimulator for one node cluster):



## Very Important Notes
1. Proxmox backup of the ONTAPsimulator (done on a working VM) (same goes for snapshots, or whatever they call them in da prox, i do not use it) does not protect the simulator. After the restoration from the backup, the internal database is corrupted and the simulator is not usable.

![image](https://user-images.githubusercontent.com/115875629/208877343-6e64c962-7323-46d4-a899-2689f4b6aef1.png)

After reboot:

![image](https://user-images.githubusercontent.com/115875629/208877560-6fbf7fff-f0cd-4de4-bda3-978a52a13413.png)

The backup of the VM should be done when it is switched off.

2. A single node ONTAP cluster can be switched off from CLI (I did not test it with two node cluster):
```
system node halt
```

![image](https://user-images.githubusercontent.com/115875629/208902035-bca9578f-fa35-4a7f-b620-83be2c7af14e.png)

When the system is waiting for physical power off, a VM with ONTAPsimulator can be safely switched off (via the Stop option in Proxmox).

![image](https://user-images.githubusercontent.com/115875629/208902434-99434e30-4c7d-42ec-9bb1-4c87e37cab9b.png)

3. To be honest, I have to mention, that on VMware Workstation I had to create a new simulator - almost every time when I powered it off. To be sure that switching off the ONTAPsimulator will not destroy it, you can take into account hibernation instead of powering it off. This kind of "stopping" ONTAP allows predicting with a higher probability that nothing will happen with the simulator. I did it many times with success.
