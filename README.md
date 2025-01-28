# RISCV_SIMULATOR
This repository is for ECE201
# RISC-V Development Environment Setup Guide

## Prerequisites

Before starting, ensure you have:
- A computer with administrative privileges
- Internet connection
- Terminal/Command Prompt access

## Docker Installation

### For Linux (Ubuntu/Debian):
1. Update package index:
   ```bash
   sudo apt-get update
   ```
2. Install Docker Engine:
   ```bash
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```
3. Verify installation:
   ```bash
   sudo docker --version
   ```

### For macOS:
1. Download Docker Desktop for Mac from [Docker's official Docs](https://docs.docker.com/desktop/setup/install/mac-install/)
2. Double-click the .dmg file
3. Drag Docker to your Applications folder
4. Start Docker from your Applications folder
5. Verify installation by opening Terminal and running:
   ```bash
   docker --version
   ```

### For Windows:
Please refer to [Docker's official Docs] https://docs.docker.com/desktop/setup/install/windows-install/

## Setting Up RISC-V Development Environment

### Pull the RISC-V Development Image
```bash
docker pull qhou3/riscv-micro
```

### Run the Container
```bash
docker run -it qhou3/riscv-micro
```

To mount a local directory (recommended for persistent work):
```bash
docker run -it -v /path/to/local/directory:/work qhou3/riscv-micro /bin/bash
```

## Basic Usage
### Compiling a RISC-V Program
1. Create a simple C program (example.c):
   ```c
   #include <stdio.h>
   
   int main() {
       printf("Hello RISC-V World!\n");
       return 0;
   }
   ```

2. Compile the program:
   ```bash
   riscv64-unknown-elf-gcc example.c -o example 
   ```

3. Run the program:
   ```bash
   spike pk example
   ```
   The output should be:
   ```
   Hello RISC-V World!
   ```
   
### Gather Instructions
1. Run the program with --log-commits and output to a log file:
   ```bash
   spike --log-commits pk example > log.txt 2>&1
   ```
2. Check the log.txt file for the instruction execution trace
   
## Troubleshooting

### Common Issues

1. **Docker permission denied**
   ```bash
   sudo usermod -aG docker $USER
   newgrp docker
   ```

2. **Container not starting**
   - Ensure Docker service is running:
   ```bash
   sudo systemctl start docker
   ```

3. **Image pull failed**
   - Check internet connection
   - Try with sudo if on Linux
   
## Acknowledgments

This Docker environment is built based on the following open-source projects:

* [RISC-V ISA Simulator](https://github.com/riscv-software-src/riscv-isa-sim) - The Spike RISC-V ISA Simulator
* [RISC-V GNU Compiler Toolchain](https://github.com/riscv-collab/riscv-gnu-toolchain) - RISC-V C and C++ cross-compiler
* [RISC-V Proxy Kernel](https://github.com/riscv-software-src/riscv-pk) - RISC-V Proxy Kernel and Boot Loader
