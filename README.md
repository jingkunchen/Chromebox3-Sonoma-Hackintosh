# Asus Chromebox 3 (i7-8550U) macOS Sonoma 14.6 EFI (OpenCore 1.0.1)

[English Version](#english-version) | [中文版](#中文版)

## English Version

This repository contains the EFI files for running macOS Sonoma 14.6.1 on the Asus Chromebox 3 with an Intel i7-8550U CPU using OpenCore 1.0.1.

### Specifications

- **Model:** Asus Chromebox 3
- **CPU:** Intel Core i7-8550U
- **GPU:** Intel UHD 620
- **RAM:** 16GB DDR4 (user-upgraded)
- **Storage:** NVMe SSD (user-upgraded, or factory SATA SSD)
- **Audio:** Realtek ALC255
- **Wi-Fi:** Intel Dual Band Wireless-AC 7265 (with support using AirportItlwm)
- **Bootloader:** OpenCore 1.0.1
- **macOS Version:** Sonoma 14.6.1

### What's Working

- [x] Intel UHD 620 Graphics (with hardware acceleration)
- [x] Audio (internal speakers, microphone, headphone jack)
- [x] Wi-Fi & Bluetooth (with Intel 7265 using AirportItlwm)
- [x] USB Ports (Type-A and Type-C)
- [x] HDMI output
- [x] Sleep/Wake
- [x] Brightness Control
- [x] Ethernet
- [x] macOS Power Management (including CPU power states)

### Not Working / Issues

- [ ] AirDrop, Handoff, and Sidecar (Intel Wi-Fi lacks native macOS support for these features)
- [ ] SD Card Reader (if present, typically unsupported in macOS)
- [ ] Thunderbolt 3 (if present, hot-plug may not work)
- [ ] Occasional wake from sleep issues (depends on ACPI patch configuration)

### Coreboot (兔子 BIOS) Configuration

To run macOS smoothly on the Asus Chromebox 3, it is recommended to replace the stock firmware with Coreboot (commonly known as "兔子 BIOS"). Here's a brief overview of the process:

1. **Install and Configure MrChromebox Coreboot**:
    - Follow the instructions on [MrChromebox.tech](https://mrchromebox.tech) to flash Coreboot firmware.
    - Ensure the firmware is configured to allow UEFI boot mode.

2. **Bootloader Setup**:
    - Use OpenCore as the bootloader. The EFI folder provided in this repository is already configured for optimal compatibility with macOS Sonoma.

3. **Disable Write Protection**:
    - Before flashing, you may need to disable write protection by removing the WP screw on the motherboard.

4. **Update Firmware**:
    - Use the MrChromebox script to install the UEFI firmware. This will replace the factory BIOS with Coreboot.

### Installation

1. **Prepare macOS USB Installer**: Create a macOS Sonoma 14.6.1 installer using [macOS Recovery](https://support.apple.com/en-us/HT201372) or from a working macOS environment.

2. **Copy EFI Folder**: After creating the USB installer, replace the EFI folder on the USB drive with the one from this repository.

3. **Boot the Installer**: Boot from the USB installer and follow the standard macOS installation steps.

4. **Post-Installation**:
    - Copy the EFI folder from the USB to your system's EFI partition after installing macOS.
    - Generate your own SMBIOS using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) and replace the `SerialNumber`, `BoardSerialNumber`, and `SmUUID` in `config.plist`.

### Setting Up Intel 7265 Wi-Fi and Bluetooth

1. Download the latest release of [AirportItlwm](https://github.com/OpenIntelWireless/itlwm).
2. Add `AirportItlwm.kext` to your EFI's `OC/Kexts` folder and update your `config.plist` to include the kext.
3. The native macOS Wi-Fi menu will now work with your Intel 7265, no need for HeliPort.

### Known Issues & Troubleshooting

- **Wake from Sleep Issues**: If the system does not wake from sleep properly, try adjusting the `Darkwake` settings in `config.plist`.
- **Intel Wi-Fi Configuration**: For Intel 7265, follow the instructions from the [OpenIntelWireless](https://github.com/OpenIntelWireless/itlwm) project to set up Wi-Fi and Bluetooth. Note that advanced features like AirDrop and Handoff are not supported.

### Credits

- [Acidanthera](https://github.com/acidanthera) for OpenCore and kexts
- [MrChromebox.tech](https://mrchromebox.tech) for Coreboot/UEFI firmware
- [Dortania](https://dortania.github.io/) for their comprehensive guides
- [OpenIntelWireless](https://github.com/OpenIntelWireless) for Intel Wi-Fi and Bluetooth support
- [Hackintosh Community](https://www.tonymacx86.com/) for testing and support
- Special thanks to [国光](https://github.com/sqlsec/Asus-ChromeBox-i7-8550U) for the inspiration and guidance.

---

## 中文版

本仓库包含用于在 Asus Chromebox 3 (搭载 Intel i7-8550U CPU) 上运行 macOS Sonoma 14.6.1 的 EFI 文件，使用 OpenCore 1.0.1 引导。

### 规格

- **型号**: Asus Chromebox 3
- **处理器**: Intel Core i7-8550U
- **显卡**: Intel UHD 620
- **内存**: 16GB DDR4 (用户自行升级)
- **存储**: NVMe SSD (用户自行升级，或者原厂 SATA SSD)
- **音频**: Realtek ALC255
- **无线网络**: Intel Dual Band Wireless-AC 7265 (通过 AirportItlwm 支持)
- **引导器**: OpenCore 1.0.1
- **macOS 版本**: Sonoma 14.6.1

### 已实现功能

- [x] Intel UHD 620 显卡 (支持硬件加速)
- [x] 音频 (内置扬声器、麦克风、耳机接口)
- [x] Wi-Fi 和蓝牙 (使用 Intel 7265 和 AirportItlwm)
- [x] USB 接口 (Type-A 和 Type-C)
- [x] HDMI 输出
- [x] 睡眠/唤醒
- [x] 亮度控制
- [x] 以太网
- [x] macOS 电源管理 (包括 CPU 电源状态)

### 不工作/存在问题

- [ ] AirDrop、Handoff 和 Sidecar (由于 Intel 无线网卡缺乏 macOS 原生支持)
- [ ] SD 卡读卡器 (如果存在，macOS 通常不支持)
- [ ] Thunderbolt 3 (如存在，热插拔可能无法正常工作)
- [ ] 偶尔的睡眠唤醒问题 (取决于 ACPI 补丁配置)

### Coreboot (兔子 BIOS) 配置

要在 Asus Chromebox 3 上顺畅运行 macOS，建议将原厂固件替换为 Coreboot (通常称为 “兔子 BIOS”)。以下是简要步骤：

1. **安装和配置 MrChromebox Coreboot**：
    - 按照 [MrChromebox.tech](https://mrchromebox.tech) 上的说明刷写 Coreboot 固件。
    - 确保固件已配置为允许 UEFI 启动模式。

2. **引导器设置**：
    - 使用 OpenCore 作为引导器。本仓库提供的 EFI 文件夹已经为 macOS Sonoma 做了最佳兼容性配置。

3. **禁用写保护**：
    - 在刷写之前，可能需要通过移除主板上的 WP 螺丝来禁用写保护。

4. **更新固件**：
    - 使用 MrChromebox 的脚本安装 UEFI 固件，这将用 Coreboot 替换工厂 BIOS。

### 安装步骤

1. **准备 macOS USB 安装盘**：使用 [macOS 恢复](https://support.apple.com/zh-cn/HT201372) 或一个正常工作的 macOS 环境创建 macOS Sonoma 14.6.1 安装盘。

2. **复制 EFI 文件夹**：创建 USB 安装盘后，将该仓库中的 EFI 文件夹替换到 USB 安装盘的 EFI 分区。

3. **启动安装程序**：从 USB 启动安装程序，按照标准的 macOS 安装步骤进行操作。

4. **安装后处理**：
    - 在安装 macOS 后，将 USB 中的 EFI 文件夹复制到系统的 EFI 分区。
    - 使用 [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) 生成你自己的 SMBIOS，并在 `config.plist` 中替换 `SerialNumber`、`BoardSerialNumber` 和 `SmUUID`。

### 设置 Intel 7265 Wi-Fi 和蓝牙

1. 下载最新版本的 [AirportItlwm](https://github.com/OpenIntelWireless/itlwm)。
2. 将 `AirportItlwm.kext` 添加到 EFI 的 `OC/Kexts` 文件夹中，并更新 `config.plist` 以包含该 kext。
3. 现在 macOS 原生的 Wi-Fi 菜单将支持 Intel 7265，不再需要使用 HeliPort。

### 已知问题和故障排除

- **睡眠唤醒问题**：如果系统无法正常从睡眠中唤醒，可以尝试调整 `config.plist` 中的 Darkwake 设置。
- **Intel 无线网卡配置**：对于 Intel 7265，请按照 [OpenIntelWireless](https://github.com/OpenIntelWireless/itlwm) 项目的指南设置 Wi-Fi 和蓝牙。需要注意的是，像 AirDrop 和 Handoff 这样的高级功能不受支持。

### 鸣谢

- [Acidanthera](https://github.com/acidanthera) 提供的 OpenCore 和 kexts
- [MrChromebox.tech](https://mrchromebox.tech) 提供的 Coreboot/UEFI 固件
- [Dortania](https://dortania.github.io/) 提供的详尽指南
- [OpenIntelWireless](https://github.com/OpenIntelWireless) 团队提供的 Intel Wi-Fi 和蓝牙支持
- [Hackintosh Community](https://www.tonymacx86.com/) 的测试和支持
- 特别感谢 [国光](https://github.com/sqlsec/Asus-ChromeBox-i7-8550U) 的灵感和指导。

---

