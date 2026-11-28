# PinOS Build Guide

## Overview

This guide documents the process of building  PinOS from its source repository using Archiso.

PinOS is an experimental Arch Linux-based operating system currently in early development. The build process uses an Arch Linux environment to configure, generate and test the ISO image.

As developemnt progresses, build instructions and requirements may change.

## Requirements

### Build Environment

PinOS is currently built from an Arch Linux environment using Archiso.

The following are required:
- Arch Linux installation.
- `archiso`, to generate the PinOS ISO image.
- Git, to obtain the PinOS source repository.

### Testing Environment

QEMU is used to test the generated ISO without requiring physical installation media.

The following packages are used:

- `qemu-desktop`, which provides QEMU virtualisation.
- `edk2-ovmf`, to provide UEFI firmware for virtual machine testing.

### Architecture

The current PinOS build targets the `x86_64` architecture. Other architectures are not currently supported. 

## Repository Structure

.
├── archlive
│   ├── airootfs
│   ├── bootstrap_packages
│   ├── efiboot
│   ├── grub
│   ├── packages.aarch64
│   ├── packages.x86_64
│   ├── pacman.conf
│   ├── profiledef.sh
│   └── syslinux
├── branding
│   ├── concepts
│   ├── inkscape-svgs
│   ├── pngs
│   ├── README.md
│   └── svgs
├── CHANGELOG.md
├── docs
│   ├── BUILD-GUIDE.md
│   ├── DECISIONS.md
│   ├── ROADMAP.md
│   └── SCOPE.md
├── .gitignore
└── README.md


## Build Environment Setup

Before building PinOS, ensure that the host system is running Arch Linux and has the required build tools installed.

### 1. Update the system

Update the host system using Pacman:

```
sudo pacman -Syu
```

### 2. Install Archiso and Git

Install the required packages:

```
sudo pacman -S archiso git
```

- `archiso` provides the tools required to generate Arch Linux ISO images.
- `git` is used to clone and manage the PinOS source repository

### 3. Install Virtual Machine Testing Tools

QEMU is used to test the generated ISO without requiring physical installation media.

Install the required packages:

```
sudo pacman -S qemu-desktop edk2-ovmf
```

- `qemu-desktop` provides QEMU virtualisation.
- `edk2-ovmf` provides UEFI firmware for VM testing

## 4. Obtaining the Source

Clone the PinOS repository from GitHub using Git:

```
git clone https://github.com/AegisRaspin/PinOS.git
```

Navigate into the cloned repository:

```
cd PinOS
```

The repository contains the Archiso profile and everything needed to build PinOS, but ensure that the `archlive/` directory is present anyway. 

## Building the ISO


## Building the ISO

Once the repository has been cloned and the build environment is prepared, the PinOS ISO can be generated using `mkarchiso`.

From the root of the PinOS repository, run:

```
mkarchiso -v -w work -o out archlive
```

### Command Arguments

| Argument | Description |
|---|---|
| `-v` | Enables verbose output during the build process. |
| `-w work` | Specifies the working directory used during the build. |
| `-o out` | Specifies the directory where the generated ISO is stored. |
| `archlive` | Specifies the Archiso profile directory. |

### Build Output

During the build process, Archiso prepares the live filesystem, installs the selected packages, configures the image and generates the final ISO.

Once completed successfully, the ISO image will be available in the `out/` directory.

Build times vary depending on hardware, network speed and package availability.

### Rebuilding

When rebuilding PinOS, the existing working directory can be reused. For a fresh build, an empty working directory can be specified using the `-w` argument.

## Testing the ISO


## Testing the ISO

After a successful build, the generated PinOS ISO can be tested using QEMU.

Archiso provides the `run_archiso` utility, which simplifies launching Archiso images in a virtual machine.

From the root of the PinOS repository, run:

```bash
run_archiso -i out/*.iso
```

The `-i` argument specifies the ISO image to boot.

### UEFI Testing

`run_archiso` uses UEFI booting by default.

The `-u` argument can also be specified explicitly:

```
run_archiso -u -i out/*.iso
```

### BIOS Testing

To test BIOS boot compatibility, use:

```
run_archiso -b -i out/*.iso
```

BIOS boot support should only be considered verified after successfully testing the image.

### Testing the Live Environment

Once PinOS has booted, verify that the following components work as expected:

- XFCE desktop environment starts successfully.
- The `pinos` live user is available.
- Zsh is configured as the default shell.
- Sudo privileges work correctly.
- Networking and DNS resolution function.


## Troubleshooting

## Notes
