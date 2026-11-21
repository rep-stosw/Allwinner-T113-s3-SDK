# Allwinner-T113-s3-SDK
Ultra-fast bare-metal SDK in C/C++ &amp; Assembly for Allwinner T113-s3 (sun8iw20p1 / Dual-Core Cortex-A7 + HiFi4 DSP). Sub-second boot, SMP dual-core, CedarX H.264/JPEG, G2D, TVD/CSI capture, Ethernet EMAC, USB Host/Device, Secure Boot, and Xtensa DSP SDK.

# Allwinner T113-s3 & HiFi4 DSP BareMetal SDK

![Architecture](https://img.shields.io/badge/Architecture-Dual--Core_Cortex--A7_%2B_HiFi4_DSP-blue)
![SoC](https://img.shields.io/badge/SoC-Allwinner_T113--s3_(sun8iw20)-orange)
![Language](https://img.shields.io/badge/Language-C_%2F_C%2B%2B_%2F_Assembly-brightgreen)
![Boot Time](https://img.shields.io/badge/Boot_Time-Sub--Second-red)

**Ultra-fast, high-performance bare-metal framework written from scratch in C, C++, and Assembly for the Allwinner T113-s3 SoC (`sun8iw20p1`) and its integrated Cadence Tensilica HiFi4 DSP co-processor.**

Designed for mission-critical embedded systems requiring sub-second boot times, zero OS overhead, full Dual-Core SMP execution (`CPU0` + `CPU1`), and direct hardware register control. The package includes two complete, tightly integrated bare-metal SDKs: one for the **Dual-Core ARM Cortex-A7** main processor and a dedicated SDK for the **HiFi4 DSP** core, along with build instructions and toolchain setup guides.

## Real Hardware Demonstration

### 1. Hardware Demo 1 (Display Engine)

https://github.com/user-attachments/assets/7e5ade3d-d5de-422d-a595-e8a08dbe8aaf

### 2. Hardware Demo 2 (G2D)

https://github.com/user-attachments/assets/9db50a86-7444-453a-8564-3dd9da2c463c

### 3. Hardware Demo 3 (H264 Decoder)

https://github.com/user-attachments/assets/80038388-ad1b-48b2-b38a-6922e126490c

### 4. Hardware Demo 4 (Analog Camera CVBS)

https://github.com/user-attachments/assets/69b30288-c9e3-4708-9033-25cc6e240b87

---

## Part 1: ARM Cortex-A7 Dual-Core BareMetal SDK

The main processor SDK provides low-level drivers, hardware acceleration pipelines, and communication stacks without any RTOS or Linux overhead:

| Category | Module / Feature | Technical Capabilities |
| :--- | :--- | :--- |
| **Core & SMP** | `Core / Clocks / DDR3` | Low-level CPU initialization, stack setup, PLL/clock tree, and embedded 128 MB DDR3 calibration |
| **Core & SMP** | `Dual-Core SMP (CPU0 + CPU1)` | Secondary ARM core (`CPU1`) startup, synchronization, and parallel dual-core execution |
| **Core & SMP** | `Interrupts / Timers / DMA` | GIC interrupt controller, high-precision hardware timers, and multi-channel DMA engine |
| **Security** | `Secure Boot` | Hardware-rooted secure boot chain implementation |
| **Video Codecs** | `CedarX H.264 & MPEG2` | Hardware-accelerated video decoding via Video Engine (VE) |
| **Video Codecs** | `CedarX JPEG Codec & PNG` | Hardware JPEG encoding/decoding (VE) + fast PNG software/accelerated decoder |
| **Display & Video In** | `LCD & TV Out (TCON_TV / TVE)` | Direct Display Engine control for RGB/LVDS LCDs and composite analog TV output |
| **Display & Video In** | `Analog TVD & CSI Camera` | Analog video capture (TV IN / TVD), parallel CSI camera capture, and hardware De-Interlacer (`DI`) |
| **2D Graphics** | `G2D Hardware Accelerator` | Hardware 2D blitting, scaling, rotation, alpha blending, and color space conversion |
| **Audio** | `Audio Codec & I2S` | Low-latency digital audio playback and recording via internal SoC DAC/ADC and external `I2S` |
| **USB Stack** | `USB Host & Mass Storage` | USB 2.0 Host block read/write with `FatFS`, plus USB Device Mass Storage (virtual drive) |
| **USB Stack** | `TinyUSB HID` | Full USB keyboard and mouse support via TinyUSB integration |
| **Storage & Network** | `SD/MMC + FatFS & EMAC` | High-speed SD card interface with `FatFS` and Ethernet `EMAC` driver (with external PHY) |
| **RF & Peripherals** | `RF4463-PRO & CMT2300A` | Drivers for Si4463 transceiver and CMT2300A wireless receiver (live H.264 video + audio streaming) |
| **RF & Peripherals** | `GPIO / UART / LEDC` | Direct GPIO manipulation, high-speed UART debugging, and addressable LED strip controller (`LEDC`) |

---

## Part 2: Cadence Tensilica HiFi4 DSP BareMetal SDK

A dedicated bare-metal SDK for the integrated **HiFi4 DSP** co-processor, built with **Xtensa GCC v13**:

* **DSP Core & Environment:** Full DSP core initialization, interrupt vector setup, instruction/data cache configuration, and C/C++ runtime environment.
* **ARM-to-DSP Firmware Loader:** Host-side driver running on the Cortex-A7 (`T113-s3`) to load, boot, and control HiFi4 DSP firmware binaries.
* **DSP Hardware Peripherals:** Direct support for DSP timers, external interrupt controller, hardware **MessageBox** (inter-processor communication with ARM), internal Audio Codec, DMA, and GPIO.
* **OPL3 (AdLib) Hardware-Accurate Emulation:** Integrated support for FM synthesis players based on [Nuked-OPL3](https://github.com/nukeykt/Nuked-OPL3) and [a2t_play](https://github.com/dmitrysmagin/a2t_play).
* **Multi-Format Chiptune / Retro Console Audio Engine:** Integrated [Game Music Emu (GME)](https://github.com/mmontag/game-music-emu) supporting real-time DSP playback of classic console formats:
  * **`AY`** — ZX Spectrum / Amstrad CPC
  * **`GBS`** — Nintendo Game Boy
  * **`GYM`** — Sega Genesis / Mega Drive
  * **`HES`** — NEC TurboGrafx-16 / PC Engine
  * **`KSS`** — MSX Home Computer / Z80 systems
  * **`NSF / NSFE`** — Nintendo NES / Famicom (including VRC6, Namco 106, and FME-7 expansion audio)
  * **`SAP`** — Atari 8-bit systems (POKEY sound chip)
  * **`SPC`** — Super Nintendo / Super Famicom (SNES)
  * **`VGM / VGZ`** — Sega Master System / Mark III, Sega Genesis / Mega Drive, BBC Micro

### Toolchains & Build Setup
The SDK documentation includes a quick-start guide detailing where to obtain the exact toolchains (**ARM GCC** for Cortex-A7 and **Xtensa GCC v13** for HiFi4 DSP) and step-by-step instructions for compiling both firmware targets.

---

## Need the SDK?
If you require the complete production-ready source code, custom linker scripts, startup codes, and build instructions, please contact the lead architect directly:

> ### **Email: repstosw2018@gmail.com**

*Direct engineer-to-engineer source transfer.*
