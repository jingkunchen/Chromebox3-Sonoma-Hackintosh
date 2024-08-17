# Asus Chromebox 3 (i7-8550U) macOS Sonoma 14.6.1 EFI (OpenCore 1.0.1)

This repository contains the EFI files for running macOS Sonoma 14.6.1 on the Asus Chromebox 3 with an Intel i7-8550U CPU using OpenCore 1.0.1.

## Specifications

- **Model:** Asus Chromebox 3
- **CPU:** Intel Core i7-8550U
- **GPU:** Intel UHD 620
- **RAM:** 16GB DDR4 (user-upgraded)
- **Storage:** NVMe SSD (user-upgraded, or factory SATA SSD)
- **Audio:** Realtek ALC255
- **Wi-Fi:** Intel Dual Band Wireless-AC 7265 (with support using AirportItlwm)
- **Bootloader:** OpenCore 1.0.1
- **macOS Version:** Sonoma 14.6.1

## What's Working

- [x] Intel UHD 620 Graphics (with hardware acceleration)
- [x] Audio (internal speakers, microphone, headphone jack)
- [x] Wi-Fi & Bluetooth (with Intel 7265 using AirportItlwm)
- [x] USB Ports (Type-A and Type-C)
- [x] HDMI output
- [x] Sleep/Wake
- [x] Brightness Control
- [x] Ethernet
- [x] macOS Power Management (including CPU power states)

## Not Working / Issues

- [ ] AirDrop, Handoff, and Sidecar (Intel Wi-Fi lacks native macOS support for these features)
- [ ] SD Card Reader (if present, typically unsupported in macOS)
- [ ] Thunderbolt 3 (if present, hot-plug may not work)
- [ ] Occasional wake from sleep issues (depends on ACPI patch configuration)

## Coreboot (兔子 BIOS) Configuration

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

## Installation

1. **Prepare macOS USB Installer**: Create a macOS Sonoma 14.6.1 installer using [macOS Recovery](https://support.apple.com/en-us/HT201372) or from a working macOS environment.

2. **Copy EFI Folder**: After creating the USB installer, replace the EFI folder on the USB drive with the one from this repository.

3. **Boot the Installer**: Boot from the USB installer and follow the standard macOS installation steps.

4. **Post-Installation**:
    - Copy the EFI folder from the USB to your system's EFI partition after installing macOS.
    - Generate your own SMBIOS using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) and replace the `SerialNumber`, `BoardSerialNumber`, and `SmUUID` in `config.plist`.

## Setting Up Intel 7265 Wi-Fi and Bluetooth

1. Download the latest release of [AirportItlwm](https://github.com/OpenIntelWireless/itlwm).
2. Add `AirportItlwm.kext` to your EFI's `OC/Kexts` folder and update your `config.plist` to include the kext.
3. The native macOS Wi-Fi menu will now work with your Intel 7265, no need for HeliPort.

## Known Issues & Troubleshooting

- **Wake from Sleep Issues**: If the system does not wake from sleep properly, try adjusting the `Darkwake` settings in `config.plist`.
- **Intel Wi-Fi Configuration**: For Intel 7265, follow the instructions from the [OpenIntelWireless](https://github.com/OpenIntelWireless/itlwm) project to set up Wi-Fi and Bluetooth. Note that advanced features like AirDrop and Handoff are not supported.

## Credits

- [Acidanthera](https://github.com/acidanthera) for OpenCore and kexts
- [MrChromebox.tech](https://mrchromebox.tech) for Coreboot/UEFI firmware
- [Dortania](https://dortania.github.io/) for their comprehensive guides
- [OpenIntelWireless](https://github.com/OpenIntelWireless) for Intel Wi-Fi and Bluetooth support
- [Hackintosh Community](https://www.tonymacx86.com/) for testing and support
