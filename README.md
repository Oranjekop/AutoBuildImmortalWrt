# AutoBuildImmortalWrt
Fork from https://github.com/wukongdaily/AutoBuildImmortalWrt

## 🤔 这是什么？
这是一个用于构建 ImmortalWrt 固件的工作流，支持自定义固件大小、可选预装 Docker、可选预置 PPPoE 拨号信息。

**主要特性**
- 支持自定义固件大小（默认 2GB）
- 支持预安装 Docker（可选）
- 支持预设 PPPoE 拨号信息（可选）
- 支持升级不修改网络配置
- 可通过 build.sh 自行调整插件

## 如何查询都有哪些插件？
https://mirrors.sjtug.sjtu.edu.cn/immortalwrt/releases/24.10.5/packages/x86_64/luci/

## 使用建议
**旁路由（单网口）**
- 单网口默认采用 DHCP 模式
- 请在上级路由器查看分配给 ImmortalWrt 的 IP，再访问后台
- 后台内按主路由网段自行设置旁路 IP

**正常路由（多网口）**
- 多网口下通常 WAN 口拨号或 DHCP，其他 LAN 口为内网 DHCP
- 可修改管理地址以避免网段冲突（工作流输入默认 `192.168.20.1`，例如改为 `192.168.80.1`）

## 该固件默认属性（必读）
- 单网口设备默认 DHCP 自动获取 IP
- 多网口设备默认 WAN 口 DHCP，LAN 口 IP 取工作流输入值（默认 `192.168.20.1`；未提供时回退为 `192.168.100.1`）
- 勾选 PPPoE 时，WAN 口模式为 PPPoE
- 建议拨号用户使用前重启一次光猫
- 上述行为可在 `99-custom.sh` 中配置与调整

## 工作流关键输入
- luci_version：选择 ImmortalWrt 版本
- rootfs_size：固件根分区大小（MB）
- custom_router_ip：多网口设备管理地址
- include_docker：是否编译 Docker 插件
- enable_pppoe / pppoe_account / pppoe_password：PPPoE 配置

## 平台说明
**x86-64**
- 工作流：build-x86-64-immortalwrt-24.10.x
- 固件输出：immortalwrt-x86-64-generic-squashfs-combined-efi.img.gz
- 配置文件：x86-64/imm.config
- 构建脚本：x86-64/build.sh

**GL-MT2500（Filogic）**
- 工作流：build-GL-MT2500-immortalwrt-24.10.x
- 硬件版本：airoha / maxlinear
- 固件输出：bin/targets/mediatek/filogic/*
- 构建脚本：mediatek-filogic/build24.sh
- 开机脚本：glinet/99-custom.sh

## 🌟鸣谢
### https://github.com/immortalwrt
### https://github.com/wukongdaily/AutoBuildImmortalWrt
