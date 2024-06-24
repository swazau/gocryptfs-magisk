# gocryptfs-magisk

## Description
This project provides working fusermount3 and gocryptfs binaries for arm64 devices, packaged as a Magisk module.

## Version
Current version: v1.0

## Requirements
- ARM64 device
- Magisk 23.0 or greater installed
- Magisk's "Mount Namespace Mode" set to "Global"

## Installation
Flash Module and reboot. Check installation by running ```fusermount``` or ```gocryptfs``` in a terminal like Termux (as root user)

## Initial Setup
Create two folders, one for encryption and one for decrypted files. For example ```mkdir enc dec```. I will assume these have been created in the /sdcard root for this example.
Create the encrypted directory using ```gocryptfs -init /sdcard/enc```, enter a password.
Mount the encrypted directory to the decrypted one using ```gocryptfs -allow_other /sdcard/enc /sdcard/dec```, enter your password.
Your output will contain some syscall and initcode errors, ignore these, as long as you get a green output with "Filesystem mounted successfully", then it is ready to use, if you have followed the above requirements and set your namespace to global, then navigate to your preferred file explorer and open /sdcard/dec, at this point it should be empty, place some files you would like encrypted. After doing this, check the enc directory to make sure it has the equivilent number of files, they will have random names, this is good, everything is working correctly.


## Usage
To mount an already created filesystem, if you have rebooted or unmounted it is simple.
```gocryptfs -allow_other /sdcard/enc /sdcard/dec``` will have it remounted, and all your encrypted files will appear in the dec folder.

To unmount the encrypted filesystem, use ```fusermount -u /sdcard/dec```, to check it has been unmounted you can use ```mount | grep gocryptfs```, this should show no mounted filesystems.


## Important Note
Magisk must have "Mount Namespace Mode" set to "Global". Otherwise, only the root user (and not your applications) will be able to view the decrypted directory.

## Included Binaries
- fusermount3
- gocryptfs 2.4
