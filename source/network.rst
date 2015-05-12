Network
=======

Pengwyn networking is powered by TI's chip AM335x.
Under Linux, instead, the default network configuration is:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'network_rst-board-251' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="network_rst-board-251" class="language-markup">root@pengwyn:~# ifconfig
 eth0    Link encap:Ethernet  HWaddr 00:18:30:FD:2D:7E
         UP BROADCAST MULTICAST  MTU:1500  Metric:1
         RX packets:0 errors:0 dropped:0 overruns:0 frame:0
         TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
         collisions:0 txqueuelen:1000
         RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
         Interrupt:56
 
 lo      Link encap:Local Loopback
         inet addr:127.0.0.1  Mask:255.0.0.0
         UP LOOPBACK RUNNING  MTU:65536  Metric:1
         RX packets:0 errors:0 dropped:0 overruns:0 frame:0
         TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
         collisions:0 txqueuelen:0
         RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

If you want that configuration to be brought up at boot you can add a few line in file */etc/network/interfaces*, for
example, if you want *eth0* to have a fixed ip address (say 192.168.0.10) and MAC address of value 1e:ed:19:27:1a:b6
you could add the following lines:

.. raw:: html

 <div>
 <div><b class="admonition-board">&nbsp;&nbsp;Board&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'network_rst-board-252' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="network_rst-board-252" class="language-markup">auto eth0
 iface eth0 inet static
     address 192.168.0.10
     netmask 255.255.255.0
     hwaddress ether 1e:ed:19:27:1a:b6</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>
