# PSoC&trade; 4 MCU: Basic device firmware upgrade (DFU)

This example demonstrates how to create a field upgradable project for PSoC&trade; 4 using the DFU middleware.
The device firmware update (DFU) will be occuring over the I2C interfaces. This includes downloading an application from a host device (like PC) and installing it in PSoC&trade; 4 device flash.
 This document details the following:
1. A high-level overview of the DFU process described in [Design and Implementation](#design-and-implementation) section.

This example bundles two applications:

**Bootloader app:** Implements a DFU middleware library based basic bootloader run by the CPU. The bootloader handles image download, verification, erase and upgradation process. Whenever you hard reset (like POR) your device, this bootloader runs first and if there is a valid application image already, it jumps to the application instantly. To keep the control in the Bootloader, user have to issue a soft reset to keep it in the Bootloader mode. And if there is no valid application the control stays in the Bootloader ready to bootload an image.

**Blinky app:** This is a tiny application run by the CPU that blinks a LED at a 5-Hz rate continuously. This application transfers control to the bootloader when a user button is pressed, or an I2C command is sent. Here the application project is kept a simple Blinky project, but user can change according to their needs.


**Note:** This example supports only *I2C* for DFU transport currently.


## Requirements

- [ModusToolbox&trade; software](https://www.infineon.com/cms/en/design-support/tools/sdk/modustoolbox-software) v3.0 or later (tested with v3.0)
**Note:** This code example version requires ModusToolbox&trade; software version 3.0 and is not backward compatible with v2.4 or older versions.
- Board support package (BSP) minimum required version: 3.0.0
- Programming language: C

## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; embedded compiler v10.3.1 (`GCC_ARM`) - Default value of `TOOLCHAIN`
- Arm&reg; compiler v6.16 (`ARM`)
- IAR C/C++ compiler v9.30.1 (`IAR`)

## Design and implementation

### Overview

This example demonstrates the basic device firmware upgrade (DFU) operations based on the [DFU middleware library](https://github.com/Infineon/dfu).


### Bootloader implementation

This bootloader project implements an immutable bootloader with support for upgrading the application firmware over I2C.

The [DFU host tool](https://www.infineon.com/dgdlac/Infineon-ModusToolbox_Device_Firmware_Update_Host_Tool_%28Version_1.2%29-Software-v01_00-EN.pdf?fileId=8ac78c8c7d0d8da4017d0f8d42ba76bb) (typically running on the host PC) sends the application (*\<APPNAME>.cyacd2*) to the device. The bootloader receives the application image in chunks and overwrites the existing application image. See Figure 4 below. If a DFU session is interrupted, the application firmware will not be in a usable state. However, the device can still run the bootloader and perform necessary actions to download and install the application in subsequent DFU sessions.

**Figure 8. DFU design overview**  
      <img src="images/dfu-overwrite.png" alt="Figure_8" width="839"/>





### Software reset

When transferring control from one application to another, the recommended method is through a device software reset. This enables each application to initialize device hardware blocks and signal routing from a known state. It is possible to freeze the state of I/O pins so that they are maintained through a software reset. Defined portions of the SRAM are also maintained through a software reset. For more information, see the device-specific technical reference manual (TRM).



## Related resources


Resources  | Links
-----------|----------------------------------
Application notes  | [AN79953](https://www.infineon.com/AN79953) – Getting started with PSoC&trade; 4 <br>  
Code examples  | [Using ModusToolbox&trade; software](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub
Device documentation | [PSoC&trade; 4 MCU datasheets](https://edit.infineon.com/cms/en/search.html?intc=searchkwr-return&_ga=2.236871304.809459600.1667797660-717891995.1665054803#!view=downloads&term=PSOC4&doc_group=Data%20Sheet) <br> [PSoC&trade; 4 technical reference manuals](https://www.infineon.com/cms/en/search.html#!term=Psoc%204%20technical%20reference%20manual&view=all)
Development kits | Select your kits from the [Evaluation Board](https://www.infineon.com/cms/en/design-support/finder-selection-tools/product-finder/evaluation-board) Finder page.
Libraries on GitHub  | [mtb-pdl-cat2](https://github.com/Infineon/mtb-pdl-cat2) – PSoC&trade; 4 peripheral driver library (PDL)  <br> [mtb-hal-cat2](https://github.com/Infineon/mtb-hal-cat2) – Hardware abstraction layer (HAL) library
Middleware on GitHub  | [Device Firmware Update (DFU) Middleware Library](https://github.com/Infineon/dfu) – Links to DFU SDK middleware
Tools  | [Eclipse IDE for ModusToolbox&trade; software](https://www.infineon.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use software and tools enabling rapid development with Infineon MCUs, covering applications from embedded sense and control to wireless and cloud-connected systems using AIROC&trade; Wi-Fi and Bluetooth® connectivity devices.

<br>

## Other resources

Infineon provides a wealth of data at [www.infineon.com](www.infineon.com) to help you select the right device, and quickly and effectively integrate it into your design.



<br>

---------------------------------------------------------

© Cypress Semiconductor Corporation, 2022. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates ("Cypress").  This document, including any software or firmware included or referenced in this document ("Software"), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress’s patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br>
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product. CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, "Security Breach").  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications. To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document. Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  "High-Risk Device" means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  "Critical Component" means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device. You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device. Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress’s published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br>
Cypress, the Cypress logo, and combinations thereof, WICED, ModusToolbox, PSoC, CapSense, EZ-USB, F-RAM, and Traveo are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit cypress.com. Other names and brands may be claimed as property of their respective owners.