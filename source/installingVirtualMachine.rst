
Installing Virtual Machine
--------------------------
The development environment is provided as a Virtual Machine image. 

To be able to start it you need first to install VirtualBox. Image has been created with VirtualBox version 4.2.6. 

.. image:: /_static/virtualboxlogo.png
   :align: left

Go to:

https://www.virtualbox.org/wiki/Downloads

and download the version for Windows. You need also to download the Extension Pack.

.. important::
   Make sure that the extension pack has the same version of virtual box.

Install the software with all the default options.

Launch the program and follow the following steps: 

.. tip::
   If you are using Linux click directly on .ova file and skip to point 3.

1. On the menu select: *File → Import Appliance*

.. image:: /_static/importAppliance.png

2. Click on “Open appliance…” button and select the iso file “PengwynSDK.ova”.

3. After opening the appliance, click on “Shared Folders” and select a folder to share with Windows.

.. image:: /_static/vbSharedFolders.png

4. If the host PC has only 1GB RAM go to "machine -> settings" menu and click on "System" tab and change RAM to 512MB.

.. image:: /_static/ivs.png

5. The ethernet card must be attached the LAN not the WLAN. To set the correct card, go to menu "machine -> Settings".
   Click on "Network" tab and select your LAN card. Click Ok button to apply your choice.

.. image:: /_static/ivs2.png

6. Click the icon "Start" button on the toolbar.

.. image:: /_static/vbStart.png

7. Every time you connect the mini-USB from the PC to the card. On menu click *Device → USB Devices → FTDI*.

.. image:: /_static/vbUSB.png

8. The default keyboard is set to USA layout.

   If your keyboard layout is different, to change it, from the menu of Ubuntu:

   go to "System -> preferences -> keyboard".

   Select "Layout" tab.

   Click on "Add..." button.

   .. image:: /_static/ivs3.png

   Select your keyboard layout and press "add" button. Then select "USA" and click "Remove Button".

   .. image:: /_static/ivs4.png

   Press "Close" button.

9. Open a terminal (ctrl + alt + t) and type the following command::

     sudo usermod –a –G vboxsf pengwyn

   User name is **pengwyn**, password is **pengwyn**.


Ubuntu will be launched with the Sitara SDK integrated ready to be used. No installation or other configuration is required.
