# MS-02 Ultra

MS-02 Ultra 是一个从MS-01全面升级的MINI PC  
此Guide对 MS-02 Ultra做一个简单的介绍，并且附上有关MS-02 Ultra有关内存兼容性，玩法等重要信息。


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


## Contributing

- Fork the repo, create a branch, and open a PR.
- Keep changes focused (fix, add an example, or translate).
- Use clear headings and short sections; prefer code blocks for commands.
- For doc fixes, reference the file path in your PR description.

## Support & Issues

Open an issue for bugs, missing steps, or platform-specific problems. Include:

- OS / firmware version
- The exact command and output (copy/paste)
- Which guide you followed

## License

MIT License


