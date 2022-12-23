# PSoC&trade; 4: MSCLP multi-touch mutual-capacitance touchpad tuning

This code example demonstrates how to use the CAPSENSE&trade; middleware to detect two finger touch positions on a mutual-capacitance-based touchpad widget in PSoC&trade; 4 devices with multi sense converter low power (MSCLP).

In addition, this code example also explains how to manually tune the mutual-capacitance-based touchpad for optimum performance with respect to parameters such as reliability, power consumption, response time, and linearity using the CSX-RM sensing technique and CAPSENSE&trade; tuner GUI. Here, CAPSENSE&trade; crosspoint (CSX) represents the mutual-capacitance sensing technique and RM represents the ratiometric method.

[View this README on GitHub.](https://github.com/Infineon/mtb-example-psoc4-msclp-mutual-capacitance-touchpad)

[Provide feedback on this code example.](https://cypress.co1.qualtrics.com/jfe/form/SV_1NTns53sK2yiljn?Q_EED=eyJVbmlxdWUgRG9jIElkIjoiQ0UyMzUzMzkiLCJTcGVjIE51bWJlciI6IjAwMi0zNTMzOSIsIkRvYyBUaXRsZSI6IlBTb0MmdHJhZGU7IDQ6IE1TQ0xQIG11bHRpLXRvdWNoIG11dHVhbC1jYXBhY2l0YW5jZSB0b3VjaHBhZCB0dW5pbmciLCJyaWQiOiJzaGFyd2FyaSIsIkRvYyB2ZXJzaW9uIjoiMS4wLjEiLCJEb2MgTGFuZ3VhZ2UiOiJFbmdsaXNoIiwiRG9jIERpdmlzaW9uIjoiTUNEIiwiRG9jIEJVIjoiSUNXIiwiRG9jIEZhbWlseSI6IlBTT0MifQ==)


## Requirements

- [ModusToolbox&trade; software](https://www.cypress.com/products/modustoolbox-software-environment) v3.0 or later

   **Note:** This code example version requires ModusToolbox&trade; software version 3.0 or later, and is not backward compatible with v2.4 or older versions.

- Board support package (BSP) minimum required version: 0.5.0
- Programming language: C
- Associated parts: [PSoC&trade; 4000T](https://www.infineon.com/002-33949)

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; embedded compiler v10.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`
- Arm&reg; compiler v6.13 (`ARM`)
- IAR C/C++ compiler v8.42.2 (`IAR`)

## Supported kits (make variable 'TARGET')

- [PSoC&trade; 4000T CAPSENSE&trade; evaluation kit](https://www.infineon.com/CY8CKIT-040T) (`CY8CKIT-040T`) - Default value of `TARGET`

## Hardware setup

This example uses the board's default configuration. See the [Kit user guide](www.infineon.com/002-34472) to ensure that the board is configured correctly. Follow the [Steps to set up the VDDA supply voltage in device configurator](#steps-to-set-up-the-vdda-supply-voltage-in-device-configurator) for optimum performance of the device with the given supply voltage.

## Software setup

This example requires no additional software or tools.

## Using the code example

Create the project and open it using one of the following:

<details><summary><b>In Eclipse IDE for ModusToolbox&trade; software</b></summary>

1. Click the **New Application** link in the **Quick Panel** (or, use **File** > **New** > **ModusToolbox Application**). This launches the [Project Creator](https://www.cypress.com/ModusToolboxProjectCreator) tool.

2. Pick a kit supported by the code example from the list shown in the **Project Creator - Choose Board Support Package (BSP)** dialog.

   When you select a supported kit, the example is reconfigured automatically to work with the kit. To work with a different supported kit later, use the [Library Manager](https://www.infineon.com/dgdl/Infineon-ModusToolbox_Library_Manager_User_Guide_3-UserManual-v01_00-EN.pdf?fileId=8ac78c8c7d718a49017d99ab34b831ce) to choose the BSP for the supported kit. You can use the Library Manager to select or update the BSP and firmware libraries used in this application. To access the Library Manager, click the link from the **Quick Panel**.

   You can also just start the application creation process again and select a different kit.

   If you want to use the application for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. In the **Project Creator - Select Application** dialog, choose the example by enabling the checkbox.

4. (Optional) Change the suggested **New Application Name**.

5. The **Application(s) Root Path** defaults to the Eclipse workspace, which is usually the desired location for the application. If you want to store the application in a different location, you can change the *Application(s) Root Path* value. Applications that share libraries should be in the same root path.

6. Click **Create** to complete the application creation process.

For more details, see the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/dgdl/Infineon-Eclipse_IDE_for_ModusToolbox_User_Guide_1-UserManual-v01_00-EN.pdf?fileId=8ac78c8c7d718a49017d99bcb86331e8) (locally available at *{ModusToolbox&trade; software install directory}/ide_{version}/docs/mt_ide_user_guide.pdf*).

</details>

<details><summary><b>In command-line interface (CLI)</b></summary>

ModusToolbox&trade; software provides the Project Creator as both a GUI tool and the command line tool, "project-creator-cli". The CLI tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the "project-creator-cli" tool. On Windows, use the command line "modus-shell" program provided in the ModusToolbox&trade; software installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; software tools. You can access it by typing `modus-shell` in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

This tool has the following arguments:

Argument | Description | Required/optional
-----------|-------------|-----------
`--board-id` | Defined in the `<id>` field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the `<id>` field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional
<br>

The following example will clone the "[CAPSENSE&trade; MSCLP mutual capacitance touchpad tuning](https://github.com/Infineon/mtb-example-psoc4-msclp-mutual-capacitance-touchpad)" application with the desired name "MSCLPMutualCapTouchpadTuning" configured for the *CY8CKIT-040T* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id CY8CKIT-040T --app-id mtb-example-psoc4-msclp-mutual-capacitance-touchpad --user-app-name MSCLPMutualCapTouchpadTuning --target-dir "C:/mtb_projects"
   ```

**Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For details, see the "Project creator tools" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/dgdl/Infineon-ModusToolbox_2.4_User_Guide-Software-v01_00-EN.pdf?fileId=8ac78c8c7e7124d1017ed97e72563632) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>

<details><summary><b>In third-party IDEs</b></summary>

Use one of the following options:

- **Use the standalone [Project Creator](https://www.infineon.com/dgdl/Infineon-ModusToolbox_Project_Creator_Guide_3-UserManual-v01_00-EN.pdf?fileId=8ac78c8c7d718a49017d99bcabbd31e5) tool:**

   1. Launch Project Creator from the Windows start menu or from *{ModusToolbox&trade; software install directory}/tools_{version}/project-creator/project-creator.exe*.
   2. In the initial **Choose Board Support Package** screen, select the BSP, and click **Next**.
   3. In the **Select Application** screen, select the specific IDE from the **Target IDE** drop-down menu.
   4. Click **Create** and follow the instructions printed in the bottom pane to import or open the exported project in the respective IDE.
<br> 

- **Use command-line interface (CLI):**

   1. Follow the instructions from the **In command-line interface (CLI)** section to create the application, and import the libraries using the `make getlibs` command.

   2. Export the application to a supported IDE using the `make <ide>` command.

   3. Follow the instructions displayed in the terminal to create or import the application as an IDE project.

For a list of supported IDEs and more details, see the "Exporting to IDEs" section of the [ModusToolbox&trade; software user guide](https://www.infineon.com/dgdl/Infineon-ModusToolbox_2.4_User_Guide-Software-v01_00-EN.pdf?fileId=8ac78c8c7e7124d1017ed97e72563632) (locally available at *{ModusToolbox&trade; software install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>

The project already has the necessary settings by default, so you can go to [Operation](#operation) to verify the operation. If you want to understand the tuning process and follow the stages for this kit or your own board, go to [Tuning procedure](#tuning-procedure) and then test it using [Operation](#operation).

## Operation

1. Connect the board to your PC using the provided micro USB cable through the KitProg3 USB connector as follows:

   **Figure 1. Connecting the CY8CKIT-040T kit to a computer**

   <img src="images/kit_connection.png" alt="" width="400" />

2. The SWD, UART, and I2C modes are multiplexed to the same pins (GPIO Pins P3[2] and P3[3]) in CY8CKIT-040T. Therefore, the interface can be switched between these using the FW-loader commands. Download and unzip the *Batch_files_for_mux_selection* zipped file from the Beta package to the *bin* folder inside the *fw-loader* folder in the ModusToolbox&trade; installation directory. 
    
   Default location: */ModusToolbox/tools_3.0/fw-loader/bin*
   
   Select the SWD mode by running the *Select_SWD* batch file to program the CY8CKIT-040T kit. For detailed information, see **Section 2.3.1** in [CY8CKIT-040T kit user guide](www.infineon.com/002-34472).

   **Note:** SWD mode is selected by default upon reset, therefore it is not required to run the batch file after reset.

3. Program the board using one of the following:

   <details><summary><b>Using Eclipse IDE for ModusToolbox&trade; software</b></summary>

      1. Select the application Project in the Project Explorer.

      2. In the **Quick Panel**, scroll down, and click **\<Application Name> Program (KitProg3_MiniProg4)**.
   </details>

   <details><summary><b>Using CLI</b></summary>

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. You can specify a target and toolchain manually:
      ```
      make program TARGET=<BSP> TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TARGET=CY8CKIT-040T TOOLCHAIN=GCC_ARM
      ```
   </details>

4. After programming, the application starts automatically.

5. To test the application, slide your finger over the CAPSENSE&trade; touchpad and notice that LED1 and LED3 turn ON with green color when touched and turn OFF when the finger is lifted.
   - LED1 brightness increases when finger is moved from left to right, with left column having minimum and right column having maximum brightness.
   - LED3 brightness increases when finger is moved from bottom to up, with bottom row having minimum and top row having maximum brightness.

### Monitor data using CAPSENSE&trade; tuner

You can also monitor the CAPSENSE&trade; data using the CAPSENSE&trade; tuner application as follows:

1. Select the I2C mode by running the *Select_I2C* batch file to enable the I2C communication between onboard KitProg and CAPSENSE&trade; tuner.

2. Open CAPSENSE&trade; tuner from the tools section in the IDE Quick Panel. 
    
      You can also run the CAPSENSE&trade; tuner application standalone from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-tuner*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS/* folder. 

     See the [ModusToolbox&trade; user guide](https://www.infineon.com/dgdl/Infineon-ModusToolbox_2.4_User_Guide-Software-v01_00-EN.pdf?fileId=8ac78c8c7e7124d1017ed97e72563632) (locally available at *ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf*) for options to open the CAPSENSE&trade; tuner application using the CLI.

3. Ensure that the kit is in CMSIS-DAP bulk mode (KitProg3 status LED is ON and not blinking). See [Firmware-loader](https://github.com/Infineon/Firmware-loader) to learn on how to update the firmware and switch modes in KitProg3.

4. In the tuner application, click on the **Tuner Communication Setup** icon or select **Tools** > **Tuner Communication Setup**. In the window that appears, select the I2C checkbox under KitProg3 and configure as follows:

   - **I2C address:** 8
   - **Sub-address:** 2 bytes
   - **Speed (kHz):** 400

   These are the same values set in the EZI2C resource.

   **Figure 2. Tuner communication setup parameters**

   <img src="images/tuner-comm-setup.png" alt="" width="600" />

5. Click **Connect** or select **Communication** > **Connect** to establish a connection.  

      **Figure 3. Establish connection**

      <img src="images/tuner-connect.png" alt="" width="400" />

6. Click **Start** or select **Communication** > **Start** to start data streaming from the device.
      
      **Figure 4. Establish connection**

      <img src="images/tuner-start.png" alt="" width="400" />

      The tuner displays the data from the sensor in the **Widget View**, **Graph View** and **Touchpad View** tabs.

7. Set the **Read Mode** to the **Synchronized** mode. Under the **Widget View** tab, you can see the touchpad widget sensors highlighted when you touch it.

   **Figure 5. Widget view of the CAPSENSE&trade; Tuner**

   <img src="images/widget-view.png" alt=""/>

8. You can view the raw count, baseline, difference count for each sensor and also the touchpad position in the **Graph View** tab. For example, to view the sensor data for a single sensor in Touchpad, select **Touchpad_Rx0_Tx0** under **Touchpad**.

   **Figure 6. Graph view of the CAPSENSE&trade; tuner**

   <img src="images/graph_view.png" alt=""/>

9. The **Touchpad View** tab shows the heat map view; it visualizes the finger movement.

   **Figure 7. Touchpad view of the CAPSENSE&trade; Tuner**

   <img src="images/touchpad-view-tuner.png" alt=""/>

10. Observe the **Widget/Sensor Parameters** section in the CAPSENSE&trade; Tuner window. The compensation CDAC values for each touchpad sensor element calculated by the CAPSENSE&trade; resource is displayed as shown in **Figure 7**.

11. Verify that the SNR is greater than 5:1 by following the steps given in **Stage 4** starting with **Step 6** in the [Tuning procedure](#tuning-procedure).

The linearity of the position graph, non-reporting of false touches, and no discontinuity in the line drawing indicate a proper tuning.

## Tuning procedure

<details><summary><b> Create custom BSP for your board </b></summary>

1. Create a custom BSP for your board having any device, by following the steps given in [KBA231373](https://community.infineon.com/t5/Knowledge-Base-Articles/ModusToolbox-2-2-and-later-Make-a-Custom-BSP-KBA231373/ta-p/251107). In this code example, it was created for the device "CY8C4046LQI-T452".

2. Open the *design.modus* file from the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS/* folder obtained in the previous step and enable CAPSENSE&trade; to get the *design.cycapsense* file. CAPSENSE&trade; configuration can then be started from scratch as explained in the following steps.

</details>

The following steps explain the tuning procedure.

**Note:** See the section **Selecting CAPSENSE&trade; hardware parameters** in the [AN85951 - PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/an85951) to learn about the considerations for selecting each parameter values.

**Figure 8. CSX touchpad widget tuning flow**

<img src="images/flowchart_for_tuning.png" alt="" width="600" />

Do the following to tune the touchpad:

<details><summary><b>Stage 1: Set the initial hardware parameters</b></summary>

1. Connect the board to your PC using the provided USB cable through the KitProg3 USB connector.

2. Launch the Device configurator tool.
   
   You can launch the Device configurator in Eclipse IDE for ModusToolbox&trade; from the **Tools** section in the IDE Quick panel or in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/device-configurator/device-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.modus* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS/* folder.

3. In the [PSoC&trade; 4000T kit](https://www.infineon.com/CY8CKIT-040T), the touchpad pins are connected to CAPSENSE&trade; channel (MSCLP 0). Therefore, make sure that you enable CAPSENSE&trade; channel in the Device configurator as shown in **Figure 9**.

   **Figure 9. Enable MSCLP channel in device configurator**

   <img src="images/device-configurator-channel.png" alt=""/>

   Save the changes and close the window.

4. Launch the CAPSENSE&trade; configurator tool.
   
   You can launch the CAPSENSE&trade; configurator tool in Eclipse IDE for ModusToolbox&trade; from the 'CAPSENSE&trade;' peripheral setting in the device configurator or directly from the **Tools** section in the IDE Quick panel. You can also launch it in standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is present in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/COMPONENT_BSP_DESIGN_MODUS/* folder.

   See the [ModusToolbox&trade; CAPSENSE&trade; configurator tool guide](https://www.infineon.com/dgdl/Infineon-ModusToolbox_CAPSENSE_Configurator_Guide_4-UserManual-v01_00-EN.pdf?fileId=8ac78c8c7d718a49017d99ab1e6531c8) for step-by-step instructions on how to configure and launch CAPSENSE&trade; in ModusToolbox&trade;.

5. In the **Basic** tab, note that a touchpad **Touchpad** is configured with **CSX RM (Mutual-cap)** Sensing Mode.  

   **Figure 10. CAPSENSE&trade; configurator - Basic tab**

   <img src="images/capsense_basictab.png" alt=""/>

6. Do the following in the **General** sub-tab under the **Advanced** tab:

   - Select **CAPSENSE&trade; IMO clock frequency** as 48 MHz.
   
   - Set **Modulator clock divider** as **1** to obtain the maximum available modulator clock frequency as recommended in the [AN85951 - PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/an85951).

      **Note:** The modulator clock frequency can be set to 48,000 kHz after changing the CAPSENSE&trade; IMO clock frequency to 48 MHz, because the modulator clock is derived from the CAPSENSE&trade; IMO clock. In the **CAPSENSE&trade; IMO clock frequency** drop-down list, select **48 MHz**.
   
   - **Number of init sub-conversions** is set based on the hint shown when you hover over the edit box. Retain the default value.

   - It is recommended to **Enable IIR filter (first order)** and set the **IIR filter raw count coefficient** to 128 when CIC2 filter is enabled. You can enable other filters later depending on the signal-to-noise ratio (SNR) requirements in **Stage 5**.

      Filters are used to reduce the peak-to-peak noise. Using filters will result in higher scan time.

   **Figure 11. CAPSENSE&trade; Configurator - General settings**

   <img src="images/adv_general.png" alt=""/>

   **Note:** Each tab has a **Restore Defaults** button to restore the parameters of that tab to their default values.

7. Go to the **CSX Settings** tab and make the following changes:

   - Set **Inactive Sensor connection** as **Ground**.

   - Set **Number of reported fingers** as **2** for two-finger detection.

   - Select **Enable CDAC auto-calibration** and **Enable compensation CDAC**.

     This helps in achieving the required CDAC calibration levels (40% of maximum count) for all sensors in the widget while maintaining the same sensitivity across the sensor elements.

   - Select **Enable CDAC dither**.

      This helps in removing flat-spots, by adding white noise that moves the conversion point around the flat-spots region.

   **Figure 12. CAPSENSE&trade; configurator - Advanced CSX settings**

   <img src="images/adv_csx.png" alt=""/>

8. Go to the **Widget Details** tab. Select **Touchpad** from the left pane, and then set the following:

   - **Maximum X-Axis position** and **Maximum Y-Axis position** to 255.

   - **Tx clock divider:** Retain default value (will be set in **Stage 3**)

   - **Clock source:** **Direct**

      **Note:** Spread spectrum clock (SSC) or PRS clock can be used as a clock source to deal with EMI/EMC issues.

   - **Number of sub-conversions:** 100

     100 is a good starting point to ensure a fast scan time and sufficient signal. This value will be adjusted as required in **Stage 5**. 

   - **Finger Threshold:** 20

     Finger Threshold is initially set to a low value, which allows the **Touchpad View** to track the finger movement during tuning.

   - **Noise Threshold:** 10

   - **Negative Noise Threshold:** 10 

   - **Hysteresis:** 5

     These values reduce the influence of baseline on the sensor signal, which helps to get the true difference count. Retain the default values for all other threshold parameters; these parameters are set in **Stage 6**. 

   **Figure 13. CAPSENSE&trade; configurator - Widget details settings**

   <img src="images/adv_widget_detail.png" alt="" />

9. Go to the **Scan Configuration** tab to select the pins and scan slots. 
   
   - Configure pins for the electrodes using the drop-down menu.

   - Configure the scan slots using the **Auto-Assign Slots** option.

      The summary section in the **Scan Configuration** tab shows 20 scan slots (for 20 sensors). Each sensor is allotted a scan slot based on the slot number. 

      See [AN85951 - PSoC&trade;4 and PSoC&trade;6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/an85951) for more details on Scan slot allotment rules. 

   - Check the notice list for warning or errors.
      **Note:** Enable the **Notice List** from the **View** menu if the notice list is not visible.

   **Figure 14. Scan configuration tab**

   <img src="images/scan-config.png" alt=""/>

10. Click **Save** to apply the settings.

</details>

<details><summary><b>Stage 2: Measure the parasitic capacitance (Cp) </b></summary>

To determine the maximum Tx/Rx Cp, measure the Cp of each Tx and Rx sensor element of the touchpad, between the sensor electrode (sensor pin) and device ground, using an LCR meter.

It can also be estimated by back-calculating for Cs (sensor capacitance) using the Raw Count equation. See [AN234231 - Achieving lowest-power capacitive sensing with PSoC&trade; 4000T](https://www.cypress.com/AN234231) for the Raw Count equation.

   **Table 1. Cp values obtained for CY8CKIT-040T kit**

   | Kit     | Maximum Rx parasitic capacitance (C<sub>P_Col</sub>) in pF | Maximum Tx parasitic capacitance (C<sub>P_Row</sub>) in pF |
   |:---------------------|:----------------------------------------| :-----|
   | CY8CKIT-040T kit            |     12           | 16 |

</details>

<details><summary><b>Stage 3: Calculate the Tx clock frequency </b></summary>

1. Calculate the Tx clock frequency using **Equation 1**.

   **Equation 1. Maximum Tx clock frequency**

   ![Equation 1](images/fsw-equation.png)

   Where,

   - F<sub>Tx</sub> is the Tx clock frequency.

   - C<sub>P_Tx</sub> and C<sub>P_Rx</sub> are the maximum parasitic capacitance of the Tx and Rx electrodes respectively.

   - R<sub>Series</sub> is the maximum total series resistance, which includes the internal resistance (which is approximately 500-ohm), the external series resistance (in CY8CKIT-040T, it is 2 kilo-ohm), and the trace resistance. Include the trace resistance if high-resistive material such as ITO or conductive ink is used. The external resistor is connected between the sensor pad and the device pin to reduce the radiated emission. ESD protection is built into the device.

2. Set an initial Tx clock divider value as per the F<sub>Tx</sub> calculated above and look at the charge and discharge waveforms of the sensor electrodes and iteratively change the divider using the CAPSENSE&trade; tuner and set a maximum frequency such that it completely charges and discharges in each phase of the MSCLP CSX sensing method.

   **Note:** The maximum frequency set should charge and discharge the sensor completely, which you can verify using an oscilloscope and an active probe. To view the charging and discharging waveforms of the sensor, probe at the sensors (or as close as possible to the sensors), and not at the pins or resistor.

   **Figure 15** and **Figure 16** show the waveforms of complete and incomplete charging and discharging of sensor respectively:

      **Figure 15. Complete charging and discharging**
   
      <img src="images/sensors-charging-complete.png" alt=""/>

      **Figure 16. Incomplete charging and discharging**
   
      <img src="images/sensors-charging-incomplete.png" alt=""/>
   
   **Table 2. Tx clock frequency settings for CY8CKIT-040T**

   | Development kit | Maximum Cp of sensor electrodes (pF) | R<sub>SeriesTotal</sub> (Ω) | Maximum Tx clock frequency (MHz) based on sensor Cp | Actual Tx clock frequency (kHz) |
   | :--------- | :------------ | :------------ | :------------ | :------------ |
   | CY8CKIT-040T (Row Sensor Pin P2.1, P2.2, P2.3, P2.4)| 16 | 2500 | 2.5 | 2.4 |

   **Notes:** 
   - Actual Tx clock frequency value is chosen such that the divider is divisible by 2, in order to have the 2 scan phases for equal durations. 

   - The Tx clock divider value, as given by **Equation 2**, is obtained by dividing HFCLK (48 MHz) by **Maximum Tx clock frequency (kHz)** calculated in **Stage 3** (see **Table 2**) and choosing the nearest ceiling sense clock divider option in the configurator.
      
      **Equation 2. Tx clock divider**

      ![Equation 2](images/tx-clock-divider.png)

      In this case, Tx clock divider = 48/2.4 = 20.

   It is recommended to set the Tx clock divider = **24** as it is observed that for the CY8CKIT-040T kit CSX touchpad, the sensors charge and discharge completely at Tx clock frequency = 2 MHz.

   Set the calculated value for the widget **Touchpad** using the steps given in **Step 8** in **Stage 1**, which ensures the maximum possible sense clock frequency (for good gain) while allowing the sensor capacitance to fully charge and discharge in each phase of the MSCLP CSX sensing method. 

3. Ensure that the following conditions are also satisfied when selecting the Tx clock frequency and CDAC compensation divider:

   - If you are explicitly using the PRS or SSCx clock source for EMI/EMC tests, ensure that you select the Tx clock frequency that meets the conditions mentioned in the [ModusToolbox&trade; CAPSENSE&trade; configurator guide](https://www.infineon.com/dgdl/Infineon-ModusToolbox_CapSense_Configurator_Guide_(Version_2.0)-Software-v01_00-EN.pdf?fileId=8ac78c8c7e7124d1017ed9999c3b364d) in addition to the above conditions. PRS and SSCx techniques spread the frequency across a range. The maximum frequency set should charge and discharge the sensor completely, which you can verify using an oscilloscope and an active probe.

</details>

<details><summary><b> Stage 4: Obtain the cross-over point and noise </b></summary>

1. Program the board.

2. Select the I2C mode by running the *Select_I2C* batch file as mentioned in section **Monitor data using CAPSENSE&trade; Tuner**. Launch the CAPSENSE&trade; Tuner to monitor the CAPSENSE&trade; data and for CAPSENSE&trade; parameter tuning and SNR measurement.

   See the [CAPSENSE&trade; tuner guide](https://www.infineon.com/dgdl/Infineon-ModusToolbox_CAPSENSE_Tuner_Guide_4-UserManual-v01_00-EN.pdf?fileId=8ac78c8c7d718a49017d99ab0fda31c5) for step-by-step instructions on how to launch and configure the CAPSENSE&trade; Tuner in ModusToolbox&trade; software.

3. Ensure that the auto-calibrated CDAC is within the recommended range.

   **Note:** Calibration may fail if the obtained raw counts is not within the targeted range. 

   - As discussed in **Step 2** of **Stage 3**, the Tx clock divider will be tuned to bring the CDAC values to the recommended range in this step.

   - Click **Touchpad** in the **Widget Explorer** to view the reference CDAC value in the sensor parameters window as shown in **Figure 17**.

   - Also, click each sensor element (*Touchpad_Rx0_Tx0* for example) in the **Widget Explorer** to view the compensation CDAC in the sensor parameters window as shown in **Figure 17**.

   - If the reference CDAC value is within the range (10/Compensation CDAC Divider) to 255 and compensation CDAC values are in the range 1 to 255, then step 5 is not required.

     **Figure 17. CDAC value**

     <img src="images/tuner-cdac-setting.png" alt="" width="500"/>

   See the [AN85951 - PSoC&trade;4 and PSoC&trade;6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) for the recommended guidelines on valid CDAC range (with and without compensation enabled) to result in calibration PASS across multiple boards because of board-to-board variations.

4. If the above condition is not satisfied, fine-tune the Tx clock divider to bring the CDAC value within range.

   From **Raw Count Equation** in [AN234231 - Achieving lowest-power capacitive sensing with PSoC&trade; 4000T](https://www.infineon.com/AN234231), it is evident that decreasing the Tx clock divider will increase the reference CDAC value for a given calibration percent and vice versa.

   1. If the reference CDAC value is not in the recommended range, decrease the Tx clock divider in the Widget Hardware Parameters window.

   2. Click **To Device** to apply the changes to the device as shown in **Figure 18**.
   
      **Figure 18. Apply changes to device**

      <img src="images/tuner-apply-to-device.png" alt="" width="600"/>

   3. Click each sensor element, for instance, **Touchpad_Rx0_Tx0** in the Widget Explorer.

   4. Observe the compensation CDAC value in the **Sensing Parameters** section of the Widget/Sensor Parameters window.

   5. If the reference CDAC values are still not in the required range and F<sub>Tx</sub> is exceeding the allowed limit, reduce the modulator clock frequency to the next lower value.

   6. Repeat steps 1 to 6 until you obtain Reference CDAC values in the range (10/Compensation CDAC Divider) to 255 and Compensation CDAC values are in the range 1 to 255.

      **Note:** As **Figure 17** shows, CDAC values are already in the recommended range. Therefore, you can leave the Tx clock divider to the value as shown in **Step 2** of **Stage 3**.

5. Capture the raw counts of each sensor element in the touchpad (as shown in **Figure 19**) and verify that they are approximately (+/- 5%) equal to 40% of the MaxCount. See [AN234231 - Achieving lowest-power capacitive sensing with PSoC&trade; 4000T](https://www.infineon.com/AN234231) for the MaxCount equation.

   1. Go to the **Touchpad View** tab and change the **Display settings** as follows:

      - **Data type:** RawCount

      - **Value type:** Current

      - **Number of samples:** 1000

    **Figure 19. Raw counts obtained on the Touchpad View tab in the tuner window**

     <img src="images/touchpad-view-rc.png" alt="" />

6. Capture and note the peak-to-peak noise of each sensor element in the touchpad.

   1. From the **Widget Explorer** section, select the  **Touchpad** widget.

   2. Go to the **Touchpad View** tab and change the **Display settings** as follows:

      - **Display mode:** Touch Reporting

      - **Data type:** RawCount

      - **Value type:** Max-Min

      - **Number of Samples:** 1000

      Capture the variation in the raw counts for 1000 samples, without placing a finger (which gives the peak-to-peak noise) and note the highest noise.

      **Note:** Under **Widget selection**, enable **Flip Y-axis** and **Swap XY-axes** for proper visualization of finger movement on the touchpad.

      **Figure 20. Noise obtained on the Touchpad View tab in the tuner window**

      <img src="images/touchpad-view-noise.png" alt="" />

      **Table 3. Max peak-to-peak noise obtained in CY8CKIT-040T**

      |Kit | Max peak-to-peak noise|
      |:----------|:-------------------------|
      |CY8CKIT-040T   |324|

7. A finger (6 mm) should be held on the touchpad in the least touch intensity (LTI) position (at the intersection of four nodes) as shown in the following figure.

   **Figure 21. Least touch intensity (LTI) position**

   <img src="images/lti-position.png" alt="" width="100" />

   **Note:** Finger movement during the test can artificially increase the noise level.

   1. Go to the **Touchpad View** tab and change the **Display settings** as follows:

      - **Display mode:** Touch Reporting

      - **Data type:** DiffCount

      - **Value type:** Current

   2. Place the finger such that an almost equal signal is obtained in all four intersecting nodes (look at the heat map displayed in the **Touchpad View** tab as shown in **Figure 22**).

      **Note:** The LTI signal is measured at the farthest point of the touchpad from the sensor pin connection, where the sensors have the worst-case RC-time constant.

      **Figure 22. LTI position in touchpad view**

      <img src="images/touchpad-view-lti.png" alt="" />

      LTI Signal = (1651 + 1764 + 1680 + 1682)/4 = 1694

</details>

<details><summary><b> Stage 5. Use the CAPSENSE&trade; tuner to fine-tune the sensitivity for 5:1 SNR </b></summary>

The CAPSENSE&trade; system may be required to work reliably in adverse conditions such as a noisy environment. The touchpad sensors should be tuned with SNR > 5:1 to avoid triggering false touches and to make sure that all intended touches are registered in these adverse conditions.

**Note:** For gesture detection, it is recommended to have approximately 10:1 SNR.

1. Ensure that the LTI Signal count is greater than 50 and meets at least 5:1 SNR (using **Equation 3**).

   In the **CAPSENSE&trade; Tuner** window, increase the **Number of sub-conversions** (located in the **Widget/Sensor Parameters** section, under **Widget Hardware Parameters**) by 10 until you achieve this requirement.

   **Equation 3: Measuring the SNR**

   ![Equation 3](images/snr-equation.png)

   Where,

   - LTI signal is the signal obtained as shown in **Figure 22**

   - Pk-Pk noise is the peak-to-peak noise obtained as shown in **Figure 20**

   SNR is measured using **Equation 3**.

   Here, from **Figure 20** and **Figure 22**,

   SNR = 1694/324 = **5.2**

   **Note:** Ensure that the **Number of sub-conversions** (Nsub) does not exceed the max limit and saturate the raw count.

2. Update the number of sub-conversions

   - Update the number of sub-conversions (Nsub) directly in the **Widget/Sensor parameters** tab of the CAPSENSE&trade; tuner.

   - CY8CKIT-040T has an in-built CIC2 filter which increases the resolution for the same scan time, see [AN234231 - Achieving lowest-power capacitive sensing with PSoC&trade; 4000T](https://www.infineon.com/AN234231) for detailed information on CIC2 filter.

   - Current consumption is directly proportional to number of sub-conversion, therefore decrease the number of sub-conversions to achieve lower current consumption.

      **Note:** Number of sub-conversion should be greater than or equal to 4.

   - Calculate decimation rate using **Equation 4**. Resolution increases with increase in decimation rate, therefore set the maximum decimation rate.

      **Equation 4. Decimation rate**

      ![Equation 4](images/decimation-equation.png)

      **Note:** Decimation rate should not exceed 255.

3. After changing the **Number of sub-conversions**, click **Apply to Device** to send the setting to the device. The change is reflected in the graphs.

   **Note:** The **Apply to Device** option is enabled only when the **Number of sub-conversions** is changed.

4. If the SNR condition is not achieved even with the maximum number of sub-conversions, enable filters in the **General** settings (go to the **Advanced** tab of the CAPSENSE&trade; configurator). This is generally not required for this kit.
</details>

<details><summary><b> Stage 6: Use the CAPSENSE&trade; tuner to tune threshold parameters </b></summary>

After confirming that your design meets the timing parameters and power requirements, and the SNR is greater than 5:1, set your threshold parameters.

**Note:** Thresholds are set based on the LTI position, because it is the least valid touch signal that can be obtained.

Set the recommended threshold values for the Touchpad widget using the LTI signal value obtained in **Stage 5**:

   - **Finger Threshold:** 80% of the LTI signal

   - **Noise Threshold:** Twice the highest noise or 40% of the LTI signal (whichever is greater)

   - **Negative Noise Threshold:** Twice the highest noise or 40% of the LTI signal (whichever is greater)

   - **Hysteresis**

      Do the following:

      1. Place the finger in the LTI position.

      2. Set the **Data type** to DiffCount and **Value type** to Max-Min in the **Touchpad View** tab and click **Clear**.

      3. Record the max-min count value (Max_Min_count) of the selected 2x2 sensors.

         **Figure 23. Obtaining the hysteresis**

         <img src="images/touchpad-view-hys.png" alt="" width="1000" />

      4. Hysteresis = Max_Min_count/2 = 423/2 = 211

   - **ON Debounce:** Default value of 3 (Set to 1 for gesture detection)

   - **Low Baseline Reset:** Default value of 30

   - **Velocity:** Default value of 2500

      **Note:** For multiple finger detection, if the velocity value is low, two touches at different positions are considered to be two different finger touches. On the other hand, if it is set at a higher value, it is considered to be the same finger moving to a different position.

   **Table 4. Software tuning parameters obtained for CY8CKIT-040T**

   |Parameter|	CY8CKIT-040T |
   |:--------|:------|
   |Number of Sub-conversions	| 100 |
   |Finger threshold 	| 1355 |
   |Noise threshold | 677 |
   |Negative noise threshold	| 677 |
   |Low baseline reset	| 30 |
   |Hysteresis	| 211 |
   |ON debounce	| 3 |
   |Velocity| 2500 |

#### **Apply settings to firmware**

1. Click **Apply to Device** and **Apply to Project** in the CAPSENSE&trade; Tuner window to apply the settings to the device and project, respectively. Close the tuner.

   **Figure 24. Apply to Project**

   <img src="images/apply_to_project.png" alt="" width="500" />

    The change is updated in the *design.cycapsense* file and reflected in the CAPSENSE&trade; configurator.

</details>

## Debugging

You can debug the example to step through the code. In the IDE, use the **\<Application Name> Debug (KitProg3_MiniProg4)** configuration in the **Quick Panel**. For more details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; software user guide](https://www.infineon.com/MTBEclipseIDEUserGuide).

**Note:** The debug port is disabled by default for CY8CKIT-040T, because it uses the pins P3[2] (SWDIO) and P3[3] (SWDCK) for I2C SDA and SCL. If debug is required - 
   1. Enable the **Debug Mode** under the **Systems** tab in the **Device Configurator** and change the **Debug Mode** setting to **SWD**. 
   2. Configure SWDIO as P3[2] and SWDCK as P3[3] pins.
   3. Disable I2C in the project by disabling the **Serial Communication Block (SCB)** resource with **EZI2C** personality in **Peripherals Tab** in the **Device Configurator**.
   4. Enable the **SWD_DEBUG_ENABLE** macro present in the *main.c* file as follows: *#define SWD_DEBUG_ENABLE (1u)*. See **Step 4** in **Section 2.3** of the Kit guide for more details.

## Design and implementation

The project contains a touchpad widget configured in CSX-RM Sensing Mode. See the [Tuning procedure](#tuning-procedure) section for step-by-step instructions to configure the other settings of the **CAPSENSE&trade; configurator**.

The project uses the [CAPSENSE&trade; middleware](https://Infineon.github.io/capsense/capsense_api_reference_manual/html/index.html); see the [ModusToolbox&trade; software user guide](https://www.infineon.com/dgdl/Infineon-ModusToolbox_2.4_User_Guide-Software-v01_00-EN.pdf?fileId=8ac78c8c7e7124d1017ed97e72563632) for more details on selecting a middleware. 

See [AN85951 - PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) for more details of CAPSENSE&trade; features and usage. 

The [ModusToolbox&trade; software](https://www.infineon.com/cms/en/design-support/tools/sdk/modustoolbox-software/) provides a GUI-based tuner application for debugging and tuning the CAPSENSE&trade; system. The CAPSENSE&trade; tuner application works with EZI2C and UART communication interfaces. This project has an SCB block configured in EZI2C mode to establish communication with the on-board KitProg, which in turn enables reading the CAPSENSE&trade; raw data by the CAPSENSE&trade; tuner, see **Figure 26**.

The CAPSENSE&trade; data structure that contains the CAPSENSE&trade; raw data is exposed to the CAPSENSE&trade; tuner by setting up the I2C communication data buffer with the CAPSENSE&trade; data structure. This enables the tuner to access the CAPSENSE&trade; raw data for tuning and debugging CAPSENSE&trade;.

The successful tuning of the touchpad is indicated by the RGB LED in the evaluation kit; the LED1 brightness increases when finger is moved from left to right and LED3 brightness increases when finger is moved from bottom to up on the touchpad.

The MOSI pin of the SPI slave peripheral is used to transfer data to the three serially connected LEDs for controlling color, brightness, and ON or OFF operation. The three LEDs form a daisy-chain connection and the communication happens over the serial interface to create an RGB configuration. The LED accepts a 8-bit input code, with three bytes for red, green, and blue color, five bits for global brightness, and three blank '1' bits. See the [LED datasheet](https://media.digikey.com/pdf/Data%20Sheets/Everlight%20PDFs/12-23C_RSGHBHW-5V01_2C_Rev4_12-17-18.pdf) for more details.

#### Set up the VDDA supply voltage in device configurator

1. Open Device configurator from the Quick Panel.

2. Go to the **Systems** tab, select the **Power** resource, and set the VDDA value under **Operating Conditions** as shown in **Figure 24**.

   **Figure 25. Setting the VDDA supply in the system tab of device configurator**

   <img src="images/vdda-settings.png" alt="" width="800"/>

### Resources and settings

See the [Operation](#operation) section for step-by-step instructions to configure the CAPSENSE&trade; configurator.

**Figure 26. Device configurator - EZI2C peripheral parameters**

<img src="images/ezi2c_config.png" alt="" width="600"/>

**Figure 27. SPI settings**

<img src="images/spi-settings.png" alt="" width="600"/>

**Table 5. Application resources**

The following ModusToolbox&trade; resources are used in this example:

| Resource  |  Alias/object     |    Purpose     |
| :------- | :------------    | :------------ |
| SCB (I2C) (PDL) | CYBSP_EZI2C          | EZI2C slave driver to communicate with CAPSENSE&trade; tuner GUI |
| CAPSENSE&trade; | CYBSP_MSCLP0 | CAPSENSE&trade; driver to interact with the MSCLP hardware and interface the CAPSENSE&trade; sensors |
| Digital pin | CYBSP_USER_LED | To visualise the touchpad response |

### Firmware flow

**Figure 28. Firmware flowchart**

<img src="images/firmware_flow.png" alt="" width="400"/>

## Related resources

Resources  | Links
-----------|----------------------------------
Application notes  | [AN79953](https://www.infineon.com/AN79953) - Getting started with PSoC&trade; 4 <br> [AN85951](https://www.infineon.com/AN85951) - PSoC&trade; 4 and PSoC&trade; 6 MCU CAPSENSE&trade; design guide <br> [AN234231](https://www.infineon.com/AN234231) - Achieving lowest-power capacitive sensing with PSoC&trade; 4000T
Code examples | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub 
Device documentation | [PSoC&trade; 6 MCU datasheets](https://www.infineon.com/cms/en/search.html#!view=downloads&term=PSoC%206&doc_group=Data%20Sheet) <br>[PSoC&trade; 6 technical reference manuals](https://www.infineon.com/cms/en/search.html#!view=downloads&term=PSoC%206&doc_group=Additional%20Technical%20Information)
Development kits | Select your kits from the [evaluation board finder](https://www.infineon.com/cms/en/design-support/finder-selection-tools/product-finder/evaluation-board) page.
Libraries on GitHub  | [mtb-hal-cat2](https://github.com/Infineon/mtb-hal-cat2) - Hardware abstraction layer (HAL) library
Middleware on GitHub | [CAPSENSE&trade;](https://github.com/Infineon/capsense) - CAPSENSE&trade; library and documents <br>
Tools | [Eclipse IDE for ModusToolbox&trade; software](https://www.infineon.com/cms/en/design-support/tools/sdk/modustoolbox-software/) - ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon&reg; MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems using AIROC&trade; Wi-Fi and Bluetooth® connectivity devices.

<br>

## Other resources

Infineon provides a wealth of data at www.infineon.com to help you select the right device, and quickly and effectively integrate it into your design.

## Document history

Document title: *CE235339* - *PSoC&trade; 4: MSCLP multi-touch mutual-capacitance touchpad tuning*

 Version | Description of change
 ------- | ---------------------
 1.0.0   | New code example. <br /> This version is not backward compatible with ModusToolbox&trade; software v2.4.
 1.0.1   | Project dependency update. 


-------------------------------------------------------------------------------

© Cypress Semiconductor Corporation, 2022. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates (“Cypress”).  This document, including any software or firmware included or referenced in this document (“Software”), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress’s patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br>
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product.  CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, “Security Breach”).  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications.  To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document.  Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  “High-Risk Device” means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  “Critical Component” means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device.  You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device.  Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress’s published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br>
Cypress, the Cypress logo, and combinations thereof, WICED, ModusToolbox, PSoC, CapSense, EZ-USB, F-RAM, and Traveo are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit cypress.com. Other names and brands may be claimed as property of their respective owners.
