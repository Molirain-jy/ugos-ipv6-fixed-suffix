# UGOS / Debian IPv6 Fixed Suffix Tool

这是一个适用于 **UGOS Pro (绿联 NAS)** 系统的 IPv6 配置工具。
家宽中无法固定ipv6前缀，只能采用反向匹配放行防火墙，固定后64位似乎不太安全，此脚本固定后4位，可以将所有需要被放行的服务器设为同样的后缀。

## 它解决了什么问题？

1.  **系统更新后配置丢失**：NAS 系统更新会重置 `/etc` 和 `/usr`，导致手动配置的 IPv6 失效。此脚本可作为“一键恢复补丁”使用。
2.  **Docker 导致 IPv6 丢失**：当 Docker 启用时，系统可能会禁用 RA 接收。工具会自动强制开启 `accept_ra=2` 修复此问题。
3.  **动态前缀 + 固定后缀**：实现 `前缀(ISP动态) + 随机(隐私) + 后缀(固定)`。
    * 例如：`240e:xxxx:xxxx:xxxx:随机:随机:随机:1f67`
    * 既保护了隐私（中间段随机），又方便防火墙根据后缀（如 `::1f67`）放行端口。

## 快速使用

### 方法一：一键安装/恢复 (推荐)

直接运行：

```bash
    curl -fsSL https://raw.githubusercontent.com/Molirain-jy/ugos-ipv6-tool/main/install.sh | sudo bash
```

### 方法二

```bash
    vi install.sh
```

```bash
   chmod +x install.sh
   sudo ./install.sh
```
