[![License](https://img.shields.io/github/license/Arm-Examples/SDS-STM32N6?label)](https://github.com/Arm-Examples/SDS-STM32N6/blob/main/LICENSE)
[![Build_AC6](https://img.shields.io/github/actions/workflow/status/Arm-Examples/SDS-STM32N6/Build_AC6.yml?logo=arm&logoColor=0091bd&label=Build%20examples%20with%20AC6)](https://github.com/Arm-Examples/SDS-STM32N6/tree/main/.github/workflows/Build_AC6.yml)
[![Test_ST_KeywordSpotting](https://img.shields.io/github/actions/workflow/status/Arm-Examples/SDS-STM32N6/Test_ST_KeywordSpotting.yml?logo=arm&logoColor=0091bd&label=Test%20ST%20Keyword%20Spotting)](https://github.com/Arm-Examples/SDS-STM32N6/tree/main/.github/workflows/Test_ST_KeywordSpotting.yml)

# SDS-STM32N6

This repository contains [Synchronous Data Streaming (SDS)](https://github.com/ARM-software/SDS-Framework) example projects for STMicroelectronics STM32N6.

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
   [Action buttons](https://github.com/Open-CMSIS-Pack/vscode-cmsis-solution#action-buttons) to build,
   load and debug the example on target hardware.
6. Follow the instructions in the example README and use the SDS view to show, record, and playback data streams.

## Example Description

The SDS examples are configured for STMicroelectronics STM32N6570-DK board and use the [MDK-Middleware](https://www.keil.arm.com/packs/mdk-middleware-keil/overview/) for the [SDSIO Interface](https://arm-software.github.io/SDS-Framework/main/sdsio.html).
The examples are configured for [Keil Studio for VS Code](https://www.keil.arm.com/).

| Example                                            | Description   |
|---                                                 |---            |
| [KeywordSpotting](./KeywordSpotting/README.md)     | SDS connection via USB to [STMicroelectronics STM32N6570-DK board](https://www.keil.arm.com/boards/stmicroelectronics-stm32n6570-dk-revc-f2017e0/features/). Implements keyword spotting algorithm with audio interface.  |

## Continuous Integration (CI)

The repository uses [GitHub Actions](.github/workflows) to test project build with AC6 and execute algorithm tests.
Refer to [Understanding GitHub Actions](https://docs.github.com/en/actions/get-started/understand-github-actions) and [Arm FVPs](https://arm-software.github.io/AVH/main/infrastructure/html/avh_gh_actions.html) documentation for more information.

| <div style="width:150px"> CI Workflow </div>                                   | Description |
|---                                                                             |---  |
| [Build_AC6](./.github/workflows/Build_AC6.yml)                                 | Use Arm Compiler for Embedded (AC6) to create binaries for different configuration of targets, build types, and boards. |
| [Test_ST_KeywordSpotting](./.github/workflows/Test_ST_KeywordSpotting.yml)     | Build the binary for a keyword spotting algorithm and execute a regression test using an FVP model. Compare the original SDS recording with the newly generated recording produced during the simulator run. Store the build outputs and SDS recordings as workflow artifacts.   |

## STM32N6570-DK Board Setup

Applications require a FSBL (First Stage Boot Loader) programmed and running on the STM32N6570-DK board. The FSBL is built and flashed to the board using the FSBL_LRUN example. This needs to be done only once, before flashing any other example.

Required ST tool:

- [STM32CubeProgrammer 2.21.0](https://www.st.com/en/development-tools/stm32cubeprog.html)
    - STM32_SigningTool_CLI: Verify the environment variable `STM32_PRG_PATH` points to the folder that contains `STM32_SigningTool_CLI.exe`

Open [FSBL_LRUN Example](./FSBL_LRUN/) in VS Code:

- Select **ExtMemLoader** Target Set and click **Build** action button to generate the flash algorithm for STM32N6570-DK board.
- Select **FSBL_Appli** Target Set:
    - Click **Build** action button to generate the FSBL binary.
    - Flash the FSBL binary to the STM32N6570-DK board:
        - Set the boot mode configuration in **development mode** (BOOT1 switch position to 1-3) and reset board after each power on cycle.
        - Click **Views and More Actions** and click **Load application to target** to flash the FSBL binary to the STM32N6570-DK board.
        - Set the boot mode configuration in **flash mode** (BOOT1 switch position to 1-2) and reset board.
        - Configured `LD1_green` (GPIO PO.01) LED should blink (in Appli/Src/main.c).

## Related

- [Arm Examples - Edge AI and Machine Learning](https://github.com/Arm-Examples#edge-ai-and-machine-learning) contains several other examples that use SDS.
- [SDS Framework - Documentation](https://arm-software.github.io/SDS-Framework/main/index.html).
- [Report issues](https://github.com/ARM-software/SDS-Framework/issues) for this example on the SDS-Framework project page.
