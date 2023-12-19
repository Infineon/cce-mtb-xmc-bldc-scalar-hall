# BLDC Scalar Hall XMC&trade;1300

_Disclaimer: This is a community code example (CCE) released for the benefit of the community users. These projects have only been tested for the listed BSPs, tools versions, and toolchains documented in this readme. They are intended to demonstrate how a solution / concept / use-case can be achieved on a particular device. For official code examples, please click [here](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software)._

This community code example (CCE) demonstrates Hall sensor based three phase BLDC motor control application using XMC1300 Boot Kit. In order to test this software, [XMC1000 Motor Control Application Kit](https://www.infineon.com/cms/en/product/evaluation-boards/kit_xmc1x_ak_motor_001/#!documents) is needed.

## Requirements

- [ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) v3.1 or later (tested with v3.1)
- [SEGGER J-Link software](https://www.segger.com/downloads/jlink/#J-LinkSoftwareAndDocumentationPack) v7.90a
- Programming language: C
- Associated parts: [XMC1300 MCU](https://www.infineon.com/cms/en/product/microcontroller/32-bit-industrial-microcontroller-based-on-arm-cortex-m/32-bit-xmc1000-industrial-microcontroller-arm-cortex-m0/xmc1300/)

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; embedded compiler v11.3 (`GCC_ARM`) - Default value of `TOOLCHAIN`

## Supported Kits

- [XMC1300 Boot Kit](https://www.infineon.com/cms/en/product/evaluation-boards/kit_xmc13_boot_001/) (`KIT_XMC13_BOOT_001`)

## Hardware setup

Before using this code example, make sure that the XMC1300 board is correctly connected to the PMSM Low Voltage 15W Motor Card which also needs to be supplied by an external DC power supply (12V to 24V) from its power jack. Please see this [User Manual](https://www.infineon.com/dgdl/Board_Users_Manual_PMSM_LV_15W_Card_R1.pdf?fileId=db3a30433f74fc8b013f755ff55e00e2) for more details. A complete hardware setup example can be seen in Figure 1 below.

<img src="images/hw-setup.png" width="700" height="375" style="border: 2px solid gray; border-radius:15px">

**Figure 1. Complete hardware setup example with XMC1000 Motor Application Kit**

**Note:** Boot Mode Index (BMI) of the device should be checked before using the software. You can use [XMC Flasher](https://softwaretools.infineon.com/tools/com.ifx.tb.tool.xmcflasher2?redirId=159477) tool to check/set it. Make sure that the **SWCLK** switch of the debugger on XMC1300 board is **on** to set the BMI. Open XMCFlasher tool, click **Connect** and choose **XMC1302-0200** from the device list. After connecting to the board, set BMI to **SPD0** as shown in Figure 2. Then disconnect and switch **off** the **SWCLK** on the XMC1300 board.

<img src="images/xmcflasher.png" width="500" height="312" style="border: 2px solid gray; border-radius:15px">

**Figure 2. Set BMI to SPD0 debug mode**

## Software setup

This code example uses Micro Inspector Pro application by default to run and control the motor from a GUI. Click [here](https://softwaretools.infineon.com/tools/com.ifx.tb.tool.ifxmicroinspectorpro) to download the application.

Please follow the steps below to control the motor from the Micro Inspector Pro application.

## Using the code example

Create the project and open it using one of the following:

<details open><summary><b>In Eclipse IDE for ModusToolbox&trade; software (recommended)</b></summary>

1. Click the **New Application** link in the **Quick Panel** (or, use **File** > **New** > **ModusToolbox&trade; Application**). This launches the [Project Creator](https://www.infineon.com/ModusToolboxProjectCreator) tool.

2. Select the kit `KIT_XMC13_BOOT_001` from the **XMC&trade; BSPs** list shown in the **Project Creator - Choose Board Support Package (BSP)** dialog.

3. In the **Project Creator - Select Application** dialog, choose the example from the list **Community Code Examples** by enabling the checkbox.

4. (Optional) Change the suggested **New Application Name**.

5. The **Application(s) Root Path** defaults to the Eclipse workspace which is usually the desired location for the application. If you want to store the application in a different location, you can change the *Application(s) Root Path* value. Applications that share libraries should be in the same root path.

6. Click **Create** to complete the application creation process.

7. To build the project, click **Build Application** from the Quick Panel.

8. To start the debugging session to run the motor, click **Generate Launches for "YourApplicationName"** in Quick Panel. Then click to **YourApplicationName Debug (Jlink)**. A debugging window will appear and the session will automatically pause in a breakpoint. Click **Resume** button from the above toolbar to continue the session.

9. While the debugging session is running, open the Micro Inspector Pro application. Click **Open Workspace** button from the upper left corner.

<img src="images/ss_ucProbeworkspace.png" width="400" height="220" style="border: 2px solid gray; border-radius:15px">

**Figure 3. Opening the workspace folder in Micro Inspector Pro**

10. Find the "BLDC_SCALAR_HALL_XMC13_uCProbe.wspx" file from your ModusToolbox workspace folder and select **Open**. A pop-up window will appear to show the existing elf file. Select the one shown and click **Open**.

<img src="images/open.png" width="500" height="440" style="border: 2px solid gray; border-radius:15px">

**Figure 4. Selecting the elf file**

11. To run and control the motor speed from the GUI, switch to **BLDC: Speed Control** mode and click **Run** button.

**Note:** If you face any issues or errors with Micro Inspector GUI while the kit is in debug mode, please reset the GUI while the debug session is on and restart from step 9.

<img src="images/run.png" width="700" height="450" style="border: 2px solid gray; border-radius:15px">

**Figure 5. Switching to running mode**

12. Press **Motor Start** to run the motor. You can also adjust the motor speed by changing the value under **Setting Target Speed**.

<img src="images/bldc-run.png" width="700" height="350" style="border: 2px solid gray; border-radius:15px">

**Figure 6. Motor control part of the running mode**

13. Right click the **Oscilloscope** tab and select **New Vertical Tab Group** in order to observe your parameters from the oscilloscope on the right side while observing the motor control parameters on the left side simultaneously.

<img src="images/hall.png" width="1000" height="328" style="border: 2px solid gray; border-radius:15px">

**Figure 7. BLDC Motor parameters observed from the oscilloscope**

**Note:** This code does not use the Device Configurator in ModusToolbox. All peripheral definitions and initializations are directly integrated within the software using low level drivers by calling the necessary libraries. When the user wants to change a configuration variable or parameter, it should be done within the code in the user config header files rather than in the Device Configurator.

<img src="images/mtb-cfg.jpg" width="500" height="335" style="border: 2px solid gray; border-radius:15px">

**Figure 8. Device Configurator in ModusToolbox**


For more details, see the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/ide_{version}/docs/mtb_ide_user_guide.pdf*).

</details>

<details open><summary><b>In command-line interface (CLI)</b></summary>


ModusToolbox&trade; software provides the Project Creator as both a GUI tool and the command line tool, "project-creator-cli". The CLI tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/* directory.

Alternatively, you can manually create the application using the following steps:

1. Download and unzip this repository onto your local machine, or clone the repository.

2. Use a CLI terminal to invoke the "project-creator-cli" tool. On Windows, use the command line "modus-shell" program provided in the ModusToolbox&trade; software installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; software tools. You can access it by typing `modus-shell` in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

The "project-creator-cli" tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--board-id` | Defined in the `<id>` field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the `<id>` field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional

<br />

The following example clones the "[BLDC Scalar Hall XMC13](https://github.com/Infineon/cce-mtb-xmc-bldc-scalar-hall)" application with the desired name "cce-mtb-xmc-bldc-scalar-hall" configured for the *KIT_XMC13_BOOT_001* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id KIT_XMC13_BOOT_001 --app-id cce-mtb-xmc-bldc-scalar-hall --user-app-name cce-mtb-xmc-bldc-scalar-hall --target-dir "C:/mtb_projects"
   ```
   
   **Note:** The cloned application contains a default BSP file (*TARGET_xxx.mtb*) in the *bsps* folder. Use the [Library Manager](https://www.infineon.com/ModusToolboxLibraryManager) (`make modlibs` command) to select or add a different BSP file, if required. If the selected kit does not have the required resources or is not supported, the application may not work. For this code example, the supported kits are "**KIT_XMC13_BOOT_001**" and "**KIT_XMC14_BOOT_001**".

3. Import the required libraries by executing the `make getlibs` command.

Various CLI tools include a `-h` option that prints help information to the terminal screen about that tool. For more details, see the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>

<details open><summary><b>In third-party IDEs</b></summary>

**Note:** Only VS Code is supported.

1. Follow the instructions from the **In command-line interface (CLI)** section to create the application, and import the libraries using the `make getlibs` command.

2. Export the application to a supported IDE using the `make <ide>` command.

   For a list of supported IDEs and more details, see the "Exporting to IDEs" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

3. Follow the instructions displayed in the terminal to create or import the application as an IDE project.

</details>

## Related resources


Resources | Links
--------------------|----------------------
Code examples  | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub|
Kit guide|  [XMC1300 boot kit](https://www.infineon.com/dgdl/Board_Users_Manual_XMC1300_CPU_Card_R2.pdf?fileId=db3a30433da5396c013da5d1ef0500b8) – Board user‘s manuals. Describes the schematic and hardware of XMC1300 board.
Device documentation| [XMC1000 family datasheets](https://www.infineon.com/cms/en/product/microcontroller/32-bit-industrial-microcontroller-based-on-arm-cortex-m/32-bit-xmc1000-industrial-microcontroller-arm-cortex-m0/#document-group-myInfineon-49) <br> [XMC1000 family technical reference manuals](https://www.infineon.com/cms/en/product/microcontroller/32-bit-industrial-microcontroller-based-on-arm-cortex-m/32-bit-xmc1000-industrial-microcontroller-arm-cortex-m0/#document-group-myInfineon-44)
Development kits | Buy at www.infineon.com<br>[KIT_XMC13_BOOT_001](https://www.infineon.com/cms/en/product/evaluation-boards/kit_xmc13_boot_001/#!documents) – Boot kit XMC1300 <br> [KIT_XMC1X_AK_MOTOR_001](https://www.infineon.com/cms/en/product/evaluation-boards/kit_xmc1x_ak_motor_001/) – XMC1000 Motor Control Application Kit |
Libraries on GitHub  | [mtb-xmclib-cat3](https://github.com/Infineon/mtb-xmclib-cat3) – XMC&trade; peripheral driver library (XMCLib) and docs 
Tools | [Eclipse IDE for ModusToolbox&trade; software](https://www.infineon.com) – ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems.

## Other resources

Infineon provides a wealth of data at www.infineon.com to help you select the right device, and quickly and effectively integrate it into your design.

For XMC&trade; MCU devices, see [32-bit XMC™ Industrial microcontroller based on Arm® Cortex®-M](https://www.infineon.com/cms/en/product/microcontroller/32-bit-industrial-microcontroller-based-on-arm-cortex-m/).

## Document history

Document title: *CCE#002-38983 - BLDC SCALAR HALL XMC13*

| Version | Description of change |
| ------- | --------------------- |
| 1.0.0   | New community code example      |
------

All other trademarks or registered trademarks referenced herein are the property of their respective owners.


© 2023 Infineon Technologies AG

All Rights Reserved.

### Legal disclaimer

The information given in this document shall in no event be regarded as a guarantee of conditions or characteristics. With respect to any examples or hints given herein, any typical values stated herein and/or any information regarding the application of the device, Infineon Technologies hereby disclaims any and all warranties and liabilities of any kind, including without limitation, warranties of non-infringement of intellectual property rights of any third party.

### Information

For further information on technology, delivery terms and conditions and prices, please contact the nearest Infineon Technologies Office (www.infineon.com).

### Warnings

Due to technical requirements, components may contain dangerous substances. For information on the types in question, please contact the nearest Infineon Technologies Office.

Infineon Technologies components may be used in life-support devices or systems only with the express written approval of Infineon Technologies, if a failure of such components can reasonably be expected to cause the failure of that life-support device or system or to affect the safety or effectiveness of that device or system. Life support devices or systems are intended to be implanted in the human body or to support and/or maintain and sustain and/or protect human life. If they fail, it is reasonable to assume that the health of the user or other persons may be endangered.

-------------------------------------------------------------------------------