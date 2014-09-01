Opkg Basics
===========

.. image:: _static/opkg.png
   :align: left

| 
| Opkg (Open PacKaGe Management) is a lightweight package management system. It is written in C and resembles apt/dpkg in operation. It is intended for use on embedded Linux devices and is used in this capacity in the OpenEmbedded and OpenWrt projects. 
| 
|

Useful commands:

- command to know what packages are installed on the file system:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-board-131' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-board-131" class="language-markup">opkg list-installed</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

- show where are the files installed of the packet:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-board-132' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-board-132" class="language-markup">opkg search name_packet</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

- show what packets depend on the “name_packet” package:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-board-133' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-board-133" class="language-markup">opkg whatdepends name_packet</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

- remove packages:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-board-134' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-board-134" class="language-markup">opkg remove name_packet</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

for this command there are important options:

1. This option will force the removal of the package but will leave any packages that depend on this package installed:

::

  -force-depends

2. This option will go up the dependency list and remove all packages in the dependency chain:

::

  -force-removal-of-dependent-packages 

- install the packages:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-board-135' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-board-135" class="language-markup">opkg install name_packet</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

How to add a repository
-----------------------

Install a web server in the virtual machine, e.g.:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-host-11' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-host-11" class="language-markup">sudo apt-get install apache2</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Copy the built packages inside the web server directory, e.g.:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-host-12' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-host-12" class="language-markup">sudo cp -r /home/architech/architech_sdk/pengwyn/yocto/build/tmp/deploy/ipk /var/www</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Create a file named *<something>.conf* (e.g. mine-repositories.conf) under */etc/opkg/* of the Pengwyn file system and fill it with the following lines:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-board-136' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-board-136" class="language-markup">src/gz arm     http://192.168.0.100/ipk/armv7a-vfp-neon
 src/gz all     http://192.168.0.100/ipk/all
 src/gz pengwyn http://192.168.0.100/ipk/pengwyn</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

.. note::

  192.168.0.100 is the server IP where there is the web server with repository

after that run the following command from Pengwyn's shell:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-board-137' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-board-137" class="language-markup">opkg update</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>


Now you are ready to download and install the packages from the network.

Tip
---

With "opkg list | wc -l" you can know approximately how many packets there are in repository

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-board-138' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-board-138" class="language-markup">opkg list | wc -l
 opkg update
 opkg list | wc -l</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

If the updating got success with the last command you see the number of packets incremented.

.. _update_package_index: 

How to update the repository in the vm
--------------------------------------

| Once you have builded a package by Hob, do you need update package index. To do this, run the following command from Pengwyn's shell.

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'opkg_rst-host-13' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="opkg_rst-host-13" class="language-markup">cd /home/architech/architech_sdk/architech/pengwyn/yocto
 source yocto/oe-init-build-env
 bitbake package-index
 opkg update</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>