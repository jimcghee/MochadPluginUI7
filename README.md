# MochadPluginUI7   = Mochad X10 Gateway =

Plugin for Vera UI7 to connect to Mochad running on a Pogoplug or Pi using a CM15A or CM19A to control X10 stuff.

I wrote none of this.  All of the credit goes to radarengineer and/or bfocht (same personn?).  The original code I found is at:

https://github.com/bfocht/vera_plugins/tree/10a72bf5253422d471e8d28d1018fce17f82d629/mochad

This plugin allows you to use X10 devices through a linux daemon called mochad.

http://sourceforge.net/projects/mochad/

Mochad runs on desktop linux boxes, routers running openwrt, and embedded devices such as plug computers. Several people are running Mochad on Dockstar and Pogoplug plug computers. Mochad supports both the cm15a (rf and power line) and cm19a (rf only) usb controllers.

Both normal X10 (housecode + unit code) or X10Sec devices are supported. You can both control devices and receive signals using this plugin.

For more information on support please check out this command reference page:

http://sourceforge.net/apps/mediawiki/mochad/index.php?title=Mochad_Reference

The goal of this plugin is to have full support for all commands.

= Installation = 

1. Download the mochad install files here: [http://code.mios.com/trac/mios_mochad-x10/changeset/6/trunk/?old_path=%2F&format=zip Mochad Install (Zip File)]

2. Click the "Mios Developers" link in "Toolbox".

3. Go to the "Luup files" tab, scroll down, and upload the three files contained in the mochad zip file (D_Mochad1.xml, I_Mochad1.xml, S_Mochad1.xml).

4. Go to the "Create Device" tab. Fill in these fields:
    * **Description:** a name for your new mochad device (e.g, "cm19a")
    * **UpnpDevFilename:** D_Mochad1.xml
    * **UnnpImplFilename:** I_Mochad1.xml
    * **IpAddress:** The ip address of the machine running the mochad daemon.

5. Exit the mios developers popup.

6. Click the little wrench in the upper right hand corner of the newly created mochad device.

7. Go to the "Advanced" tab and scroll down to the "Variables" section.

8. Fill in the following variables:
    * **BinaryModules:** a comma separated list of house/unit codes for any appliance modules you may have. For example: "A1,D2"
    * **DimableModules:** a comma separated list of house/unit codes, but for *old style* dimmable modules.
    * **SoftstartModules:** a comma separated list of house/unit codes, but for newer dimmable modules like any recently produced LM465s.
    * **MotionSensors:** a comma separated list of house/unit codes for any motion sensors you may have. Don't forget that X10 outside motion sensors (like the !EagleEye MS14A and the !ActiveEye MS16A) have a photosensor that will return a code for transitions to night/day. These alerts occur at a unit code one above the currently set unit code. This means that a motion sensor set to M1 will alert on M1 when there is motion and M2 for day / night.
    * **RFSecMotionSensors:** a comma separated list of RFSec motion sensors like the MS10A. For example: "02:00:00,03:00:00"
    * **RFSecDoorSensors:**  a comma separated list of RFSec door/window sensors like the ds10a
    * **PowerLineCommand:** this is set to 0 to control lights with RF commands and 1 to control lights with PL commands. PL control requires a cm15a.
