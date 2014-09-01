.. _nfs:

How to configure Minicom
========================

.. index:: Minicom

.. _usbSerial:

Usb-Serial
----------

On your Host Operating System (not on guest operating system running with the Virtual Machine) you need to have a serial communication program like minicom (for Linux as host operating systems) or HyperTerminal (for Windows as host operating system). In this document only the setup of minicom program will be treated. 

The required steps to get the usb-serial link work are:

1. clean the kernel messages buffer with the following command:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'remote_rst-host-21' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="remote_rst-host-21" class="language-markup">sudo dmesg -c</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

2. connect the Pengwyn board to the PC with mini-USB cable near DVI connector.

3. determine the serial device name with this command:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'remote_rst-host-22' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="remote_rst-host-22" class="language-markup">dmesg | grep ttyUSB</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

on the standard output you will see something like:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'remote_rst-host-23' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="remote_rst-host-23" class="language-markup">[11401.006607] usb 1-1.1: FTDI USB Serial Device converter now attached to ttyUSB0</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

In such an example, ttyUSB0 is the serial device name, and /dev/ttyUSB0 is the serial device

3. run command (sudo password is **architech**)

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'remote_rst-host-24' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="remote_rst-host-24" class="language-markup">sudo minicom -w -s</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

4. select *select port setup* and press enter.

5. setup the port with the following configuration:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'remote_rst-host-25' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="remote_rst-host-25" class="language-markup">A -    Serial Device      : /dev/ttyUSB0
 B - Lockfile Location     : /var/lock
 C -   Callin Program      :
 D -  Callout Program      :
 E -    Bps/Par/Bits       : 115200 8N1
 F - Hardware Flow Control : No
 G - Software Flow Control : No</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

6. once you are done configuring the serial port, you are back to minicom main menu and you can select *exit*.

7. Control that the SD card is in the slot of Pengwyn board if is in it, you can press the reset button.

8. if everything has been properly configured, the target board will boot and finally, the login will appear:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'remote_rst-board-141' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="remote_rst-board-141" class="language-markup">Yocto (Built by Poky 7.0.1) 1.2.1
 ttyO0
 
 pengwyn login:</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Login with username root, no password is required.
