
SDK Structure Overview
----------------------
At the start of the Ubuntu desktop, there are three icons:

- “set local ip and install USBserial”: sets the local IP 192.168.0.20 and enables serial connection to the board 
- Code Composer Studio v5: Eclipse based IDE used for both application & debug using gdbserver
- Link to ti-sdk-am335x-evm-05.06.00.00: link to the main directory that contains the Sitara Linux SDK

.. image:: /_static/vbDesktop.png

The Sitara SDK directory contains the code and tools used to develop for Sitara devices.

You will find the following folders:

.. image:: /_static/sdkFolders.png

**bin**: Contains the helper scripts for configuring the host system and target device. Most of these scripts are used by the setup.sh script.

**board-support**: Contains the SDK components that need to be modified when porting to a custom platform. This includes the kernel and boot loaders as well as any out of tree drivers.

**docs**: Contains various SDK documentation such as the software manifest and additional user's guide. This is also the location where you can find the training directory with the device training material.

**Example-applications**: Contains the sources of the  TI example applications, as seen during the out-of-box demonstration.

**filesystem**: Contains the reference file systems. These include the smaller base file system as well as the full-featured SDK file system.

**host-tools**: Contains the host side tools such as pinmux and flash tool.

**linux-devkit**: Contains the cross-compile toolchain and libraries to speed up the development for the target device. 
Graphics_SDK_setuplinux_<version>.bin: This is the installer for the graphics SDK. The graphics SDK components are used by the Sitara Linux SDK to provide additional demos and pre-built 
Qt libraries to accelerate various Qt functions.