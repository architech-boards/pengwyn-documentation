.. _kernel_page: 

How to customize the Linux Kernel
=================================

From menuconfig
---------------

The most frequent way of customization of the Linux Kernel is to change the .config file that contains the Kernel options. Setup the environment and run:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-91' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-91" class="language-markup">~/architech_sdk/architech/pengwyn/yocto/build$ bitbake linux-pengwyn -c cleanall
 ...
 ~/architech_sdk/architech/pengwyn/yocto/build$ bitbake linux-pengwyn -c menuconfig
 ...</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

a new window, like the following one, will pop-up

.. image:: _static/menuconfig.png

follow the instructions, save and exit, than you ready to generate your preferred image based on your customized kernel. If you prefer, you can build just the kernel running:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-92' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-92" class="language-markup">~/architech_sdk/architech/pengwyn/yocto/build$ bitbake linux-pengwyn
 
 ...</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

At the end of the build process, the output file (uImage.bin), along with the built kernel modules (modules-3.2.0-r0-pengwyn.tgz), will be placed under *tmp/deploy/images/* inside your build directory, so, if you are building your system from the default directory, the destination directory will be */home/architech/architech_sdk/architech/pengwyn/yocto/build/tmp/deploy/images*.

From sources
------------

If you want to modify the Linux kernel sources instead, insert the following commands to create an image of the actual used sources:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-93' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-93" class="language-markup">~$ mkdir -p /home/architech/Documents/linux-kernel
 ~$ cd /home/architech/Documents/linux-kernel
 ~/Documents/linux-kernel$ cp /home/architech/architech_sdk/architech/pengwyn/yocto/poky/meta-silica/recipes-kernel/linux/linux-pengwyn-3.2/linux-pengwyn* .
 ~/Documents/linux-kernel$ tar -xzf linux-pengwyn_3.2.tar.gz
 ~/Documents/linux-kernel$ mv linux-pengwyn_3.2 a
 ~/Documents/linux-kernel$ patch -p1 -d a/ &lt; linux-pengwyn_3.2.patch
 patching file ...
 ...
 ~/Documents/linux-kernel$ cp -r a/ b/</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Modify the sources contained inside directory **b**, than create your patch

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-94' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-94" class="language-markup">~/Documents/linux-kernel$ diff -Naur a/ b/ &gt; linux-pengwyn_3.2.mine.patch
 ~/Documents/linux-kernel$ cp linux-pengwyn_3.2.mine.patch /home/architech/architech_sdk/architech/pengwyn/yocto/poky/meta-silica/recipes-kernel/linux/linux-pengwyn-3.2/</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Create a file named *linux-pengwyn_3.2.bbappend* inside directory */home/architech/architech_sdk/architech/pengwyn/yocto/poky/meta-silica/recipes-kernel/linux/* and write the following text inside the .bbappend file:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-95' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-95" class="language-markup">SRC_URI += "file://linux-pengwyn_3.2.mine.patch \
 "</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Clean and build:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-96' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-96" class="language-markup">bitbake linux-pengwyn -c cleanall
 bitbake linux-pengwyn</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Building kernel without bitbake
-------------------------------

The following commands are used to build the kernel without bitbake. First of all, install the package uboot-mkimage:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-97' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-97" class="language-markup">apt-get install uboot-mkimage</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>


and setup the environment:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-98' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-98" class="language-markup">export PATH="$PATH:/opt/poky/1.2.1/sysroots/i686-pokysdk-linux/usr/bin/armv5te-poky-linux-gnueabi"</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

After that, in linux kernel folder, set the kernel options:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-99' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-99" class="language-markup">make ARCH=arm CROSS_COMPILE=arm-poky-linux-gnueabi- menuconfig</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

and build the kernel:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-910' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-910" class="language-markup">make ARCH=arm CROSS_COMPILE=arm-poky-linux-gnueabi- uImage</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

It is not necessary using *make clean* to rebuild the kernel image after have modified source code.

.. note::

 Use option -j with make to speed up the compilation

 -j [jobs], --jobs[=jobs]
            Specifies  the number of jobs (commands) to run simultaneously.  If there is more than one -j option, the last one is effective.  If the -j option is given without
            an argument, make will not limit the number of jobs that can run simultaneously.

 example: make -j 4 ARCH=arm CROSS_COMPILE=arm-poky-linux-gnueabi- uImage