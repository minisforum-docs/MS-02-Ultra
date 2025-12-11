# MS-02 Ultra — Known Issues

This document lists all known issues for released MS-02 Ultra models and their corresponding workarounds.

---
## Table of Contents

- [PCIe SMBus Causing Boot Failure](#pcie-smbus-causing-boot-failure)
- [RTL8127 Driver Leaves Device Unbootable After Shutdown](#rtl8127-driver-leaves-device-unbootable-after-shutdown)

## PCIe SMBus Causing Boot Failure

### Summary
If inserting a PCIe device prevents the system from booting, try disabling (shielding) the PCIe SMBus lines.

### Details
The PCH (Platform Controller Hub) provides only a single SMBus channel. To implement full PCIe functionality, the MS-02 Ultra shares the same SMBus routing between the memory module and the PCIe device.

- The memory SMBus is used for memory configuration and frequency negotiation and is critical for proper memory initialization.
- Some PCIe devices implement SMBus incorrectly or pull the bus low, which can disrupt memory SMBus communication and prevent boot.
- Certain PCIe devices (for example, some Intel Optane PCIe SSDs) may present themselves in a way that interferes with SODIMM frequency negotiation, causing the system to fail to boot or the memory not to be recognized.

### Workaround
Mask the PCIe connector SMBus/JTAG pins by applying double-sided tape to physically cover pins 5–9 on the PCIe edge connector (covering at least pins 5 and 6 is essential). This prevents the PCIe device from connecting its SMBus to the shared line.

PCIe front 11 pins (A/B sides) — mask pins 5–9:

| Pin | B-side | A-side | Description |
|-----:|--------|--------|-------------|
| 1 | +12V | PRSNT1# | Connects to PRSNT2# pin |
| 2 | +12V | +12V | Main power |
| 3 | +12V | +12V | Main power |
| 4 | GND | GND | Ground |
| 5 | SMCLK | TCK | SMBUS and JTAG port |
| 6 | SMDAT | TDI | SMBUS and JTAG port |
| 7 | Ground | TDO | SMBUS and JTAG port |
| 8 | +3.3V | TMS | SMBUS and JTAG port |
| 9 | TRST# | +3.3V | SMBUS and JTAG port |
| 10 | +3.3V AUX | +3.3V | Aux / standby power |
| 11 | WAKE# | PERST | Link reactivation / fundamental reset |

Note: Use non-conductive tape and make sure only the intended pins are masked.

---

## RTL8127 Driver Leaves Device Unbootable After Shutdown

### Summary
A built-in Linux kernel `r8169` driver in some kernels may leave Realtek RTL8127 NICs in a state after shutdown that prevents the system from powering on again.

### Cause
Certain `r8169` driver implementations on shutdown can put RTL8127 hardware into a non-standard state that disables the NIC's `Power_En` signal. Without this signal the system may fail to start properly on the next power-on attempt.

### Temporary workaround
In BIOS, go to `On Board Setting` and disable the RTL8127 onboard network device to quickly verify whether this is the cause.

### Recommended solution (Solution 1): Install RTL8127 DKMS driver
This is the preferred fix. Use the DKMS package built for RTL8127.

- Download the DKMS package:
  - Example: `https://github.com/minisforum-repo/r8127-dkms/releases/download/11.015.00-1/r8127-dkms_11.015.00-1_all.deb`

PVE / Proxmox VE (ensure you have the No-Subscription repository configured):
```bash
apt update
apt install dkms pve-headers-$(uname -r)
dpkg -i r8127-dkms_11.015.00-1_all.deb
# Reboot and test
```

Ubuntu / Debian:
```bash
apt update
apt install dkms linux-headers-$(uname -r)
dpkg -i r8127-dkms_11.015.00-1_all.deb
# Reboot and test
```

#### Solution 2: Obtain the Latest Driver from Realtek
Visit: https://www.realtek.com/Download/List?cate_id=584
Download `10G Ethernet LINUX driver r8127 for kernel up to 6.15` and upload it to MS-02 Ultra, then extract.

```bash
apt update

# For PVE system, ensure Proxmox VE No-Subscription Repository is installed
# For PVE system, install PVE Kernel Header and related software
apt install gcc make pve-headers-$(uname -r)


# For Ubuntu/Debian, install Kernel Header and related software
apt install gcc make  linux-headers-$(uname -r)


# Navigate to the directory and run the installation
cd r8127-11.015.00
./autorun.sh
```


