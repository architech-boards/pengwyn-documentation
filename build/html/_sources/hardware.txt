Hardware
========

**Jumper settings**

+--------------------+---------------------------------------+
|                    |            boot sequence              |
+------+------+------+---------+---------+---------+---------+
|  J1  |  J2  |  J3  |   1st   |   2nd   |   3rd   |   4th   |
+======+======+======+=========+=========+=========+=========+
| open | open | open |  MMC0   |  SPI0   |  UART0  |  USB0   |
+------+------+------+---------+---------+---------+---------+
| open | open |close |  EMAC1  |  MMC0   | XIP MUX2|  NAND   |
+------+------+------+---------+---------+---------+---------+
| open |close | open | Fast ext|  EMAC1  |  UART0  |Reserved |
+------+------+------+---------+---------+---------+---------+
| open |close |close |  UART0  |  EMAC1  |Reserved |Reserved |
+------+------+------+---------+---------+---------+---------+
|close | open | open |  NAND   | NANDI2C |  MMC0   |  UART0  |
+------+------+------+---------+---------+---------+---------+
|close | open |close |  UART0  |  SPI0   | XIP MUX2|  MMC0   |
+------+------+------+---------+---------+---------+---------+
|close |close | open | XIP MUX2|  UART0  |  SPI0   |  MMC0   |
+------+------+------+---------+---------+---------+---------+
|close |close |close |  USB0   |  NAND   |  SPI0   |  MMC0   |
+------+------+------+---------+---------+---------+---------+

The hardware documentation of Pengwyn can be found here:

`http://downloads.architechboards.com/doc/Pengwyn/download.html <http://downloads.architechboards.com/doc/Pengwyn/download.html>`_
