U-boot
======

This chapter explains how to compile the u-boot.

Get the sources
---------------

The bootloader used by Pengwyn board is **U-Boot**. If you need to modify the bootloader or
to recompile it you have two ways to get the sources:

* use the sources you find in Yocto build directory after having compiled at least once a yocto image, or
* download the official u-boot release, than patch it with the BSP patches for Pengwyn board.

Anyway, we will assume in this guide that u-boot sources will be copied to:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'bootloader_rst-host-71' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="bootloader_rst-host-71" class="language-markup">/home/architech/Documents/u-boot</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

and such directory does not yet exists on your PC.
Of course, you are free to choose the path you like the most for u-boot sources, just remember
to replace the path used in this guide with your custom path.
So, where can we get the sources?

1. From Yocto sources

The first way is based on the sources set up by the Yocto build system. However, it is never
advisable to work with the sources in the Yocto build directory, if you really want to modify
the source code inside the Yocto environment we strongly suggest to refer to the official Yocto
documentation. To avoid messing up Yocto recipes and installation, it is desirable to copy the
patched u-boot sources you find in the build directory elsewhere. The directory we are talking
about is this one:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'bootloader_rst-host-72' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="bootloader_rst-host-72" class="language-markup">/home/architech/architech_sdk/architech/pengwyn/yocto/build/tmp/work/pengwyn-poky-linux-gnueabi/u-boot-ti-staging/2014.07-r7+gitrAUTOINC+7e537bfdd2/git/</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Replace:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'bootloader_rst-host-73' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="bootloader_rst-host-73" class="language-markup">/home/architech/architech_sdk/architech/pengwyn/yocto/build/</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

all over this chapter with your custom build directory path if you are not working with the default SDK 
build directory.

2. From the official u-boot release

The second way is to get the official U-Boot sources and patch them with Pengwyn BSP patches.
Pengwyn board uses U-Boot version 2014.07, which can be downloaded from:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'bootloader_rst-host-74' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="bootloader_rst-host-74" class="language-markup">cd /home/architech/Documents
 git clone -b ti-u-boot-2014.07 git://git.ti.com/ti-u-boot/ti-u-boot.git
 mv ti-u-boot u-boot
 cd u-boot
 git checkout 7e537bfdd261bf8bf444f3ac4d1be3db4ee124e8</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Build U-boot
------------

Patches are in the Yocto meta-layer **meta-pengwyn**. You can use them right away if you are working with the SDK:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'bootloader_rst-host-75' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="bootloader_rst-host-75" class="language-markup">patch -p1 -d /home/architech/Documents/u-boot/ &lt; /home/architech/architech_sdk/architech/pengwyn/yocto/meta-pengwyn/recipes-bsp/u-boot/u-boot-ti-staging-2014.07/0001-pengwyn.patch</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

However, if you are not working with the official SDK the most general solution to check them out and patch the sources is:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'bootloader_rst-host-76' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="bootloader_rst-host-76" class="language-markup">cd /home/architech/Documents
 git clone -b dizzy https://github.com/architech-boards/meta-pengwyn.git
 patch -p1 -d /home/architech/Documents/u-boot &lt; /home/architech/Documents/meta-pengwyn/recipes-bsp/u-boot/u-boot-ti-staging-2014.07/0001-pengwyn.patch</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Configuration and board files for Pengwyn board are in:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'bootloader_rst-host-77' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="bootloader_rst-host-77" class="language-markup">/home/architech/Documents/u-boot/board/ti/am335x/*
 /home/architech/Documents/u-boot/include/configs/pengwyn.h</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Suppose you modified something and you wanted to recompile the sources to test your patches, well, you
need a cross-toolchain. To use it to compile the bootloader or the operating system kernel run:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'bootloader_rst-host-78' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="bootloader_rst-host-78" class="language-markup">source /home/architech/architech_sdk/architech/pengwyn/toolchain/environment-nofs</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

then you can run these commands to compile it:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'bootloader_rst-host-79' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="bootloader_rst-host-79" class="language-markup">cd /home/architech/Documents/u-boot/
 make pengwyn_config
 make -j &lt;2 * number of processor's cores&gt; pengwyn</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Once the build process completes, you can find *u-boot.img* and *MLO* file inside directory */home/architech/Documents/u-boot*.
