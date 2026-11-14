# Pixelbook Go Hackintosh EFI

## Project Overview

This project is an OpenCore EFI configuration for the **Google Pixelbook Go**, intended for booting and running macOS in a Hackintosh environment. The EFI is based on [Interstellar750/pixelbookgo_hackintosh](https://github.com/Interstellar750/pixelbookgo_hackintosh) and has been further developed.

## EFI Versions and macOS Compatibility

The EFI in this project is divided into two versions by macOS version:

| EFI Version | Applicable macOS Versions | Notes |
|---|---|---|
| `EFI-12-14` | macOS 12.0 up to before 14.4 (`< 14.4`) | Suitable for macOS 12, 13, and versions before 14.4 |
| `EFI14-26` | macOS 14.4 to 26.0 (`>= 14.4` and `<= 26.0`) | After installation, you must inject the OCLP-Mod patch yourself to enable Wi-Fi |

### Important Notes

- **macOS 26 is not recommended**: The Pixelbook Go has limited hardware performance, resulting in a poor experience.
- When using `EFI14-26`, you must inject the **OCLP-Mod** patch yourself after macOS installation to enable Wi-Fi:  
  <https://github.com/laobamac/OCLP-Mod/releases>
- **By default, no EFI version includes `AirportItlwm`**. Download the driver corresponding to your macOS version from the following address:  
  <https://github.com/OpenIntelWireless/itlwm/releases>  
  After downloading, place the corresponding kext into `EFI/OC/Kexts` and add the corresponding entry under `Kernel -> Add` in `config.plist`.
- The EFI has been sanitized for SMBIOS. Before use, you must complete the SMBIOS settings yourself in a config editor, set the model to `MacBookAir8,1`, and generate the three SMBIOS identifiers (System Serial Number, MLB, and System UUID). Do not use the EFI directly from the repository.
- The audio userspace driver must be installed manually after system installation by installing `AtlasAudio.pkg` and restarting the computer.

## Hardware Specifications

### Test Machine Hardware Specifications

This project has currently been tested only on the following configuration:

| Item | Test Machine Specifications |
|---|---|
| Model | Google Pixelbook Go |
| CPU | Intel Core i5-8200Y (Amber Lake Y, 2 cores 4 threads) |
| iGPU | Intel UHD Graphics 615 |
| Memory | 16GB LPDDR3 |
| Storage | 128GB eMMC |
| Display | 13.3-inch 1920×1080 LCD |

### Pixelbook Go Reference Specifications

| Item | Reference Specifications |
|---|---|
| Model | Google Pixelbook Go |
| CPU | Intel Core m3-8100Y / i5-8200Y / i7-8500Y (Amber Lake Y) |
| iGPU | Intel UHD Graphics 615 |
| Memory | 8GB / 16GB LPDDR3 |
| Storage | 64GB / 128GB / 256GB eMMC |
| Display | 13.3-inch LCD, 1920×1080 / 4K UHD with touchscreen |
| Wireless Card | Intel Wireless-AC 9560, 2×2 802.11ac |
| Bluetooth | Integrated into the Intel wireless card, Bluetooth 5.0 |
| Ports | 2× USB-C, 3.5mm headphone jack |
| Keyboard/Trackpad | Backlit keyboard, trackpad |
| Audio | Built-in speakers, microphone, 3.5mm headphone jack |
| Camera | Front camera |

## Working Status

| Function | Status | Notes |
|---|---|---|
| CPU Power Management / Turbo Boost | ✅ |  |
| Intel UHD 615 iGPU Acceleration | ⚠️ | Some Electron / Chromium apps may have rendering errors (suspected to be due to lack of hardware support on the macOS platform) |
| Internal Display | ✅ |  |
| Brightness Adjustment | ✅ |  |
| Audio (Speaker/Headphone/Microphone) | ⚠️ | Partial driver support |
| eMMC | ⚠️ | AppleSDHC |
| Keyboard | ✅ |  |
| Trackpad | ✅ |  |
| Battery Status | ✅ |  |
| Charging | ✅ |  |
| USB-C Data | ✅ |  |
| USB-C Video Output | ✅ |  |
| Wi-Fi | ✅ | By default, no EFI version includes `AirportItlwm`. Download the corresponding version yourself and place it in `EFI/OC/Kexts`; `EFI14-26` also requires injecting the OCLP-Mod patch after installation |
| Bluetooth | ✅ |  |
| Sleep/Wake | ✅ |  |
| Touchscreen | ✅ |  |
| Camera | ❌ | No hardware driver |
| AirDrop / Handoff / Universal Clipboard | ❌ | Not supported by the driver |
| Google Titan C | ❌ | Unavailable |

## Notes on eMMC and Audio

- eMMC support is based on <https://github.com/acidanthera/EmeraldSDHC> with further development. The HS400 transfer rate is fully supported, but driver development is still in an early stage and may have other unknown bugs <https://github.com/FangHaoLin-daxia/AppleSDHC>.
- The speaker and microphone are driven through independent development (AtlasAudio), but they are still in an early stage. Known bug: when playing audio / video / system sounds, there is a small chance of audio distortion and noise.
- Development of the 3.5mm headphone driver is in progress <https://github.com/FangHaoLin-daxia/atlasaudio>.
- AtlasAudio does not currently support macOS 12 or earlier.

## Disclaimer

> This project is for learning, research, and technical exchange only. Do not use it for commercial purposes. Any data loss, hardware damage, or legal risk caused by using this project shall be borne by the user. Flashing firmware and modifying the EFI involve risks; be sure to back up in advance.

## License

This project is licensed under the **Apache License 2.0 (Apache-2.0)**.
