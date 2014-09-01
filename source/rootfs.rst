Root FS
=======

By default, Pengwyn's Yocto/OpenEmbedded SDK will generate an image *<name image>.tar.gz*:

The *.tar.gz* file can be flattened out in your final medium partition (on SD card, flash memory) or on your host development system and used for build purposes with the Yocto Project.

If you want use a new SD card to unpack your image .tar.gz then read the following section else skip it.

.. include:: sdcard.rst

| 
| When you build a new file system you can delete everything contained on the second partition and you can untar file *.tar.gz* to the second partition on the SD card.
| If you have built a new kernel just overwrite the old one on the first partition.

After a writing operation use always *sync* command to make sure everything has been really written to the SD card:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'rootfs_rst-host-51' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="rootfs_rst-host-51" class="language-markup">sync</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>
