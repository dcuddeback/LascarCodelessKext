# Lascar Codeless Kext

This project contains a codeless kext that allows programs to access Lascar USB air sensors on OS X
using user space libraries such as libusb. It currently supports the EL-USB-RT sensor.

## Installation

1. Build the kernel extension with XCode. From the project's root directory, run `xcodebuild`:

   ```
   xcodebuild
   ```

2. Copy the files to a temporary location with `sudo`:

   ```
   sudo cp -vr build/Release/LascarCodelessKext.kext /tmp/
   ```

   Copying the files with `sudo` sets the permissions appropriately for a kernel extension. You can
   verify that the permissions are correct by running:

   ```
   kextutil -nt /tmp/LascarCodelessKext.kext
   ```

   This will print diagnostics about the kernel extension. If `kextutil` doesn't show any errors,
   continue to the next step to install the kext.

3. Move the kext to a directory recognized by the system and update the system's cache:

   ```
   sudo mv -v /tmp/LascarCodelessKext.kext /System/Library/Extensions/
   sudo touch /System/Library/Extensions/
   ```

   The next time the USB air sensor is plugged into the system, it should be available to user space
   programs.
