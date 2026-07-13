# SDS-STM32N6
This repository contains SDS example projects for STMicroelectronics STM32N6.

## Quick Start

1. Install [Keil Studio](https://marketplace.visualstudio.com/items?itemName=Arm.keil-studio-pack) and [Arm SDS](https://marketplace.visualstudio.com/items?itemName=Arm.cmsis-sds) from the
   VS Code marketplace.
2. Clone this Git repository into a VS Code workspace.
3. Open the [CMSIS View](https://mdk-packs.github.io/vscode-cmsis-solution-docs/userinterface.html#2-main-area-of-the-cmsis-view)
   in VS Code and use the ... menu to choose an example via *Select Active Solution from workspace*.
    - First choose the *FSBL_LRUN* example to build and flash the FSBL for STM32N6570-DK board (see [STM32N6570-DK Board Setup](#stm32n6570-dk-board-setup)).
    - Then choose an SDS example.
4. The related tools and software packs are downloaded and installed. Review progress with *View - Output - CMSIS Solution*.
5. In the CMSIS view, use the
   [Action buttons](https://github.com/ARM-software/vscode-cmsis-csolution?tab=readme-ov-file#action-buttons) to build,
   load and debug the example on target hardware.
6. Follow the instructions in the example README and use the SDS view to show, record, and playback data streams.

## Example Description

The SDS examples are configured for STMicroelectronics STM32N6570-DK board and use the [MDK-Middleware](https://www.keil.arm.com/packs/mdk-middleware-keil/overview/) for the [SDSIO Interface](https://arm-software.github.io/SDS-Framework/main/sdsio.html).
The examples are configured for [Keil Studio for VS Code](https://www.keil.arm.com/).

| Example                                            | Description   |
|---                                                 |---            |
| [KeywordSpotting](./KeywordSpotting/README.md)     | SDS connection via USB to [STMicroelectronics STM32N6570-DK board](https://www.keil.arm.com/boards/stmicroelectronics-stm32n6570-dk-revc-f2017e0/features/). Implements keyword spotting algorithm with audio interface.  |


## STM32N6570-DK Board Setup

Applications require a FSBL (First Stage Boot Loader) programmed and running on the STM32N6570-DK board. The FSBL is built and flashed to the board using the FSBL_LRUN example. This needs to be done only once, before flashing any other example.

Required ST tool:

- [STM32CubeProgrammer 2.21.0](https://www.st.com/en/development-tools/stm32cubeprog.html)
    - STM32_SigningTool_CLI: Verify the environment variable `STM32_PRG_PATH` points to the folder that contains `STM32_SigningTool_CLI.exe`

Open [FSBL_LRUN Example](./FSBL_LRUN/FSBL/) in VS Code:

- Select **ExtMemLoader** Target Set and click **Build** action button to generate the flash algorithm for STM32N6570-DK board.
- Select **FSBL_Appli** Target Set:
    - Click **Build** action button to generate the FSBL binary.
    - Flash the FSBL binary to the STM32N6570-DK board:
        - Set the boot mode configuration in **development mode** (BOOT1 switch position to 1-3) and reset board after each power on cycle.
        - Click **Views and More Actions** and click **Load application to target** to flash the FSBL binary to the STM32N6570-DK board.
        - Set the boot mode configuration in **flash mode** (BOOT1 switch position to 1-2) and reset board.
        - Configured `LD1_green` (GPIO PO.01) LED should blink (in Appli/Src/main.c).
