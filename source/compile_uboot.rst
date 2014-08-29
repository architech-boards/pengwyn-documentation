
Compile U-Boot, MLO and Kernel
------------------------------

This document covers the general use of U-Boot v2012.10 and the AMSDK on the  following platforms:

am335x EVM
am335x EVM-SK
Pengwyn

Before starting to build the projects open a terminal (ctrl + alt + t)  and go to the root folder of the SDK Sitara::

  cd ti-sdk-am335x-evm-05.06.00.00

Type "cd ti-", and press the "tab" key for autocompletion. Create a folder to copy once completed system images.::

  cd board-support

In this folder you will find the projects that we're going to compile.::
  
  mkdir built-images 

This folder will be used as destination for the built images.

Build U-Boot & MLO
^^^^^^^^^^^^^^^^^^

Now go into the project U-Boot::

  cd u-boot-2012.10-psp05.06.00.00

As TI is suggesting,  we, as well, recommend keeping the object files separated when building. You can do this using the following option parameter when invoking the make command:: 
  
  O = object-directory

Where "object-directory" is the name of a folder you created for this purpose with::

  mkdir object-directory

You can now compile the bootloader with the following commands::

  rm -rf ./object-directory
  export PATH="/home/pengwyn/ti-sdk-am335x-evm-05.06.00.00/linux-devkit/bin:$PATH"
  make O=object-directory CROSS_COMPILE=arm-arago-linux-gnueabi- ARCH=arm pengwyn

When the compilation ends you will find the bootloader files in the directory of the object files:

- u-boot.img
- MLO

Copy these files to built-images folder::
  
  cp MLO ../../built-images
  cp u-boot.img ../../built-images

Build the Kernel
^^^^^^^^^^^^^^^^

.. image:: /_static/tux.*
   :align: left

From ti-sdk-am335x-evm-05.06.00.00 directory, go to the folder for the development of the operating system::

  cd board-support

In this folder there are the projects t we're going to compile. Now go into the Kernel::

  cd linux-3.2.0-psp05.06.00.08
  export PATH="/home/pengwyn/ti-sdk-am335x-evm-05.06.00.00/linux-devkit/bin:$PATH"
  make ARCH=arm CROSS_COMPILE=arm-arago-linux-gnueabi- uImage

When compilation finish do::
  
  cd arch/arm/boot

There you will find the compiled kernel “uImage”, copy it to the folder you created previously (built-images)::

  cp uImage /home/pengwyn/ti-sdk-am335x-evm-05.06.00.00/board-support/built-images    

You do not need to copy the driver modules to the file system because the compiled kernel already includes them. 






