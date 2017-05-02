+++
creatordisplayname = "whatbatman"
creatoremail = "whatbatman@protonmail.com"
date = "2017-05-02T13:25:57Z"
description = "Extracting application files from non-rooted Android devices"
lastmodifierdisplayname = "whatbatman"
lastmodifieremail = "whatbatman@protonmail.com"
tags = ["pwn","android"]
title = "Extracting Files from Non-Rooted Android Apps"

[menu]

  [menu.main]
    identifier = "file_extraction_android"
    parent = ""
    weight = 20

+++

A lot of applications store files on Android devices insecurely, but people believe they are safe since their device is not rooted. Unfortunately, if you have physical access to the device you can still extract files stored by any application on the device, using ADB.

### Requirements
* Device must not be encrypted
* Device must be unlocked

### Extracting The Files
Connect the device to a computer and enable ADB Debugging on the device. Start the backup with the following command:

    adb backup ~/app_backup/backup.ab apk.to.backup

Click the "Backup my data" button on the Android device.

Now that the backup is complete, you can extract the backup. There are a lot of janky ways to extract the backup, however they are janky. It is best to use a tool that rarely fails, the [Android Backup Extractor](https://github.com/nelenkov/android-backup-extractor). 

    java -jar abe.jar unpack backup.ab backup.tar

Now you can simply ```untar``` the backup and you will all the file contents


### Prevention
To prevent this from being used on an application there are several options that can be set within the Android framework, the links are provided below:

* https://developer.android.com/reference/android/R.attr.html#allowBackup
* https://developer.android.com/reference/android/R.attr.html#backupAgent
* https://developer.android.com/reference/android/R.attr.html#backupInForeground
* https://developer.android.com/reference/android/R.attr.html#fullBackupOnly
* https://developer.android.com/reference/android/R.attr.html#restoreAnyVersion
