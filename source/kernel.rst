Linux Kernel
============

Like we saw for the :ref:`bootloader <bsp_bootloader_label>`, the first thing you need is: sources.
Get them from *Bitbake* build directory (if you built the kernel with it) or get them from the Internet.

*Bitbake* will place the sources under directory:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-121' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-121" class="language-markup">/path/to/build/tmp/work/pengwyn-poky-linux-gnueabi/sitara-linux-ti-staging/3.14.26-r22g+gitrAUTOINC+2489c022b2/git</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>


If you are working with the virtual machine, you will find them under directory:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-122' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-122" class="language-markup">/home/architech/architech_sdk/architech/pengwyn/yocto/build/tmp/work/pengwyn-poky-linux-gnueabi/sitara-linux-ti-staging/3.14.26-r22g+gitrAUTOINC++XXX/git</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

| XXX is a random code assigned by bitbake.
| We suggest you to **don't work under Bitbake build directory**, you will pay a speed penalty and you could have troubles syncronizing the all thing. Just copy them some place else and do what you have to do.

If you didn't build them already with *Bitbake* or you just want to do make every step by hand, you can
always get them from the Internet by cloning the proper repository and checking out the proper hash commit:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-123' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-123" class="language-markup">cd ~/Documents
 git clone -b sitara-ti-linux-3.14.y git://git.ti.com/sitara-linux/sitara-linux.git
 cd sitara-linux
 git checkout 2489c022b2932432606f897741a71b712e6dbe77</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>


and by properly patching the sources:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-124' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-124" class="language-markup">cd ~/Documents
 patch -p1 -d sitara-linux/ &lt; /home/architech/architech_sdk/architech/pengwyn/yocto/meta-pengwyn/recipes-kernel/linux/sitara-linux-ti-staging-3.14.26/0002-pengwyn.patch
 cp /home/architech/architech_sdk/architech/pengwyn/yocto/meta-pengwyn/recipes-kernel/linux/sitara-linux-ti-staging-3.14.26/defconfig ~/Documents/sitara-linux/arch/arm/configs/pengwyn_defconfig</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

However, if you are not working with the official SDK the most general solution to check them out and patch the sources is:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-125' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-125" class="language-markup">cd ~/Documents
 git clone -b dizzy https://github.com/architech-boards/meta-pengwyn.git
 git clone git://git.yoctoproject.org/meta-ti.git
 cd meta-ti
 git checkout 56ea9223d7a3d3da38dd4fef10b4dfeb0667992d
 patch -p1 -d sitara-linux/ &lt; meta-pengwyn/recipes-kernel/linux/sitara-linux-ti-staging-3.14.26/0002-pengwyn.patch
 cp meta-pengwyn/recipes-kernel/linux/sitara-linux-ti-staging-3.14.26/defconfig sitara-linux/arch/arm/configs/pengwyn_defconfig</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>


Now that you have the sources, you can start browsing the code from the following files:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-126' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-126" class="language-markup">~/Documents/sitara-linux/arch/arm/boot/dts/pengwyn-common.dtsi
 ~/Documents/sitara-linux/arch/arm/boot/dts/pengwyn-dvi.dts
 ~/Documents/sitara-linux/arch/arm/boot/dts/pengwyn-touch.dts</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

For build the kernel source the script to load the proper environment for the cross-toolchain:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-127' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-127" class="language-markup">source /home/architech/architech_sdk/architech/pengwyn/toolchain/environment-nofs</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-128' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-128" class="language-markup">cd ~/Documents/sitara-linux
 make pengwyn_defconfig
 make menuconfig</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

and to compile it:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-129' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-129" class="language-markup">make -j &lt;2 * number of processor's cores&gt; uImage</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

If you omit *-j* parameter, *make* will run one task after the other, if you specify it *make* will parallelize
the tasks execution while respecting the dependencies between them.
Generally, you will place a value for *-j* parameter corresponding to the double of your processor's cores number,
for example, on a quad core machine you will place *-j 8*.

Once the kernel is compiled, the last build to do is the dtb file. This file permits at the boot time to configure the kernel with a specific hardware configuration. So if you are using a touchscreen you will build the *pengwyn-touch.dts* file else if you are using a display with dvi connector will be *pengwyn-dvi.dts* file. In the same directory where you have compiled the kernel launch the command:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-1210' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-1210" class="language-markup">make pengwn-touch.dtb</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

or

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-1211' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-1211" class="language-markup">make pengwyn-dvi.dtb</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

By the end of the build process you will get *uImage* under *arch/arm/boot* and *pengwyn-touch.dtb* or *pengwyn-dvi.dtb* under *arch/arm/boot/dts* directories.
