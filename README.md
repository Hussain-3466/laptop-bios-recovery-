# laptop-bios-recovery-
Hardware-level recovery of a laptop with corrupted BIOS firmware using an external SPI programmer.


# Laptop BIOS Recovery

A collaborative hardware-level BIOS recovery project involving the restoration of an **HP 15-bs133ne** laptop with corrupted firmware.

## Overview

An **HP 15-bs133ne** laptop became unbootable due to corrupted BIOS firmware.

After investigating the issue, we determined that the normal software-based recovery options were insufficient. Rather than replacing the motherboard, we performed a chip-level firmware recovery by directly accessing the BIOS SPI flash chip and programming it using an external **CH341B programmer**.

An important part of the recovery was preserving machine-specific firmware data from the original corrupted dump. We inspected the original `.bin` image and identified blocks containing system-specific information, including data associated with the laptop's product identification and serial information. Relevant data was preserved and incorporated into the recovery process rather than treating the original firmware image as completely disposable.

The laptop was successfully restored to a working, bootable state.

> **Note:** This documentation was written retrospectively after completing the recovery. No photographs or screenshots were captured during the original repair because the focus at the time was on diagnosing and resolving the issue.

## Objective

Recover the laptop from a corrupted BIOS state while preserving relevant machine-specific firmware information, without replacing the motherboard.

## Hardware & Software

| Component            | Details               |
| -------------------- | --------------------- |
| Laptop               | **HP 15-bs133ne**     |
| BIOS/SPI Flash Chip  | **25B64BSIG**         |
| Programmer           | **CH341B Programmer** |
| Programming Software | **NeoProgrammer**     |
| Firmware Image       | BIOS `.bin` image     |

## Recovery Process

### 1. Diagnosis

The laptop was unable to boot normally, leading us to investigate the BIOS/firmware as a potential source of the failure.

After determining that conventional BIOS recovery methods were insufficient, we proceeded with a hardware-level recovery.

### 2. Identifying the BIOS Flash Chip

The BIOS flash chip was located on the laptop's motherboard and identified by the marking:

`25B64BSIG`

The chip was accessed directly for firmware read/write operations.

### 3. Reading the Original Firmware

A **CH341B programmer** was used to interface with the BIOS flash chip.

Before modifying the chip, the existing firmware was read and saved as a `.bin` dump.

Keeping a copy of the original firmware was important because the image contained machine-specific information that could potentially be lost by simply writing a generic BIOS image.

### 4. Inspecting the Firmware Dump

The original BIOS dump was inspected to understand its contents and locate machine-specific data.

Among the information identified were blocks associated with the laptop's:

* Product identification
* Serial number
* Other system-specific firmware information

Relevant blocks were preserved for use during the recovery.

> **Privacy note:** Machine-specific identifiers and keys are intentionally not included in this repository.

### 5. BIOS Recovery

The appropriate BIOS firmware was prepared for programming while retaining the relevant system-specific information from the original dump.

The resulting firmware image was programmed to the SPI flash chip using:

**CH341B → NeoProgrammer → BIOS SPI Flash**

### 6. Verification & Testing

After programming, the firmware was verified and the laptop was reassembled and powered on.

The system successfully recovered from its corrupted BIOS state and returned to normal operation.

## Result

**Successful BIOS recovery.**

The HP 15-bs133ne was restored to a bootable and functional state without replacing the motherboard.

The recovery also demonstrated the importance of preserving the original firmware dump when performing chip-level BIOS recovery, as the dump may contain system-specific information that is not necessarily present in a generic BIOS image.

## Technical Concepts

This project involved hands-on work with:

* BIOS/UEFI firmware
* SPI flash memory
* `.bin` firmware images
* CH341B hardware programming
* NeoProgrammer
* Firmware inspection and modification
* Machine-specific firmware data preservation
* Chip-level firmware recovery
* Motherboard-level troubleshooting
* Firmware verification

## Collaboration

This was a collaborative hardware recovery project completed with a friend.

We worked together throughout the troubleshooting and recovery process, including diagnosing the failure, identifying the BIOS flash chip, inspecting the firmware dump, performing the chip-level recovery, and validating the system afterward.

## Lessons Learned

This project provided practical experience with:

* Diagnosing firmware-related hardware failures
* Understanding SPI flash memory and BIOS storage
* Working directly with motherboard-level components
* Reading and programming firmware using an external programmer
* Inspecting binary firmware images
* Preserving machine-specific firmware information during recovery
* Verifying firmware programming operations
* Troubleshooting below the operating-system level
* Collaborative hardware debugging

## Documentation

This repository documents the recovery process and technical approach used during the repair.

Original photographs and screenshots were not captured during the repair because the priority at the time was resolving the failure. Hardware photographs and additional documentation may be added later if the device and components are available.

---

**Project type:** Collaborative hardware/firmware recovery
**Device:** HP 15-bs133ne
**Focus:** BIOS/UEFI · SPI Flash · CH341B · Firmware Analysis · Hardware Troubleshooting

