# 64-bit OS Kernel

A minimal 64-bit operating system kernel built from scratch, designed for learning and experimentation. This project demonstrates fundamental OS concepts including boot loading, memory management, and kernel initialization.

##  Features

- **Pure 64-bit Architecture**: Built specifically for x86_64 systems
- **Bootable ISO**: Creates a complete bootable image
- **Containerized Build**: Consistent development environment using Docker
- **Cross-platform Development**: Works on Linux, macOS, and Windows
- **Educational Focus**: Clean, documented code for learning OS development

##  Quick Start

For experienced users, run these commands in sequence:

```bash
# Build and run the OS
docker build buildenv -t myos-buildenv
docker run --rm -it -v "$(pwd)":/root/env myos-buildenv make build-x86_64 && exit
qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso
```

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Docker** - [Download here](https://www.docker.com/get-started)
- **QEMU** - Must be installed and added to your system PATH
  - Linux: `sudo apt install qemu-system-x86` (Ubuntu/Debian) or equivalent
  - macOS: `brew install qemu`
  - Windows: Download from [QEMU website](https://www.qemu.org/download/)
- **Terminal/Command Line Interface**

## 🔧 Build Instructions

### Step 1: Build the Docker Environment

```bash
docker build buildenv -t myos-buildenv
```

This creates a containerized build environment with all necessary tools and dependencies.

### Step 2: Enter the Build Environment

Choose the command for your operating system:

**Linux / macOS / WSL / Git Bash:**
```bash
docker run --rm -it -v "$(pwd)":/root/env myos-buildenv
```

**Windows Command Prompt:**
```cmd
docker run --rm -it -v "%cd%":/root/env myos-buildenv
```

**Windows PowerShell:**
```powershell
docker run --rm -it -v "${pwd}:/root/env" myos-buildenv
```

### Step 3: Build the Kernel

Inside the Docker container, run:

```bash
make build-x86_64
```

This compiles the kernel and creates a bootable ISO image at `dist/x86_64/kernel.iso`.

### Step 4: Exit the Container

```bash
exit
```

### Step 5: Run the OS

**Important**: Run QEMU on your host system, not inside Docker.

```bash
qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso
```

Your custom OS should boot in a QEMU window!

##  Cleanup

To remove the Docker build image when you're done:

```bash
docker rmi myos-buildenv -f
```

### Customization

- Modify kernel code in the `src/` directory
- Rebuild with `make build-x86_64` inside Docker
- Test changes by running the new ISO in QEMU

##  Troubleshooting

**QEMU not found**: Ensure QEMU is installed and added to your system PATH.

**Docker permission errors**: On Linux, you may need to run Docker commands with `sudo` or add your user to the docker group.

**Build failures**: Make sure you're running the build command inside the Docker container, not on your host system.

