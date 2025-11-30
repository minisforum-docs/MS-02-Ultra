# MS-02 Ultra内存兼容性文档
MS-02 Ultra是从MS-01的全面升级。最大支持了256GB的ECC内存  
但是因为消费级CPU仅有128Bit通道，每2个内存槽通过T-Type走线共享64Bit的内存通道  
采用共享内存通道能够提升最大的内存容量，但是会导致不管是1根还是2根还是4根的能支持的内存频率降低  

此文档包含所有有关MS-02 Ultra有关内存兼容性的Guide  

<font color="#dd0000">购买内存时，请务必参考官方的[内存出厂清单](#内存官方出厂清单)和[QVL清单](#内存qvl清单)</font><br />

MS-02 Ultra的CPU背面有4个DEBUG灯，其中有内存灯，如果是卡CPU/内存，那很有可能是内存原因导致无法启动




## ECC支持
由于Intel官方的CPU SKU限制，仅285HX CPU支持ECC内存。 275HX，235HX不支持ECC内存，但是仍然支持最大256GB的内存容量
|  CPU型号  | ECC 支持 |最大内容容量|CSODIMM|
|-----------|--------------|--------------|--------------|
| 285HX | ✅ |256GB|✅|
| 275HX|❌ |256GB|✅|
| 235HX|❌ |256GB|✅|

## 内存频率

### 2根内存条时特别留意
> **警告**
> 使用2根内存条时，只能插正面（CPU面）的两个内存插槽，如果只插背面的内存插槽，会无法开机！！


### 出厂默认内存频率设定

- SAGV: 启用(系统没有负载的时候会降低内存频率节省功耗的功能)
- 1R: 4800Mhz(只有一面有内存颗粒的内存就是1R)
- 2R: 4400Mhz(2面都有内存颗粒的内存就是2R)

### 内存官方出厂清单
此列表展示官方出货的内存  
|  内存品牌和型号 | 容量 |ECC |2根频率 | 4根频率 |原生频率 |1R/2R|
|-----------|--------------|---|---|--------------|---- |---- |
| Kingston KSM56T46BD8KM-48HM| 48GB |✅| 4400Mhz |4400Mhz |5600Mhz |2R |
| Apacer D41.35741H.001| 48GB |✅| 4400Mhz |4400Mhz |5600Mhz |2R |
| Crucial CT48G56C46S5.M16C1| 48GB |NO| 4400Mhz |4400Mhz |5600Mhz |2R |
| Crucial CT32G56C46S5.C16D(Y52K)| 32GB |NO| 4400Mhz |4400Mhz |5600Mhz |2R |
| Crucial CT32G56C46S5.C8BA(Y53A)| 32GB |NO| 4800Mhz |4800Mhz |5600Mhz |1R |
| Adata CBDAD5S560032G-BAD| 32GB |NO| 4400Mhz |4400Mhz |5600Mhz |2R |
| Crucial CT16G56C46S5.C8D(Y52K)| 16GB |NO| 4800Mhz |4800Mhz |5600Mhz |1R |
| Crucial CBDAD5S560016G-BAD| 16GB |NO| 4800Mhz |4800Mhz |5600Mhz |1R |


### 内存QVL清单
此列表展示非官方出货匹配的内存  
2根内存能使用，大概率4根内存也能使用  
|  内存品牌和型号 | 容量 |ECC |PASS|2根频率 | 4根频率 |原生频率 |1R/2R|失败详情|
|-----------|--------------|---|----|--------------|---- |---- |---- |-|
| SK Hynix HMCG88AGBAA095N| 32GB |NO|✅| 4400Mhz |  |5600Mhz |2R ||
| SAMSUNG M425R4GA3BB0-CWMOL| 32GB |NO|❌| 4400Mhz |  |5600Mhz |2R |Burnin测试报错卡死|
| Crucial HMCG88AGBAA095N| 48GB |NO|✅| 4400Mhz |  |5600Mhz |2R ||
| TeamGroup TED532G4800C40-SBK| 32GB |NO|✅| 4400Mhz |  |5600Mhz |2R ||
| Kingston HMCG88AGBAA095N| 16GB |NO|✅| 4400Mhz/4800Mhz |  |5600Mhz |1R ||
| ADATA AD5S480032G-B| 32GB |NO|✅| 4400Mhz |  |4800Mhz |2R ||
| ADATA AD5S560032G-B| 32GB |NO|✅| 4400Mhz |  |5600Mhz |2R ||
| Crucial CT24G56C46S5.M8B1| 32GB |NO|✅| 4400Mhz |  |5600Mhz |2R ||
| KINGBANK KN556F2442| 48GB |NO|❌| 4400Mhz |  |5600Mhz |2R |S4,Reboot失败|
| GEIL(金邦) GS516GB5600C46SC| 16GB |NO|❌| 4400Mhz |  |5600Mhz |2R |S4,S5卡死|
| SAMSUNG M425R2GA3BB0-CWMOD| 16GB |NO|✅| 4400Mhz/4800Mhz | 4800Mhz  |5600Mhz |1R ||
| SAMSUNG M425R2GA3BB0-CWMOD| 16GB |NO|✅| 4400Mhz/4800Mhz | 4800Mhz  |5600Mhz |1R ||
| Colorful NB16G5600D5NP46| 16GB |NO|✅| 4400Mhz/4800Mhz |  |5600Mhz |1R ||
| JUHOR JH4B50000334| 16GB |NO|✅| 4400Mhz/4800Mhz |  |5600Mhz |1R ||
| Gloway VGM5SX56C46AG-STACNN |16GB |NO|✅| 4400Mhz/4800Mhz |  |5600Mhz |1R ||
| Lenovo 联想通用系列N |16GB |NO|✅| 4400Mhz/4800Mhz | 4400Mhz |5600Mhz |1R ||


### 最高内存频率/超频

MS-02 Ultra实际上能够跑到更高的内存频率上，但是为了能兼容更多的内存，将默认的出厂频率调整为比较低的频率上  
此文档仅描述目前的少量的测试结果，不代表每一台MS-02 Ultra的实际情况   
并且非常注意，超频是一种DIY行为，你需要自己对内存频率的调整负责，MINISFORUM和此文档的制作者不会为你因为调整内存带来的不稳定进而导致的数据丢失等付任何责任。

> **警告**
> 超频是一种DIY行为，你需要自己对内存频率的调整负责，MINISFORUM和此文档的制作者不会为你因为调整内存带来的不稳定进而导致的数据丢失等付任何责任。

超频内存需要先关闭SAGV动态内存省电功能  
`Advanced` -> `Onboard Devices Setting` -> `SAGV`
  
然后在
`Advanced` -> `Onboard Devices Setting` -> `Maximum Memory Frequency`里面调整频率X


- MS-02 Ultra内存设计不支持超内存电压
- 探索内存频率时，务必至少也要跑完完整的MEMTEST
- 一般来说，在官方的兼容列表内的内存，插2根的时候，可以最高调到4800，插入4根的时候可以最高调到5200Mhz
- 对于CSODIMM内存。虽然能够以较高的频率通过MEMTEST测试，但是可能长期使用也会有问题。不建议太高内存频率
- 如果有人能够稳定的跑到更高的频率欢迎提issue来更新此文档

|  内存品牌和型号 | 容量 | 2根最大频率 | 4根最大频率 | CSODIMM |
|-----------|--------------|---|--------------|--------------|
| Skhynix HMCGY8MHBWB335N | 48GB | 5400Mhz |6000Mhz|YES|
| Crucial CT48G56C46S5.M16C1| 48GB |4800Mhz |5200Mhz|NO|
| Crucial CT64G56C46S5.M16C1| 64GB |4800Mhz |5200Mhz|NO|
| Crucial CT32G56C46S5.C8BA(Y53A)| 32GB | Wait for Test |Wait for Test |NO|

