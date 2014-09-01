FAQ
===

What is the password of user **architech**?
-------------------------------------------

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'faq_rst-host-101' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="faq_rst-host-101" class="language-markup">architech</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

What is **sudo**?
-----------------

**sudo** is a program for Unix-like computer operating systems that allows users to run programs/commands with the security privileges of another user, normally the superuser or root. Not all the users can call sudo, only the **sudoers**, **architech** user is a sudoer. When you run a command preceeded by sudo Linux will ask you the user password, for **architech** user the password is **architech**.

What is the password for user root?
-----------------------------------

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'faq_rst-host-102' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="faq_rst-host-102" class="language-markup">root</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

When should I use an external power supply?
-------------------------------------------

Pengwyn Board can be powered directly from the USB connector, the power consumption is about 250mA without any option installed. 
When powered from USB, the board can supply enough current to a USB keyboard (or a USB mouse) and to the DVI interface.
If you want to connect something more power hungry to the USB port, we suggest you to power the board with an external power supply or to use externally powered USB devices.

The first time I ran the virtual machine I obtained an error related to the Ethernet controller. What can I do?
---------------------------------------------------------------------------------------------------------------

We used a Realteck Ethernet controller when we built the virtual machine, if you have a different one is not a problem, click on **change network settings** and insert the proper configuration for your machine.

My build is taking too long, what can I do to optimize?
-------------------------------------------------------

Please, refer to:

* :ref:`hobSpeedup` Section of Chapter :ref:`howToUseHOB`, and/or
* :ref:`pokySpeedup` Section of Chapter :ref:`howToUsePoky`.

When I try to create the SD card something goes wrong, what can I do?
---------------------------------------------------------------------

The simplest reason could be that the SD card is write protected or locked, please double check that.

How do I enable commercially licensed recipes?
----------------------------------------------

Commercially licensed recipes are disabled by default.
Your conf/local.conf file, contained in your build directory (by default is /home/architech/architech_sdk/architech/pengwyn/yocto/build/), has a (commented) line starting with:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'faq_rst-host-103' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="faq_rst-host-103" class="language-markup"># LICENSE_FLAGS_WHITELIST</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

uncomment it (delete **#** symbol).

For the details, please refer to `the official Yocto Project documentation <http://www.yoctoproject.org/docs/1.2/poky-ref-manual/poky-ref-manual.html#enabling-commercially-licensed-recipes>`_.

How do i know which drivers are included?
-----------------------------------------
* If you have built an image then you can go in *~/architech_sdk/architech/pengwyn/yocto/build/tmp/work/pengwyn-poky-linux-gnueabi/linux-pengwyn-3.2-r0/linux-pengwyn_3.2/drivers*. In this directory there are all kernel linux drivers.

* If you haven't build an image then use following commands:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'faq_rst-host-104' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="faq_rst-host-104" class="language-markup">~$ mkdir -p /home/architech/Documents/linux-kernel
 ~$ cd /home/architech/Documents/linux-kernel
 ~/Documents/linux-kernel$ cp /home/architech/architech_sdk/architech/pengwyn/yocto/poky/meta-silica/recipes-kernel/linux/linux-pengwyn-3.2/linux-pengwyn* .
 ~/Documents/linux-kernel$ tar -xzf linux-pengwyn_3.2.tar.gz
 ~/Documents/linux-kernel$ patch -p1 -d linux-pengwyn_3.2 &lt; linux-pengwyn_3.2.patch
 patching file ...
 ~/Documents/linux-kernel$ cd linux-pengwyn_3.2/drivers</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

In this directory there are all kernel linux drivers.

* Another metod is using the *menuconfig* of linux. In *linux-pengwyn_3.2* directory use the command:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'faq_rst-host-105' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="faq_rst-host-105" class="language-markup">make menuconfig</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Once opened go in *Device Drivers*.

I have problems to create a patch for the kernel. How can I do that?
--------------------------------------------------------------------
If you have already built the kernel before modify it, you need purge all file objects. To do this use the following command:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'faq_rst-host-106' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="faq_rst-host-106" class="language-markup">make ARCH=arm mrproper</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

will cleanup totally the sources. See :ref:`kernel_page` for details.

How do I include QWebView widget in my project? The compilation fails
---------------------------------------------------------------------
Open your .pro project file and add a new line under *QT += core gui*:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'faq_rst-host-107' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="faq_rst-host-107" class="language-markup">QT += webkit</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

I have problems with internet connection
----------------------------------------
If yuor company uses proxy then read this page to configure correctly yocto:
`Working Behind a Network Proxy <https://wiki.yoctoproject.org/wiki/Working_Behind_a_Network_Proxy>`_.

I have builded a package but I do not see it in opkg list. Why?
---------------------------------------------------------------
Please, refer to :ref:`update_package_index`
