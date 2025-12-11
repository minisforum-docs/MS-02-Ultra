# MS-02 Ultra

MS-02 Ultra 是一个从MS-01全面升级的MINI PC  
此Guide对 MS-02 Ultra做一个简单的介绍，并且附上有关MS-02 Ultra有关内存兼容性，玩法等重要信息。

<font color="#dd0000">另外购买内存时，请务必参考官方的[内存出厂清单](#内存官方出厂清单)和[QVL清单](#内存qvl清单)</font><br />





## 简单的产品介绍
### 从MS-01 到MS-02 Ultra的提升点
提升主要是以下几点
1. 升级的PCIE的拓展性。
    - 部分解决的显卡难以购买的问题，支持了双槽半高的显卡（Amazon，淘宝，JD都可以随便购买到）
    - 最多3xPCIE插槽。如果不需要显卡，灵活性更高，能够更加方便的拓展
2. 内存支持了ECC，并且最大内容翻倍到256GB
    - 仅285HX CPU支持ECC
    - 所有的机型都支持256GB
3. 电源直接内置，不用掉一坨电源了
4. CPU性能直接翻倍
    - 之前最高13900H(60W/80W)6大8小核，02 Ultra采用285HX最大8核16核(100W/140W)
    - 改善了CPU导热材料为相变材料，CPU风道采用了服务器级别贯穿风道
    - 就算是235HX（6大8小核）性能也比13900H好10-20%
5. 雷电接口从USB4 40Gbps 升级为 2x80Gbps TBT5(USB4 V2)和1xUSB4(40Gbps)
6. 当然，体积也提升了，从1.7L变成了4.8L

### 使用Tips

### 其他文档
 - [MS-02 Ultra内存兼容性文档](/Docs/Chinese/02-Ultra-Memory.md)
 - [MS-02 Ultra 已知问题以及解决方式](/Docs/Chinese/02-Ultra-KnowIssue.md)


### 独立显卡

- 插入带显示功能的独立显卡时，会默认自动关闭集成显卡。请使用独立显卡进行显示输出。但您可以在`Onboard Devices Setting` -> `Internal Graphics` 中强制启用此功能
- 独立显卡支持 `Gigabyte GeForce RTX™ 5060 OC Low Profile`和 `ASUS GeForce RTX™ 5060 LP`
- 每一个PCIe插槽都支持标准的PCIe 75W供电，所以适配`MS-01`的显卡也是支持的 
- 显卡内置电源适配器为 `350W`, 285HX默认TDP为`PL1/PL2:100W/140W` 当插入显卡后，因为显卡和CPU会互相烤，所以会自动降低TDP为`90/110W`
- 插入双槽半高显卡时，会遮挡住一个PCIex4插槽，导致此插槽无法使用

### CPU功率释放
本文档介绍出厂的默认CPU功率释放情况。PL1为长时间功率，PL2为短时间Turbo功率。插入显卡后当插入显卡后，因为显卡和CPU会互相烤，所以会降低TDP
- 当插入显卡后，因为显卡和CPU会互相烤，所以会自动降低TDP为`90/110W`
- 你可以在`Power & Performance`菜单中手动调整当前的TDP(插拔显卡后手动设置的数值会重置)
- MS-02 Ultra初始风扇和TDP设定是综合所有情况的最佳设定，若您需要调整为更高TDP使用，请务必参考[风扇转速调整](#风扇转速调整)同步调大风扇

|  CPU | 无显卡PL1/PL2 |插入显卡PL1/PL2 | 睿频时间 | 温度墙 |
|-----------|--------------|---|---|--------------|
| 285HX| 100W/140W |90W/110W| 32秒 | 90° |
| 275HX| 100W/140W |90W/110W| 32秒 | 90° |
| 235HX| 80W/100W |60W/100W| 32秒 | 90° |

### Idle功耗
MS-02 Ultra（285HX版本）附带一张非常强的25Gbps网卡。但此网卡芯片功耗也很高，而且待机功率和负载功率几乎一样。
此表格对比插入25G网卡后，和没插网卡的285HX的功耗。
(测试结果为 安装完Windows并装好所有驱动，没有连接互联网的idle情况)
|  CPU | G3 Status |Windows Idle With 25G NIC | Windows Idle NO 25G NIC | BIOS Menu With 25G NIC | BIOS Menu NO 25G NIC |
|-----------|--------------|---|---|--------------|--------------|
| 285HX| 1.55W |9.8-12-13W| 22W | 46.8W | 52.2W |



### 固态硬盘数量和速度
对于带 Minisforum专用E810拓展卡的情况下最大支持4个SSD，其中2个在主板上，2个在专用拓展卡上。  
目前此拓展卡仅标配在285HX的版本上，275HX和235HX仅有2个在主板上的SSD。  

为了兼容性E810专用拓展卡的槽位，默认被设置为PCIe3.0x4的速度。您可以在BIOS中手动进一步调整为PCIe4.0。调整后建议跑一次硬盘速度测试，若有任何异常请调整为PCIe3.0

BIOS中`Onboard Devices Setting`->`PCI-E Port`的SSD中修改 PCIe Speed

### 风扇转速调整
MS-02 Ultra使用EC控制器控制风扇转速。  
用户可在BIOS菜单中手动调整风扇的转速。  
`Advanced` -> `Hardware Monitor` -> `XXX Fan Setting` -> `User Mode`
启用后，会出现4个温度点和4个PWM值，PWM值最大为250，250时风扇的满转速。

### VPRO功能
因为 Intel的CPU限制，目前仅285HX的CPU支持VPRO功能。  
所以285HX的版本的2.5G 网卡为I226-LM，芯片组为WM880, 而275HX/235HX版本的2.5G网卡为I226-V芯片组为HM870。  
仅285HX的版本支持 AMT远程控制技术。  
对于支持VPRO的功能的可以直接进入`MEBx`菜单进行VPRO的相关设置。  
默认密码为 `admin`，第一次需要修改密码，至少为8位，带英文大小写和数字和特殊符号。  


