Touch Screen
============

This procedure will guide you to the installation of the display on the Pengwyn board and the configuration of the software to test it.

.. image:: _static/display-1.png

Installing the board
--------------------

1. switch off the board

2. connect display

.. image:: _static/display-2.png

3. switch on the board without SD card


Installing the software
-----------------------

If you don't have a SD card formatted with 2 partitions, one for the boot and one for the root filesystem, create it as in :ref:`Deploy <quick_deploy_rootfs_label>`. Now we want install in rootfs the qt4e-demo-image-pengwyn.tar.gz image.

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'video_rst-host-21' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="video_rst-host-21" class="language-markup">sudo tar -zxf ~/architech_sdk/architech/pengwyn/yocto/tmp/deploy/images/pengwyn/qt4e-demo-image-pengwyn.tar.gz -C /path/to/sdcard/rootfs</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

And substitute the pengwyn.dtb with this one:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'video_rst-host-22' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="video_rst-host-22" class="language-markup">sudo cp ~/architech_sdk/architech/pengwyn/yocto/tmp/deploy/images/pengwyn/zImage-pengwyn-touch.dtb /path/to/sdcard/boot/pengwyn.dtb</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Make sure everything has been really written to the SD card:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'video_rst-host-23' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="video_rst-host-23" class="language-markup">sync</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Then insert SD card on Pengwyn board and wait Linux start-up. First time, **the touch screen calibration is needed**, than qt4 demo will start.
