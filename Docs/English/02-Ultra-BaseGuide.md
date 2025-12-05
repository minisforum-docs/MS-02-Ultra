# MS-02 Ultra

MS-02 Ultra is a major upgrade of the MS-01 MINI PC.  
This guide provides a concise introduction to the MS-02 Ultra and important information about memory compatibility, usage tips, and other key details.

**When purchasing RAM, always refer to the official memory shipping list and the QVL list** (see the sections "Official Memory Shipping List" and "Memory QVL List" below).

## Quick Product Overview

### Improvements from MS-01 to MS-02 Ultra
Key upgrades include:

1. Expanded PCIe expandability
   - Partially addresses GPU availability issues by supporting low-profile dual-slot cards (available from Amazon, Taobao, JD, etc.).
   - Up to 3x PCIe slots. If a discrete GPU is not required, the extra slots give more flexibility for expansion.
2. ECC memory support and doubled maximum capacity to 256 GB
   - ECC is supported only on systems with the 285HX CPU.
   - All SKUs support up to 256 GB total memory.
3. Built-in power supply — no external PSU required.
4. Substantially improved CPU performance
   - MS-01 peaked at Core i9-13900H (60W/80W) with 6 P-cores and 8 E-cores. MS-02 Ultra uses HX series chips (285HX up to 8 P + 8 E cores, 100W/140W).
   - Thermal interface has been upgraded to a phase-change material and the cooling duct is a server-grade through-flow design.
   - Even the 235HX (6 P + 8 E cores) outperforms 13900H by ~10–20%.
5. Thunderbolt upgraded from USB4 40Gbps to 2x 80Gbps TBT5 (USB4 v2) and 1x USB4 (40Gbps).
6. Increased chassis volume from 1.7L to 4.8L.

### Usage Tips

### ECC and Memory Details and Memory QVL List
Reference: [MS-02 Ultra Memory Compatibility Document](/Docs/English/02-Ultra-Memory.md)

### Discrete GPU Notes

- Inserting a discrete GPU with display output will, by default, disable the integrated GPU. Use the discrete GPU for display output. You can force integrated graphics to remain enabled under Onboard Devices Setting -> Internal Graphics.
- Supported low-profile GPUs include the `Gigabyte GeForce RTX™ 5060 OC Low Profile` and `ASUS GeForce RTX™ 5060 LP`.
- Each PCIe slot provides the standard 75W PCIe slot power, so GPUs compatible with the MS-01 are supported.
- The internal PSU is rated at 350W. On 285HX systems the default CPU TDP is PL1/PL2 = 100W/140W; when a discrete GPU is installed the CPU TDP will be reduced automatically (because the GPU and CPU share thermal budget) to 90W/110W.
- Installing a dual-slot low-profile GPU will block one PCIe x4 slot, making that slot unusable.

### CPU Power and Limits
This section describes the factory default CPU power settings. PL1 is sustained power; PL2 is short-duration turbo power. Note that installing a GPU reduces the CPU TDP due to shared thermal load.

- When a discrete GPU is installed, CPU TDP is automatically reduced to 90W/110W(285HX).
- You can manually change the current TDP in the BIOS under Power & Performance (note: manual values reset if you remove/insert the GPU).
- The factory fan curve and TDP settings are designed as a balanced default for most scenarios. If you plan to increase sustained TDP, be sure to also increase fan speed per the "Fan Speed Adjustment" section.

| CPU   | No GPU PL1/PL2 | With GPU PL1/PL2 | Turbo Duration | Temperature Limit |
|-------|----------------|------------------|----------------|-------------------|
| 285HX | 100W / 140W    | 90W / 110W       | 32 s           | 90°C              |
| 275HX | 100W / 140W    | 90W / 110W       | 32 s           | 90°C              |
| 235HX | 80W / 100W     | 60W / 100W       | 32 s           | 90°C              |

### Idle Power Consumption
The MS-02 Ultra (285HX version) includes a very powerful 25Gbps NIC. However, this NIC chip has high power consumption, and idle power draw is nearly identical to load power draw.
This table compares idle power consumption between systems with and without the 25G NIC installed on the 285HX.
(Test results are from Windows installations with all drivers installed and no internet connection in idle state)

| CPU | G3 Status | Windows Idle With 25G NIC | Windows Idle NO 25G NIC | BIOS Menu With 25G NIC | BIOS Menu NO 25G NIC |
|-----|-----------|---------------------------|-------------------------|------------------------|----------------------|
| 285HX | 1.55W | 9.8-12-13W | 22W | 46.8W | 52.2W |


### SSD Count and Speeds
With MinisForum's dedicated E810 expansion card installed, the system can support up to 4 SSDs: 2 on the motherboard and 2 on the expansion card. Currently the E810 card ships standard only with 285HX SKUs; 275HX and 235HX SKUs only have the 2 onboard SSDs.

For compatibility, the E810 expansion card's slots are set to PCIe 3.0 x4 by default. You can change them to PCIe 4.0 in BIOS, but after switching it is recommended to run a storage benchmark. If you see anomalies, revert the slot to PCIe 3.0.

Adjust the SSD PCIe speed in BIOS: `Onboard Devices Setting` -> `PCI-E Port` -> `PCIe Speed`.

### Fan Speed Adjustment
MS-02 Ultra uses an EC controller to manage fan speed. Users can adjust fan curves in BIOS:

`Advanced` -> `Hardware Monito`r -> `[XXX Fan Setting]` -> `User Mode`

When User Mode is enabled you can set 4 temperature points and 4 PWM values. PWM ranges up to 250; PWM = 250 corresponds to full fan speed.

### vPro (AMT) Support
Due to Intel CPU limitations, vPro (AMT) is supported only on 285HX systems.

- The 2.5G NIC on 285HX SKUs is I226-LM with WM880 chipset; 275HX/235HX SKUs use I226-V with HM870.
- Only 285HX SKUs support AMT remote management.
- If your system supports vPro, enter the MEBx menu in BIOS to configure vPro/AMT settings.
- Default MEBx password is `admin`. On first use you must change it to a password of at least 8 characters that includes uppercase, lowercase, digits, and a special character.



