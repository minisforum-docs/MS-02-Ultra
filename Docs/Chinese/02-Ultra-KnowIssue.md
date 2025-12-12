# MS-02 Ultra 已知问题以及解决方式

此页面记录MS-02 Ultra 已上市的型号的所有已知问题，和对应的解决方案


## 目录

- [PCIe SMBus导致无法开机](#pcie-smbus导致无法开机)
- [RTL8127 驱动问题关机后导致无法再次开机](#rtl8127-驱动问题关机后导致无法再次开机)

## PCIe SMBus导致无法开机

### 问题总结

如果遇到PCIe设备插入无法开机，可以直接试试屏蔽PCIe SMBus总线。

### 详细原因 
因为PCH的SMBus只有一路。为了实现完整的 PCIe Function，MS-02 Ultra内存的SMBus和PCIe的SMBUS共用一路走线。  
内存的SMBus负责高速CPU支持的内存频率等信息，非常重要。  
1. 某些PCIe设备的SMBus实现不标准或者直接拉低，会直接导致内存SMBus通信异常。进而直接导致无法开机。
2. 某些PCIe设备（傲腾PCIe固态硬盘）虽然SMBus实现很标准，但是协商过程中会被识别为内存设备，并且影响SODIMM的内存频率协商，也会导致无法开机/内存无法识别的问题。

### 解决方案

PCIe的前11个PIN为(不用担心A面/B面)   
中使用胶带直接双面 屏蔽 5-9 PIN。（至少保证5，6两个PIN被屏蔽掉了）


|  Pin | B面 | A | 描述|
|-|-|-|-|
|1|+12V|PRSNT1#|连接到PRSNT2#Pin|
|2|+12V|+12V|主供电|
|3|+12V|+12V|主供电|
|4|GND|GND||
|5|SMCLK|TCK|SMBUS and JTAG PORT|
|6|SMDAT|TDI|SMBUS and JTAG PORT|
|7|Ground|TDO|SMBUS and JTAG PORT|
|8|+3.3V|TMS|SMBUS and JTAG PORT|
|9|TRST#|+3.3V|SMBUS and JTAG PORT|
|10|+3.3V AUX|+3.3V|Aux power & standby power|
|11|WAKE#|PERST|Link reactivation; fundamental reset[26]|


## RTL8127 驱动问题关机后导致无法再次开机

### 问题总结
Linux 某个内核自带的RTL8127驱动关机时会把RTL8127状态异常，进而导致无法再次开机、
### 问题原因
Linux 某个内核版本内的自带的r8169驱动，在关机时，会把RTL8127网卡置为一种异常状态。  
此异常状态会让RTL8127不输出Power_En信号，进而影响到开机过程。
### 解决方案

临时解决方案(可通过此方法快速定位是否为此问题): BIOS中`On Board Setting`关闭RTL8127网卡设备  

#### 解决方案1(推荐): 安装RTL8127 DKMS驱动

PVE系统
(需要先替换掉 Proxmox VE No-Subscription Repository)
```bash
tee /etc/apt/sources.list.d/pve-enterprise.sources > /dev/null << 'EOF'
Types: deb
URIs: http://download.proxmox.com/debian/pve
Suites: trixie
Components: pve-no-subscription
Signed-By: /usr/share/keyrings/proxmox-archive-keyring.gpg
EOF
```
下载并上传 此 dkms驱动包: https://github.com/minisforum-repo/r8127-dkms/releases/download/11.015.00-1/r8127-dkms_11.015.00-1_all.deb
``` bash
# 确认已安装Proxmox VE No-Subscription Repository
# 安装dkms和当前内核对应的kernel headers
apt update
apt install dkms pve-headers-$(uname -r)

# 安装dkms包
dpkg -i r8127-dkms_11.015.00-1_all.deb
# 安装完成后 重启系统测试一下
```
Ubuntu/Debian系统
``` bash
# 安装dkms和当前内核对应的kernel headers
apt update
apt install dkms linux-headers-$(uname -r)

# 安装dkms包
dpkg -i r8127-dkms_11.015.00-1_all.deb
# 安装完成后 重启系统测试一下
```

#### 解决方案2: 直接从RTL官方下载最新的驱动
访问网站: https://www.realtek.com/Download/List?cate_id=584
下载 `10G Ethernet LINUX driver r8127 for kernel up to 6.15` 并上传MS-02 Ultra然后解压

PVE系统
(需要先替换掉 Proxmox VE No-Subscription Repository)
```bash
tee /etc/apt/sources.list.d/pve-enterprise.sources > /dev/null << 'EOF'
Types: deb
URIs: http://download.proxmox.com/debian/pve
Suites: trixie
Components: pve-no-subscription
Signed-By: /usr/share/keyrings/proxmox-archive-keyring.gpg
EOF
```

```

apt update

# PVE系统 确认已安装Proxmox VE No-Subscription Repository
# PVE系统安装 PVE的Kernel Header和相关软件
apt install gcc make pve-headers-$(uname -r)


# Ubuntu/Debian安装 Kernel Header和相关软件
apt install gcc make  linux-headers-$(uname -r)


# cd进入目的 自动安装
cd r8127-11.015.00
./autorun.sh
```


