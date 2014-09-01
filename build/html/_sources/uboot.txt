.. _uboot:

How to customize u-boot
=======================

To customize **u-boot** you need to modify the sources. First of all, you need to have two different directories, one that contains the exact sources that poky uses to build the system, and another one with your modifications. To explain how to setup those two directories, hereafter will be assumed that you will work inside directory *~/Documents*. Open the terminal, than type:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'uboot_rst-host-41' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="uboot_rst-host-41" class="language-markup">~/Documents$ mkdir /home/architech/Documents/u-boot-configuration
 ~/Documents$ cd /home/architech/Documents/u-boot-configuration
 ~/Documents/u-boot-configuration$ cp ../../architech_sdk/architech/pengwyn/yocto/poky/meta-silica/recipes-bsp/u-boot/u-boot-pengwyn-2013.01/* .
 ~/Documents/u-boot-configuration$ tar -xzf u-boot-pengwyn-2013.01.tar.gz
 ~/Documents/u-boot-configuration$ mv u-boot-pengwyn-2013.01 a
 ~/Documents/u-boot-configuration$ patch -p1 -d a/ &lt; u-boot-pengwyn-2013.01.patch
 patching file arch/arm/cpu/armv7/am33xx/board.c
 patching file arch/arm/include/asm/arch-am33xx/cpu.h
 patching file arch/arm/include/asm/arch-am33xx/omap_gpmc.h
 patching file board/silica/pengwyn/Makefile
 patching file board/silica/pengwyn/mux.c
 patching file boards.cfg
 patching file common/miiphyutil.c
 patching file common/spl/spl_nand.c
 patching file drivers/mtd/nand/nand_base.c
 patching file drivers/mtd/nand/nand_bbt.c
 patching file drivers/mtd/nand/nand_ids.c
 patching file drivers/mtd/nand/omap_gpmc.c
 patching file drivers/net/cpsw.c
 patching file drivers/net/phy/Makefile
 patching file drivers/net/phy/phy.c
 patching file drivers/net/phy/ti.c
 patching file include/configs/pengwyn.h
 patching file include/linux/mtd/mtd-abi.h
 ~/Documents/u-boot-configuration$ cp -r a/ b/</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Directory *b* contains the sources that you can modify. Typically, you will want to modify u-boot settings, in which case you should edit file *~/Documents/u-boot-configuration/* **b** */include/configs/pengwyn.h* with your preferred editor. When you are done with your modifications, type:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'uboot_rst-host-42' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="uboot_rst-host-42" class="language-markup">~/Documents/u-boot-configuration$ diff -Naur a/ b/ &gt; u-boot-pengwyn-2013.01.mine.patch
 ~/Documents/u-boot-configuration$ cp u-boot-pengwyn-2013.01.mine.patch /home/architech/architech_sdk/architech/pengwyn/yocto/poky/meta-silica/recipes-bsp/u-boot/u-boot-pengwyn-2013.01/</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Create a file named *u-boot-pengwyn_2013.01.bbappend* inside directory */home/architech/architech_sdk/architech/pengwyn/yocto/poky/meta-silica/recipes-bsp/u-boot/* and write the following text inside the .bbappend file:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'uboot_rst-host-43' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="uboot_rst-host-43" class="language-markup">SRC_URI += "file://u-boot-pengwyn-2013.01.mine.patch \
 "</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

You are now ready to build (actually, rebuild) your customized version of u-boot:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'uboot_rst-host-44' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="uboot_rst-host-44" class="language-markup">~/architech_sdk/architech/pengwyn/yocto/build$ bitbake u-boot-pengwyn -c cleanall
 ...
 ~/architech_sdk/architech/pengwyn/yocto/build$ bitbake u-boot-pengwyn</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Once the build process finished, the output files (MLO and u-boot-pengwyn.img) will be placed under *tmp/deploy/images/* inside your build directory, so, if you are building your system from the default directory, the destination directory will be */home/architech/architech_sdk/architech/pengwyn/yocto/build/tmp/deploy/images*.


Build u-boot without bitbake
----------------------------

Set the enviroment with following command:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'uboot_rst-host-45' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="uboot_rst-host-45" class="language-markup">export PATH="$PATH:/opt/poky/1.2.1/sysroots/i686-pokysdk-linux/usr/bin/armv5te-poky-linux-gnueabi"</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Go in u-boot folder and launch these commands to build:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'uboot_rst-host-46' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="uboot_rst-host-46" class="language-markup">make ARCH=arm CROSS_COMPILE=arm-poky-linux-gnueabi- pengwyn_config
 make ARCH=arm CROSS_COMPILE=arm-poky-linux-gnueabi-</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>
