# MS-02 Ultra — Memory Compatibility Guide

The MS-02 Ultra is a full upgrade from the MS-01. It supports up to 256 GB of memory (ECC-capable on supported SKUs). Because consumer CPUs provide a 128-bit memory bus, every two memory slots share a 64-bit channel using T-Type traces. Sharing channels increases maximum capacity but reduces the supported memory frequency whether you use 1, 2, or 4 modules.

This document contains all guidance related to MS-02 Ultra memory compatibility.

**When buying RAM, always refer to the official [Official Memory Shipping List](#Official Memory Shipping List) and [Memory QVL List](#Memory QVL List)<**

There are four debug LEDs on the back of the CPU socket; one is the memory LED. If the system is stuck at CPU/memory initialization, memory issues are likely preventing boot.

## ECC Support

Due to Intel SKU restrictions, only systems with the 285HX CPU support ECC memory. 275HX and 235HX SKUs do not support ECC, but all SKUs still support up to 256 GB total memory.

| CPU model | ECC support | Max total memory | CSODIMM |
|-----------|-------------:|-----------------:|--------:|
| 285HX     | ✅           | 256 GB           | ✅      |
| 275HX     | ❌           | 256 GB           | ✅      |
| 235HX     | ❌           | 256 GB           | ✅      |

## Memory Frequency

### Important when using 2 DIMMs
> **Warning**
> When using 2 DIMMs, install them only in the two front (CPU-facing) slots. If you install only in the rear slots, the system will not boot.

### Factory default memory frequency settings

- SAGV: Enabled (dynamic memory frequency downclocking when idle to save power)
- 1R (single-rank): 4800 MHz (modules with memory chips on one side)
- 2R (dual-rank): 4400 MHz (modules with memory chips on both sides)

### Official Memory Shipping List
This list shows memory modules shipped with the product.

| Memory brand & model | Capacity | ECC | 2-DIMM freq | 4-DIMM freq | Native freq | Rank |
|----------------------|---------:|:---:|------------:|------------:|------------:|:----:|
| Kingston KSM56T46BD8KM-48HM | 48 GB | ✅ | 4400 MHz | 4400 MHz | 5600 MHz | 2R |
| Apacer D41.35741H.001      | 48 GB | ✅ | 4400 MHz | 4400 MHz | 5600 MHz | 2R |
| Crucial CT48G56C46S5.M16C1  | 48 GB | NO  | 4400 MHz | 4400 MHz | 5600 MHz | 2R |
| Crucial CT32G56C46S5.C16D(Y52K) | 32 GB | NO | 4400 MHz | 4400 MHz | 5600 MHz | 2R |
| Crucial CT32G56C46S5.C8BA(Y53A) | 32 GB | NO | 4800 MHz | 4800 MHz | 5600 MHz | 1R |
| Adata CBDAD5S560032G-BAD    | 32 GB | NO  | 4400 MHz | 4400 MHz | 5600 MHz | 2R |
| Crucial CT16G56C46S5.C8D(Y52K) | 16 GB | NO | 4800 MHz | 4800 MHz | 5600 MHz | 1R |
| Crucial CBDAD5S560016G-BAD  | 16 GB | NO  | 4800 MHz | 4800 MHz | 5600 MHz | 1R |

### Memory QVL List
This list shows non-official but tested compatible memory. If two DIMMs work, four DIMMs will likely work as well.

| Memory brand & model | Capacity | ECC | Pass | 2-DIMM freq | 4-DIMM freq | Native freq | Rank | Failure notes |
|----------------------|---------:|:---:|:----:|------------:|------------:|------------:|:----:|---------------|
| SK Hynix HMCG88AGBAA095N | 32 GB | NO | ✅ | 4400 MHz |  | 5600 MHz | 2R | |
| SAMSUNG M425R4GA3BB0-CWMOL | 32 GB | NO | ❌ | 4400 MHz |  | 5600 MHz | 2R | Burn-in test error / hang |
| Crucial HMCG88AGBAA095N | 48 GB | NO | ✅ | 4400 MHz |  | 5600 MHz | 2R | |
| TeamGroup TED532G4800C40-SBK | 32 GB | NO | ✅ | 4400 MHz |  | 5600 MHz | 2R | |
| Kingston HMCG88AGBAA095N | 16 GB | NO | ✅ | 4400 / 4800 MHz |  | 5600 MHz | 1R | |
| ADATA AD5S480032G-B | 32 GB | NO | ✅ | 4400 MHz |  | 4800 MHz | 2R | |
| ADATA AD5S560032G-B | 32 GB | NO | ✅ | 4400 MHz |  | 5600 MHz | 2R | |
| Crucial CT24G56C46S5.M8B1 | 32 GB | NO | ✅ | 4400 MHz |  | 5600 MHz | 2R | |
| KINGBANK KN556F2442 | 48 GB | NO | ❌ | 4400 MHz |  | 5600 MHz | 2R | S4, reboot failure |
| GEIL GS516GB5600C46SC | 16 GB | NO | ❌ | 4400 MHz |  | 5600 MHz | 2R | S4/S5 hang |
| SAMSUNG M425R2GA3BB0-CWMOD | 16 GB | NO | ✅ | 4400 / 4800 MHz | 4800 MHz | 5600 MHz | 1R | |
| Colorful NB16G5600D5NP46 | 16 GB | NO | ✅ | 4400 / 4800 MHz |  | 5600 MHz | 1R | |
| JUHOR JH4B50000334 | 16 GB | NO | ✅ | 4400 / 4800 MHz |  | 5600 MHz | 1R | |
| Gloway VGM5SX56C46AG-STACNN | 16 GB | NO | ✅ | 4400 / 4800 MHz |  | 5600 MHz | 1R | |
| Lenovo Generic N Series | 16 GB | NO | ✅ | 4400 / 4800 MHz | 4400 MHz | 5600 MHz | 1R | |

## Maximum Memory Frequency / Overclocking

The MS-02 Ultra can reach higher memory frequencies in some cases, but factory defaults are set lower to maximize compatibility. This document summarizes limited test results and does not guarantee every MS-02 Ultra will behave identically.

Overclocking is a DIY activity. You are responsible for any instability or data loss caused by changing memory settings — MINISFORUM and the document author are not liable.

> **Warning**
> Overclocking is a DIY activity. You are responsible for any instability or data loss caused by memory overclocking.

- The MS-02 Ultra memory design does not support overvolting memory.
- When testing higher frequencies, always run a full MEMTEST.
- Generally, modules from the official compatibility list can reach up to 4800 MHz with 2 DIMMs, and up to 5200 MHz with 4 DIMMs.
- For CSODIMM modules: even if they pass MEMTEST at higher frequencies, long-term stability may be an issue. Do not run them at excessively high frequencies.
- If someone achieves stable operation at higher frequencies, please open an issue to update this document.

| Memory brand & model | Capacity | 2-DIMM max freq | 4-DIMM max freq | CSODIMM |
|----------------------|---------:|----------------:|----------------:|--------:|
| Skhynix HMCGY8MHBWB335N | 48 GB | 5400 MHz | 6000 MHz | YES |
| Crucial CT48G56C46S5.M16C1 | 48 GB | 4800 MHz | 5200 MHz | NO |
| Crucial CT64G56C46S5.M16C1 | 64 GB | 4800 MHz | 5200 MHz | NO |
| Crucial CT32G56C46S5.C8BA(Y53A) | 32 GB | Wait for test | Wait for test | NO |

