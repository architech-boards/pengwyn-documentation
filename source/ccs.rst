
Code Composer Studio V5
-----------------------

.. image:: /_static/ccslogo.png
   :align: left

Code Composer Studio v5 is currently provided with the Sitara Software Development Kit.

It is based on Eclipse IDE and includes the Remote System Explorer plug-in that enable access the remote target board. This software is already installed and configured in the SDK Pengwyn.

To launch it click the icon "Code Composer Studio v5" on the desktop and ap the Eclipse work environment will appear.

The active project is helloWorld, which we're going to compile and debug in this tutorial. 

The workspace used is located in:

/home/pengwyn/workspace_v5_1

The project helloWorld is already configured to work with CCS5. If you want create a new project quickly, use this project as template and modify the source code. 

From the menu, click View → Project Explorer: the left panel will show the projects available in the workspace. 

Open helloWold project and double-click on hello.c file. 

.. image:: /_static/ccs1.png

To build the project go to Project → Build All.

Go to Window → Open Perspective → Other... → Remote System Explorer to open the Remote System Explorer perspective.

.. image:: /_static/ccs2.png

If doesn't work check Ethernet connection (read “Connect host PC to Pengwyn board” paragraph).

Access Target File System
^^^^^^^^^^^^^^^^^^^^^^^^^

Expand the Root node under Sftp Files node. 

The remote system file tree should now show the root directory. You can navigate anywhere in the remote file system down to file level. 

Files can be dragged and dropped into the remote file tree.  A context menu allows you to create, rename or delete files and folders. 

The local file system on the Linux host can also be accessed by expanding the Local node.

Navigate to the /home/root/ folder on your target board.

.. image:: /_static/access_target1.png
 
Now we’ll copy our executable to this /home/root target location. First switch back to CCS Edit perspective using the upper right double arrow >> 

.. image:: /_static/access_target2.png

In Project explorer window, open the Debug group. Select the executable helloWorld.exe, R-click → copy. 

.. image:: /_static/access_target3.png

Switch to Remote System Explorer perspective using the upper right double arrow >>. In the Remote Systems window, R-click → paste will copy your executable to the Pengwyn /home/root directory.

.. image:: /_static/access_target4.png

SSH Terminal
^^^^^^^^^^^^
To open an SSH Terminal view: right click the Ssh Terminals node under the Remote System → my_pengwyn and select Launch Terminal from the context menu.

.. image:: /_static/ssh1.png
 
Type shell commands at the prompt in the terminal window.

Below is a sample command to print the current directory path and list its contents.

In the Console window, Print Working Directory confirm that the binary is there::

  ls -l

Before you can run your program, you need to make it executable::

  chmod 755 helloWorld.exe

Run your program::
  
  ./helloWorld.exe

.. image:: /_static/ssh2.png

Running the Debug Session
^^^^^^^^^^^^^^^^^^^^^^^^^
Each time you start the debugger, you must first start the gdbserver program on the target.

Start gdbserver for the helloWorld project with a port number of 10000 (this port number must match the number that was entered in the Debug Configuration).

At the target console command line, type::

  gdbserver :10000 ./helloWorld.exe

Once started, you should see a response similar to below:

.. image:: /_static/debug1.png

Go to Run → Debug Configurations, select “hello Debug” and click on Debug button

.. image:: /_static/debug2.png

CCS will change to the CCS Debug perspective. The debug panel will show the running threads and their status. The source code window will show the program halted at the first executable source code line in the main() function. 

.. image:: /_static/debug3.png

The Variables window will show the local variables and their current values.

Like any debug enviroment, you can use breakpoints, use the debugger Step Over and Step Into command icons to step through the source code. 

To resume program execution, click the run → resume menu item.

