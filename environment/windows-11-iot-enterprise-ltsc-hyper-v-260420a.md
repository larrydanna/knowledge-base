# Windows 11 IoT Enterprise LTSC in Hyper-V

**Date:** 2026-04-20  
**Category:** environment  
**Tags:** `windows`, `hyper-v`, `iot`, `ltsc`, `virtualization`, `vm`  
**Related:** [Workstation Setup — Windows 10 / 11](workstation-setup-windows-260413a.md) · [Windows 11 Remote Desktop Access](windows-remote-desktop-260420a.md)

---

## TL;DR

- Download the official evaluation ISO from the Microsoft Evaluation Center and use the x64 build unless you specifically need ARM64
- On the host, enable Hyper-V, then create a **Generation 2** VM with Secure Boot enabled, a vTPM, at least 8 GB startup RAM, and a 64 GB+ VHDX
- Install and customize the VM like a normal Windows machine, but avoid Microsoft Store app updates if you plan to generalize it later
- For a reusable base image, run `sysprep /generalize /oobe /mode:vm /shutdown`, keep that VHDX as the parent image, and create new VM instances from child differencing disks
- Use checkpoints for short-term rollback only; do not treat long checkpoint chains as your cloning or template strategy

---

## Download the Windows 11 IoT Enterprise LTSC ISO

Microsoft provides Windows 11 IoT Enterprise LTSC as an evaluation download through the Evaluation Center. For dev/test work, that is the cleanest starting point because you get a standard ISO and don't need OEM media. [1]

Recommended choice:

- **Architecture:** x64 for most developer workstations
- **Use ARM64 only** if your host and intended tooling specifically require it

Keep the ISO somewhere stable on the host, for example:

```powershell
New-Item -ItemType Directory -Path "D:\ISO" -Force
```

---

## Enable Hyper-V on the host

Hyper-V on Windows requires **Windows 11 Pro or Enterprise** on the host. If Hyper-V is not already enabled, turn it on in an elevated PowerShell session and reboot when prompted. [2]

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

If you want your VM to appear as a separate machine on your LAN, create an **External** virtual switch in Hyper-V Manager. If you just need outbound internet access and easy setup, the **Default Switch** is fine.

---

## Create the VM in Hyper-V

Use Hyper-V Manager for the first VM so you can confirm the settings visually. Microsoft recommends **Generation 2** unless you have a specific compatibility reason not to. [3]

### Recommended starter settings

| Setting | Recommendation |
|---|---|
| Generation | **Generation 2** |
| Startup memory | **8 GB** |
| Dynamic memory | On; min **4 GB**, max **16 GB** |
| Virtual processors | **4** |
| Disk | **100 GB dynamic VHDX** |
| Network | **Default Switch** or your External switch |
| Security | **Secure Boot on**, **Enable Trusted Platform Module** |

Windows 11 setup expects Secure Boot and TPM support. On a Gen 2 VM, leave Secure Boot enabled and turn on the virtual TPM in **Settings → Security** before installation if needed.

### Hyper-V Manager steps

1. Open **Hyper-V Manager**
2. Select **New → Virtual Machine**
3. Choose **Generation 2**
4. Set startup memory to **8192 MB**
5. Attach a virtual switch
6. Create a new **100 GB** VHDX
7. Choose **Install an operating system from a bootable image file** and point to the ISO
8. Finish the wizard
9. Open the VM's **Settings** and confirm **Secure Boot** is enabled
10. In **Security**, enable **Trusted Platform Module**
11. Start the VM and install Windows normally

### PowerShell example

This is a good repeatable baseline once you know the GUI flow. Adjust paths and switch name to match your host.

```powershell
$vmName = "Win11-IoT-LTSC-Dev-01"
$vmPath = "D:\Hyper-V\$vmName"
$isoPath = "D:\ISO\Windows11IoTEnterpriseLTSC_x64.iso"
$vhdPath = "$vmPath\$vmName.vhdx"

New-VM -Name $vmName `
  -Generation 2 `
  -Path $vmPath `
  -MemoryStartupBytes 8GB `
  -NewVHDPath $vhdPath `
  -NewVHDSizeBytes 100GB `
  -SwitchName "Default Switch"

Set-VMProcessor -VMName $vmName -Count 4
Set-VMMemory -VMName $vmName `
  -DynamicMemoryEnabled $true `
  -MinimumBytes 4GB `
  -StartupBytes 8GB `
  -MaximumBytes 16GB

Add-VMDvdDrive -VMName $vmName -Path $isoPath
Set-VMFirmware -VMName $vmName -EnableSecureBoot On `
  -FirstBootDevice (Get-VMDvdDrive -VMName $vmName)
