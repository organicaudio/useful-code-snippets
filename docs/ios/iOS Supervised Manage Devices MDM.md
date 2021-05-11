# iOS Supervised Manage Devices / MDM

## [Enable Supervised Mode] How to supervise managed devices without data loss?
https://www.manageengine.com/mobile-device-management-msp/how-to/supervising-managed-unsupervised-devices.html

### Problem:
Supervision of iOS mobile devices provides IT admins additional control over these devices. Supervision of devices can be performed while enrolling them in Mobile Device Manager Plus using DEP Enrollment and Apple Configurator. There are cases when the devices are brought under management without supervising them and these devices are in use, supervising these devices by re-enrolling them leads to loss of the data present in the device. This document provides the steps to supervise devices that are in use without losing the data present in the devices.

_NOTE: Apple recommends that the device to be supervised be reset and re-enrolled but as this may not be feasible in most cases, the following method serves as a work around._

### Requirements:
- Device to be supervised- main device
- A temporary device to back up data- temp device (This device may or may not be enrolled with MDM)
- Apple Configurator/ Apple DEP

### Using Apple Configurator:
- Ensure that the settings Remove apps on profile removal, Restrict App data backup is unchecked when the apps were distributed.
- Back up the main device using iTunes. _(No third party backups like iMazing)_
- Restore this content on a temporary device which can be either supervised or unsupervised.
- Back up the temporary device using iTunes.
- Restore the backup of the temporary device into the device to be supervised.
- After restoration, on the setup screen, connect the device to Apple Configurator and enroll it using the steps mentioned here.
- All the app data is restored in the enrolled device and the MDM profile is installed with the new Apple Configurator profile.
- The enrolled device will be awaiting user assignment and profile distribution. The apps will have to be brought under management again.

## Prepare Applie Configurator 2.0

On Apple Configurator 2, click File, select New Profile and then select Wi-Fi. Do not modify any other profiles as this might affect the profiles distributed using MDM. 
Create a Wi-Fi profile and save it.
Click File and choose New Blueprint and name it.
Open the newly created Blueprint and click Profiles, you have to add the newly created Wi-Fi profile (which was created in step #2).
Right-click and choose Prepare as shown in the below image.
Specify the Configuration Type as Manual. If you wish to add mobile devices into your Apple Business Manager (ABM) portal from Apple Configurator 2, enable the Add to Device Enrollment Program option. Learn how, from this document.
Add the new server details by specifying the Server Name and Enrollment URL, configured in the MDM server.
Trust anchor certificates are automatically added. If Apple Configurator takes too long to fetch anchor certificates, skip and proceed directly to the Assign to organization step by clicking on Next.

------------------------------------------------------------------------------------------

### [Disable Supervised Mode] How to remove iOS supervision and release devices in Apple Business Manager

https://www.miradore.com/knowledge/ios/how-to-remove-iphone-ipad-supervision/

#### How to tell if an iPad or iPhone is supervised?
On the device, go to Settings > General > About. The device is supervised if you see a text saying “This iPad/iPhone is supervised and managed by (company name)”.


#### How to disable supervision on an iPhone or iPad?
In most cases, only the institution which owns the device can turn off the supervised mode.

Unenrolling or retiring devices from the MDM does not make them unsupervised.

A device can be enrolled in supervision two ways: Apple Configurator & Apple DEP.

The supervised mode can be removed by resetting/wiping the device to factory settings (Erase all content and settings) if the supervised mode was enabled using Apple Configurator.

If the device is still supervised after a factory reset, then it has been automatically enrolled and supervised using Apple Business Manager / DEP.  The unenrollment will need to be retired from the DEP's console.


##### How to remove iOS devices from Apple Business Manager

Sometimes you may want to remove an iPad or iPhone from Apple Business Manager entirely, for example, if the device is lost, sold or broken.

You can do that by following the guidance provided on the Apple Business Manager User Guide. It explains how you can release iOS devices in Apple Business Manager.

https://support.apple.com/en-nz/guide/apple-business-manager/asmec4d28461/web


------------------------------------------------------------------------------------------
### How To Supervise An iPhone Without Erasing Data (2018)
https://www.tecklyfe.com/how-to-supervise-an-iphone-without-erasing-data/