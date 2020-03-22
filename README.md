# xilinx-yocto-workspace

## Prerequisites
- Docker

## Instructions

Steps to build firmware for **zedbord-zynq7**:
- `source ./setup-environment`
- `build-interractive` (host env)
- `build-zedbord-zynq7` (builder env)

NOTE: `build-help` to see all available build commands (supports host and builder)

## Project Structure
- **builder**: The docker-based builder files
- **scripts**: Contains all the host scripts that are executed at the host environment.

## Related Repositories
- https://github.com/Xilinx/yocto-manifests.git