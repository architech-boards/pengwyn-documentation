
Connect host PC to Pengwyn board
--------------------------------

For connecting the board click the icon “set local ip and install USBserial” and push  “Run in Terminal” button. Enter the password: pengwyn.

.. image:: /_static/connecthost1.png

This script will set the IP address of the host pc to 192.168.0.20 and it will enable USB connection. 

To check the configuration is correct use these commands::

  ls /dev/ttyUSB*
  ifconfig eth0

If all is ok you will see:

.. image:: /_static/connecthost2.png

Open a terminal (ctrl + alt + t) and open Minicom with the following options::

  minicom -w -s 

If all works correctly you will se this screen:

.. image:: /_static/connecthost4.png

Reset the board with the reset button on the board, located near the sd-card slot. You will see the startup of the Pengwyn on the terminal.

At login insert: root and press enter. 

.. image:: /_static/connecthost3.png

Configure the IP address with the command::

  ifconfig eth0 192.168.0.101

Now the connection is completed.