Set-VMKeyProtector -VMName $vmName -NewLocalKeyProtector
Enable-VMTPM -VMName $vmName
Start-VM -Name $vmName
```

---

## Configure the VM as your base development machine

After Windows is installed, treat it like a normal workstation build:

1. Apply Windows Updates
2. Install your common dev tooling
3. Configure VS Code, Git, shells, SDKs, and package managers
4. Remove anything you know you never want in cloned images

Use [Workstation Setup — Windows 10 / 11](workstation-setup-windows-260413a.md) as the follow-on checklist for the dev stack.

### Important Sysprep-friendly habit

If this VM will become your reusable base image, prefer **winget**, MSI installers, and direct vendor installers over installing or updating apps from the **Microsoft Store**. Microsoft notes that Store app updates can cause `Sysprep /generalize` to fail because those app packages become user-specific. [4]

---

## Capture a reusable gold image

For multiple future VMs, the best default pattern is:

1. Build one clean **gold** VM
2. Generalize it with Sysprep
3. Preserve its VHDX as the parent image
4. Create each new VM from a child differencing disk

This gives you fast spin-up while keeping each VM independent.

### Generalize the base VM

Inside the guest, run Sysprep from an elevated command prompt or PowerShell session. Microsoft explicitly documents `/mode:vm` for images that stay on the same hypervisor class. [4]

```powershell
%WINDIR%\System32\Sysprep\Sysprep.exe /generalize /oobe /mode:vm /shutdown
```

What this does:

- `/generalize` removes machine-specific identity data
- `/oobe` makes the next boot go through first-run setup
- `/mode:vm` optimizes the image for VM reuse
- `/shutdown` leaves the disk in a safe state to capture

Best practices:

- **Do not boot the gold VM again** after Sysprep unless you intend to re-customize and re-capture it
- Copy the resulting parent VHDX to a dedicated templates folder
- Mark the parent VHDX as read-only so you do not accidentally attach it directly to a writable VM

Example host-side organization:

```powershell
New-Item -ItemType Directory -Path "D:\Hyper-V\Templates" -Force
Copy-Item "D:\Hyper-V\Win11-IoT-LTSC-Dev-01\Win11-IoT-LTSC-Dev-01.vhdx" `
  "D:\Hyper-V\Templates\Win11-IoT-LTSC-Dev-Base.vhdx"
Set-ItemProperty "D:\Hyper-V\Templates\Win11-IoT-LTSC-Dev-Base.vhdx" `
  -Name IsReadOnly -Value $true
```

### Create fast new VM instances from differencing disks

Hyper-V supports differencing disks directly. The child VHDX stores only the changes while the parent remains untouched. Microsoft documents differencing VHDX creation in `New-VHD`, and Microsoft performance guidance recommends keeping differencing chains short. [5, 7]

```powershell
$parent = "D:\Hyper-V\Templates\Win11-IoT-LTSC-Dev-Base.vhdx"
$vmName = "Win11-IoT-LTSC-Dev-02"
$vmPath = "D:\Hyper-V\$vmName"
$child = "$vmPath\$vmName.vhdx"

New-Item -ItemType Directory -Path $vmPath -Force | Out-Null
New-VHD -Path $child -ParentPath $parent -Differencing

New-VM -Name $vmName `
  -Generation 2 `
  -Path $vmPath `
  -MemoryStartupBytes 8GB `
  -VHDPath $child `
  -SwitchName "Default Switch"

Set-VMProcessor -VMName $vmName -Count 4
Set-VMMemory -VMName $vmName `
  -DynamicMemoryEnabled $true `
  -MinimumBytes 4GB `
  -StartupBytes 8GB `
  -MaximumBytes 16GB
Set-VMKeyProtector -VMName $vmName -NewLocalKeyProtector
Enable-VMTPM -VMName $vmName
Start-VM -Name $vmName
```

Use this pattern when you want **fresh machine identities** and **fast provisioning** with minimal extra disk consumption.

---

## When to export/import instead

Hyper-V export/import is useful when you want to archive or move a known-good VM. The **Copy** import type generates a new Hyper-V VM ID, which is convenient for duplication on the same host. [6]

```powershell
Export-VM -Name "Win11-IoT-LTSC-Dev-01" -Path "D:\Hyper-V\Exports"
```

```powershell
Import-VM `
  -Path "D:\Hyper-V\Exports\Win11-IoT-LTSC-Dev-01\Virtual Machines\<vmcx-file>.vmcx" `
  -Copy `
  -GenerateNewId
```

Use export/import when:

- You want a portable backup of the VM
- You want to move the VM to another Hyper-V host
- You want a copy of the same machine state for one-off experiments

Do **not** confuse a new Hyper-V VM ID with a new Windows machine identity. If you need multiple concurrently running clones that behave like distinct machines, the **Sysprep + parent VHDX + differencing disk** workflow is the safer default.

---

## Avoid using checkpoints as your image strategy

Checkpoints are great before risky changes such as SDK upgrades, Visual Studio installs, or registry edits. They are **not** the right long-term mechanism for building a reusable VM catalog.

Why:

- They create differencing disk chains
- Long chains add I/O overhead
- They are easier to break with storage moves, merges, or interrupted maintenance

Use checkpoints for **temporary rollback**, then merge or delete them once the change is accepted.

---

## Suggested host folder layout

Keeping a predictable layout makes repeatable VM creation much easier.

```text
D:\ISO\
D:\Hyper-V\Templates\
D:\Hyper-V\Exports\
D:\Hyper-V\Win11-IoT-LTSC-Dev-01\
D:\Hyper-V\Win11-IoT-LTSC-Dev-02\
```

That gives you:

- a stable place for ISO files
- a protected location for gold parent disks
- a separate archive area for exports
- one folder per running VM

---

## Sources

[1] [Windows 11 IoT Enterprise LTSC Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-iot-enterprise-ltsc)  
[2] [Install Hyper-V in Windows and Windows Server](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/install-hyper-v)  
[3] [Create a virtual machine in Hyper-V](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine)  
[4] [Sysprep (Generalize) a Windows installation](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation)  
[5] [New-VHD (Hyper-V)](https://learn.microsoft.com/en-us/powershell/module/hyper-v/new-vhd)  
[6] [Export and import virtual machines](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/deploy/export-and-import-virtual-machines)  
[7] [Hyper-V storage I/O performance tuning](https://learn.microsoft.com/en-us/windows-server/administration/performance-tuning/role/hyper-v-server/storage-io-performance#virtual-hard-disk-types)
