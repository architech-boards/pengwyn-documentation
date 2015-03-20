Meta Layer
==========

A Yocto/OpenEmbedded meta-layer is a directory that contains recipes, configuration files, patches, etc., all needed by
*Bitbake* to properly "see" and build a BSP, a distribution, a (set of) package(s), whatever.
**meta-pengwyn** is a meta-layer which defines the customizations to make to TI's AM335x BSP and Yocto/OpenEmbedded
in order to get a working system, tailor made of Pengwyn.

You can get it with *git*:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'meta_layer_rst-host-191' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="meta_layer_rst-host-191" class="language-markup">git clone -b dizzy https://github.com/architech-boards/meta-pengwyn.git</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

The machine name for Pengwyn is **pengwyn**.

The strictly BSP related recipes are located under:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'meta_layer_rst-host-192' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="meta_layer_rst-host-192" class="language-markup">meta-pengwyn/recipes-bsp/u-boot/
 meta-pengwyn/recipes-bsp/flash/
 meta-pengwyn/recipes-kernel/linux/</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

The other recipes are there just to customize other aspects of the system or to offer some facility to help you easily
manage some task, for example, working with flash memory or partitions.

Pengwyn is powered by a NAND memory, big enough to place a full featured root file system inside of it.
However, you might not be interested in how to place the file system inside of it from the beginning and how to mount and
unmount it inside your file system.
There is a recipe inside meta-pengwyn, **pengwyn-flash-utils**, that will install three scripts inside the target file system
to make the aforementioned tasks easy:

* *pengwyn_to_flash*

* *pengwyn_mount_flash*

* *pengwyn_umount_flash*

*pengwyn_to_flash* takes as input files, cleans and formats the NAND flash memory, and finally takes the files you gave
him to setup the file system. For more information just run:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'meta_layer_rst-host-193' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="meta_layer_rst-host-193" class="language-markup">pengwyn_to_flash -h</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

from Pengwyn shell.

*pengwyn_mount_flash* lets you mount the flash memory partition inside your filesystem (under */mnt/flash*) without any effort
and, likewise, *pengwyn_umount_flash* helps you unmounting the partition.

Remember that to install those scripts inside the target, you need to add **meta-openmbedded/meta-oe** meta layer to your *bblayers.conf* file. If you are working with Architech virtual machine, you don't have to worry about that, everything is already in place.

*pengwyn-flash-utils* won't be placed by default inside your file system, if you want it you need to add a line like this one
to your *local.conf* file

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'meta_layer_rst-host-194' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="meta_layer_rst-host-194" class="language-markup">IMAGE_INSTALL_append = " pengwyn-flash-utils"</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Probably the most comfortable way, at least at the beginning, to build a valid SD card is to use file *.sdcard* that
*Bitbake* emits when builds an image. However, *Bitbake* prepares a final iso image to write to the medium without any knowledge of its size. If you write the image on an SD card, for example, the first thing you notice is that the file system does not fit the card.
