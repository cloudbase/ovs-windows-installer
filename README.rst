Open vSwitch Windows installer
==============================

This project generates a MSI installer for Open vSwitch on Windows, including
CLI executables, services and the Hyper-V vswitch forwarding extension.

Requirements
------------

Visual Studio 2013 community, professional, premium or ultimate edition
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Visual Studio Community 2013 is freely available at:
https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx

WiX Toolset 3.9
^^^^^^^^^^^^^^^

Download and install from:
http://wixtoolset.org/releases/v3.9/stable

Microsoft_VC120_CRT_x86.msm
^^^^^^^^^^^^^^^^^^^^^^^^^^^

This Windows merge module is available with Visual Studio and contains the
Visual C++ 2013 x86 runtime redistributables files.
Copy the file in the *Redist* directory.

Open vSwitch binaries
---------------------

Build the Open vSwitch project and copy:

* *ovs-vswitchd.exe*, *ovsdb-server.exe*, *OVS.psm1* and *vswitch.ovsschema* in the
  *Services* directory
* *openvswitch.sys*, *openvswitch.cat* and *openvswitch.inf* in the *Driver*
  directory
* CLI executables and depending DLLs in the *Binaries* directory 
* PDB symbols in the *Symbols* directory

Note: the kernel driver needs to be signed.

Build instructions
------------------

Build the solution in the Visual Studio IDE or via command line:
   
    msbuild ovs-windows-installer.sln /p:Platform=x86 /p:Configuration=Release

Silent installation
-------------------

    msiexec /i OpenvSwitch.msi ADDLOCAL=OpenvSwitchCLI,OpenvSwitchDriver /l*v log.txt
