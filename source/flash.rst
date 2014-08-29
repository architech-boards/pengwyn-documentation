
Pengwyn Flash Memory
====================

This section will explain how to transfer the data from the sd-card to flash memory of Pengwyn.

Before going on you must have executed all steps explained in "Connect host PC to Pengwyn board" section.
Minicom must work correctly.

1. Remove J1 jumper and insert SD-CARD with prebuilt file

.. image:: /_static/flash1.png

2. Reset with S1 button.

   At the beginning, when you see with Minicom that u-boot procedure starts, press any key to stop it.

.. image:: /_static/flash2.png

3. Erase and upload the FLASH memory with the commands::

     nand erase.chip
     run nandupdate

4. Reset board with S1 button. Start Linux operating system, at login enter user name:

   **root**

   the password is not required.

5. Create flash file system with the automated script::

     ./create_nand_fs.sh
     .. image:: /_static/flash3.png

6. Shutdown linux with the command::

     Shutdown –h now

7.	Remove SD-CARD, insert jumper in J1 and reset the board with S1 button

The system now will restart from NAND flash with new operating system.
