# macOS-Install-on-VMware
Guide with step-by-step instructions to install macOS on VMware, including configuration files and setup tips for smooth installation.

🖥️ macOS Installation on VMware Workstation Pro (Cheatsheet)

---

## **1. Hardware Requirements**

- **80 GB free space**
- **Virtualization enabled** in BIOS
- **8 GB RAM minimum**

---

## **2. Install VMware Workstation Pro**

Download & install:

🔗 https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion

---

## **3. Download Required Files**

- macOS ISO →
    
    🔗 https://archive.org/details/macos_iso
    
- Unlocker Tool →
    
    🔗 https://github.com/paolo-projects/auto-unlocker
    

---

## **4. Unlock VMware for macOS**

1. Extract **Unlocker ZIP**.
2. Run **Unlocker.exe** (as Admin).
3. Click **Patch → OK**.

---

## **5. Create New Virtual Machine**

1. Open VMware → **Create New VM**.
2. Select **I will install the OS later**.
3. Choose **macOS** (thanks to Unlocker) → Select Version.
4. Enter VM Name → Next.
5. Select **Store virtual disk as single file** → Finish.

---

## **6. Configure VM Settings**

1. Right-click VM → **Edit VM Settings**.
2. Allocate **CPU, RAM** (at least 8 GB).
3. CD/DVD (SATA) → **Use ISO Image File** → Load macOS ISO.
4. Network Adapter → **NAT**.
5. Display → Enable **Accelerate 3D Graphics** (optional).
6. Options → Advanced → **Firmware Type: UEFI only**.

---

## **7. Patch the VMX File**

1. Right-click VM → **Open VM Directory**.
2. Open **macOS.vmx** in Notepad.
3. Find:
    
    ```
    ethernet0.VirtualDev = "e1000e"
    
    ```
    
    Replace with:
    
    ```
    ethernet0.VirtualDev = "vmxnet3"
    
    ```
    

### Intel PCs → Add at end:

```
smbios.reflectHost = "TRUE"
hw.model = "MacBookPro14,3"
board-id = "Mac-551B86E5744E2369"
smc.version = "0"

```

### AMD PCs → Add at end:

```
smc.version = "0"
cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111"
smbios.reflectHost = "TRUE"
hw.model = "MacBookPro14,3"
board-id = "Mac-551B86E5744E2388"

```

1. Save & close file.

---

## **8. Install macOS**

1. Start VM → Apple logo appears.
2. Select **Language** → Continue.
3. Open **Disk Utility** → Select *Vmware Virtual SATA Harddrive Media*.
    - Name: `macOS`
    - Format: **APFS**
    - Scheme: **GUID Partition Map**
    - Click **Erase** → Done.
4. Close Disk Utility → Select **Install macOS [Version]**.
5. Agree to Terms → Choose `macOS` Disk.
6. Installation (20–30 minutes).
7. Complete initial macOS setup.

---

## **9. Enable Full Screen (VMware Tools)**

1. Download VMware Tools **v11.3.5** (only version supporting macOS):
    
    🔗 https://support.broadcom.com/group/ecx/productfiles?subFamily=VMware%20Tools&displayGroup=VMware%20Tools%2011.x&release=11.3.5&os=&servicePk=203551&language=EN&freeDownloads=true
    
2. Extract `darwin.iso`.
3. VMware → Edit VM → **CD/DVD (SATA)** → Use ISO → Select `darwin.iso`.
4. Boot VM → VMware Tools icon on desktop.
5. Install → Enter password → Approve installation.
6. macOS → **System Preferences > Security & Privacy** → Allow **VMware, Inc.**.
7. Restart VM.

✅ macOS now runs **full screen with VMware Tools**!
