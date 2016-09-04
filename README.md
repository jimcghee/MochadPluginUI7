# MochadPluginUI7   = Mochad X10 Gateway =

Plugin for Vera UI7 to connect to Mochad running on a Pogoplug or Pi using a CM15A or CM19A to control X10 stuff.

I wrote none of this.  All of the credit goes to radarengineer and/or bfocht (same person?).  The original code I found is at:

https://github.com/bfocht/vera_plugins/tree/10a72bf5253422d471e8d28d1018fce17f82d629/mochad

This plugin allows you to use X10 devices through a linux daemon called mochad.

http://sourceforge.net/projects/mochad/

Mochad runs on desktop linux boxes, routers running openwrt, and embedded devices such as plug computers. Several people are running Mochad on Dockstar and Pogoplug plug computers. Mochad supports both the cm15a (rf and power line) and cm19a (rf only) usb controllers.

Both normal X10 (housecode + unit code) or X10Sec devices are supported. You can both control devices and receive signals using this plugin.

For more information on support please check out this command reference page:

http://sourceforge.net/apps/mediawiki/mochad/index.php?title=Mochad_Reference

The goal of this plugin is to have full support for all commands.

== Installation ==

There are two approaches to installation.  The Safe way and the Pretty way.
The safe way is to copy the 8 files you download to the Luup engine and create the Mochad device manually.  It's down side is that you won't have a 'Mochad' app listed in 'My Apps'.  Doesn't really matter except it isn't as pretty.
The Pretty way is to install the UI5 Mochad and before it can do any damage copy the same 8 files to the Luup engine.  The problem is that if you should give Mochad your Pi's IP before copying the new files, it will go into a crash/reboot loop that will keep creating A1, A2, and M1 over and over again.  In other words, DON'T BE IN A RUCH TO GIVE YOUR NEW MOCHAD DEVICE THE IP ADDRESS OF YOUR PI!

== The 'Install the App' way ==

1. Download the Mochad install files here: [https://github.com/jimcghee/MochadPluginUI7]. 
	Click the 'clone or download' button, then click 'Download ZIP'.  Extract the zip into a local directory.

2. 	Install 'Mochad X10 Gateway' from the App store.
	A minute or two after 'Mochad X10 Gateway' is installed, you will see a blue banner that says:
	
	Cannot connect to Mochad on : Mochad
	
	At this point you have installed the UI5 version that DOESN'T WORK!  This is good.
	
3.	Click the "Apps" link on the left side of the Vera Web page, then click "Develop Apps", 
	then "Luup files".

4. 	You will see a green "Upload" button.  Grab 8 of the 9 files downloaded/extracted (ignore the README) 
	and drop them on the "upload" button.  You will see all 8 files copy.  
	
5.	Click 'Serial Port Configuration' (on the same page) and click the Save button.  
	This will cause the Luup engine to reload.
	
6.	Click Device and look in "No Room" to find the newly created Mochad device 
	titled: 'Mochad Control of cm15a over ethernet'.

7.	Go to the "Advanced" tab and click "Params" and enter the IP address of the Pi running Mochad. 
	It's OK now because you have uploaded the new files to your Vera.
	Click 'New Service' and 'Reload Engine'.  Wait for reload to complete.

8.	Go to the "Advanced" tab and click "Variables" and fill in the following variables:
    * **BinaryModules:** a comma separated list of house/unit codes for any appliance modules you may have. For example: "A1,D2"
    * **DimableModules:** a comma separated list of house/unit codes, but for *old style* dimmable modules.
    * **SoftstartModules:** a comma separated list of house/unit codes, but for newer dimmable modules like any recently produced LM465s.
    * **MotionSensors:** a comma separated list of house/unit codes for any motion sensors you may have. Don't forget that X10 outside motion sensors (like the !EagleEye MS14A and the !ActiveEye MS16A) have a photosensor that will return a code for transitions to night/day. These alerts occur at a unit code one above the currently set unit code. This means that a motion sensor set to M1 will alert on M1 when there is motion and M2 for day / night.
    * **RFSecMotionSensors:** a comma separated list of RFSec motion sensors like the MS10A. For example: "02:00:00,03:00:00"
    * **RFSecDoorSensors:**  a comma separated list of RFSec door/window sensors like the ds10a
    * **PowerLineCommand:** this is set to 0 to control lights with RF commands and 1 to control lights with PL commands. PL control requires a cm15a.
	
9.	Again, click 'New Service' and 'Reload Engine'.  When the reload completes, all of your new X10 
	devices should appear in the 'No Room' page.

== The 'Alternate' way ==

	Instead of installing the Mochad app, you will create it's device manually.
	
	Do STEP 1 and SKIP STEP 2.
	
	Do STEP 3, and 4, and then:
	
	Go to the "Create Device" tab. Fill in these fields:
    * **Description:** a name for your new Mochad device (e.g, "cm19a")
    * **UpnpDevFilename:** D_Mochad1.xml
    * **UnnpImplFilename:** I_Mochad1.xml
    * **IpAddress:** The ip address of the machine running the Mochad daemon.

	Then, click the 'Create Device' button.
	
	Complete the process, beginning with STEP 5 (reloading the Luup engine).

Note: If you already have the Mochad app running in UI5, you can copy/paste the values in step 8 from your old installation so all your devices will automatically be created and all you will have to do is name them, put them in rooms, and wire them to your scenes.
