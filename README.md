# VFP Installers

This repository contains installers for various components of Visual FoxPro (VFP).

## VFP 9

vfp9.iso is an ISO file created from the VFP 9 installation CD. To install VFP 9, download [vfp9.iso](https://vfpxrepository.com/files/vfp9.iso), double-click to open it in File Explorer, then run Setup.exe.

> Note: VFP 9 is not open source; you must have a license key to install it. This is provided as a convenience since most laptops no longer come with optical drives.
> To purchase VFP 9, see https://store.forwardthinkingsoftware.com/Catalog/Tools for North Americans (bundled with Visual Extend). For other continents, contact Rainer Becker: ++49-6173-950903, Fax ++49-6173-950904, http://www.visualextend.com/, bestellungen@dfpug.de. VFP 9 is also still included in MSDN Subscriptions from Microsoft.

## VFP 9 Service Pack 2 (SP2) and Hotfix 3

These are updates to VFP 9. Use the `VERSION()` command to assess your current version of VFP.

The **latest fully patched version of VFP 9** is

```
Visual FoxPro 09.00.0000.7423 for Windows
```

If your version is `09.00.0000.2412` then you don't have any service packs installed.

To upgrade VFP 9 to the latest service pack and hotfix, follow these steps.

### Step 1: Upgrade VFP 9 to Service Pack 2

If your version is `09.00.0000.5815` then you already have Service Pack 2 installed.  You can skip to the next step to install the latest hotfix.

Execute the file `VFP9_sp2.exe` to update the original release of VFP 9 to Service Pack 2.

The file `VFP9SP2_BugFixList.htm` lists the changes in SP2.

### Step 2: Upgrade VFP 9 SP2 to Hotfix 3 (the Latest Hotfix)

Execute `VFP90SP2-KB968409-ENU.exe` to extract files into a folder you will subsequently specify. Follow the instructions in the readme (in that folder) to copy the files to their correct locations.

### Step 3: Install MS XML4

Run MSXML.msi to install MS XML version 4, which is required by the Task Pane and the XMLAdapter class.

## Runtime Installers

The VFP runtime installers are no longer available for download from Microsoft's web site, so we've made them available on VFPX. Here you find the latest builds of the VFP runtime installers, as compiled by [Jürgen Wondzinski](https://github.com/Woody-Soft) (better known as "wOOdy") several years ago, when ProLib was still alive.

In the meantime, some Windows components got updates (mainly the MSXML3 stuff), but the regular Windows Update mechanism will take care of those.

Just run the installer, and then any PC starting from Win98 and newer is ready to run a regular VFP app without any further installation. If you have custom ActiveX controls, you will need to take care of those yourself.

Since those installers have been built with the WISE Installbuilder, the source code may only serve as a reference of what components need to be included. We hope to rebuild them using a modern freeware install-builder, but in the meantime those dog-old installers still do their job.

### Instructions

These installers include the all the latest hotfixes and security updates.

#### Explanation of the filename

The filename of our runtime installers is built by three parts:

 * Visual FoxPro version (ie. VFP9)
 * Service pack level (ie. SP1)
 * Runtime identifier (RT)

For example, the filename 'VFP9SP0RT.exe' stands for runtime installer of Microsoft Visual FoxPro 9.0 without any servicepack.

#### Installation

Just download the runtime you need for your own application to any folder on your machine and execute the installer by either double-clicking the file or [Start] [Run] <path\to\exe> [OK]

The runtime installer provides you a dialog to choose the several VFP specific runtime files (required ones are pre-selected), and to specify the installation directory. The common path where the runtime should be placed as a recommendation by Microsoft is pre-defined.

#### Silent installation
Additionally to the normal execution, our setup routines offers an installation mode without any user interaction. This is called 'silent mode'. The silent mode is controlled by commandline-switches and an optional response file.

#### Command line options

Here's an overview of possible commandline options:

| Option | Function |
|--------|----------|
| /M | Runs installation in manual mode, prompting for system directories such as Windows, System, etc. |
| /M=filename | Specifies a response file for installation. |
| /S | Silent mode, automatic mode with no user choices. |
| /T | Install in testmode (no files are really installed) |
| /X pathname | Extracts files to pathname |
| /Z pathname | Extracts files to pathname, then reboots |

#### Response file

While using the commandline option "/M=filename", you are able to specify a response file in order to define components and path information, if you need different settings.

The response file contains pairs of keys and values to control the installation process. Currently we provide three keys in our setups:

| Key | Function |
|-----|----------|
| ZIEL | Destination path of runtime files. The default is %CommonFiles%\Microsoft Shared\VFP. |
| SELECT_RT | Core runtime files of Visual FoxPro. This key controls the installation of EXE, MTDLL. VC++ runtime files and (since VFP 9.0) the report applications. Default is 'ABCabc' |
| SELECTION | Language dependent runtime files of Visual FoxPro. Default is 'ABCa' |

The keys SELECT_RT and SELECTION use characters to correspond with the option in the installer. This way, 'A' stands for first option, 'B' for second, and so on... Using lower characters just disables the option in the dialog.

Here is a sample how this response file (ie. setup.txt) looks like:

    ZIEL=C:\Program Files\MyApp
    SELECT_RT=ABCDabc
    SELECTION=ABCDEFa

To use this response file, call the installer like this:

    VFP9SP0RT.exe /S /M=setup.txt

## Other Installers

* Execute `VFPODBC.msi`, `VFPODBC_German.msi`, or `VFPODBC_Spanish.msi` to get the latest VFP ODBC driver.
* Execute `HTMLHelp.exe` to install the Microsoft HTML Help Workshop (needed to build CHM files).
* Execute `VFPOLEDBSetup.msi` to get the latest VFP OLE DB provider.
* Use `VFPODBC.msm` or `VFPOLEDB.msm` as merge modules with a Windows Installer based installer to instal the latest VFP ODBC driver or OLE DB provider.
* Execute `VFP9.0sp2-KB958371-X86-Enu.exe` to install a ActiveX control security update (from [https://www.microsoft.com/en-us/download/details.aspx?id=22158](https://www.microsoft.com/en-us/download/details.aspx?id=22158).

## More Info

* See wOOdy's blog entry ["How to install VFP9 in a modern world"](http://woody-prolib.blogspot.com/2018/12/how-to.html) for more details and tips on how to set up VFP 9 and upgrade to the latest version.

* See [ODBC_Release_Notes.md](ODBC_Release_Notes.md) for Microsoft's release notes for the ODBC driver.

* See [OLEDB_Release_Notes.md](OLEDB_Release_Notes.md) for Microsoft's release notes for the OLE DB provider.

