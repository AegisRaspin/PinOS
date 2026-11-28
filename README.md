
# PinOS

**PinOS** is an experimental, Arch Linux-based operating system built using [Archiso](https://gitlab.archlinux.org/archlinux/archiso).

The project aims to explore Linux distribution development, system configuration, and the process of building and customising a Linux-based operating system.

PinOS is currently in early development, with its first prototype targeting a functional, lightweight desktop environment.

## Features

The current prototype includes:

- **Arch Linux base** – Built using Archiso and official Arch Linux repositories.
- **XFCE** – A desktop environment providing a graphical user interface.
- **LightDM** – Display manager for graphical login sessions.
- **Zsh** – Default shell for the live user.
- **Sudo** – Administrative privileges through the `wheel` group.
- **Networking** – Network connectivity and DNS resolution.
- **British English** – Configured `en_GB` locale.

## System Information

| Property | Details |
|---|---|
| Base distribution | Arch Linux |
| Build system | Archiso |
| Architecture | x86_64 |
| Desktop environment | XFCE |
| Display manager | LightDM |
| Default shell | Zsh |
| Locale | en_GB |
| Release | 0.1.0 (prototype) |

## Building

PinOS is built using Archiso on an Arch Linux host.

### Requirements

- Arch Linux build environment
- `archiso`
- `qemu-desktop` (for virtual machine testing)
- `edk2-ovmf` (for UEFI virtual machine testing)

### Build instructions

Clone the repository and enter the project directory:

```
git clone https://github.com/AegisRaspin/PinOS.git
cd PinOS
```

Build the ISO using:

```
mkarchiso -v -w work -o out archlive
```

The generated ISO image will be placed in the `out/` directory.

### Testing

To test the generated ISO using QEMU:

```
run_archiso -i out/*.iso
```

For additional build and testing information, see the project documentation.

## Limitations

PinOS is an experimental live environment. The current prototype does not include:

- An automated graphical or command-line installer.
- Persistent storage between live sessions.
- Individual user-account creation.
- ARM architecture support.
- Secure Boot support.

These limitations reflect the scope of the current prototype and may change in future releases.

## Documentation

Additional project documentation is maintained in the `docs/` directory.

This includes:

- Build guide
- Project decisions
- Development roadmap
- Scope

## Development

PinOS is a personal development project focused on understanding Linux system architecture and distribution development.

Future development may explore installation, user management, system customisation, and additional hardware architectures.

## Acknowledgements

PinOS is built upon the work of the Arch Linux project and its contributors.

- [Arch Linux](https://archlinux.org/)
- [Archiso – GitLab](https://gitlab.archlinux.org/archlinux/archiso)
- [Archiso – GitHub mirror](https://github.com/archlinux/archiso)
- [ArchWiki](https://wiki.archlinux.org/)

