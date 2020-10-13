---
title: "Sign Unsigned Android"
date: 2018-05-20T11:35:32-04:00
weight: 1
subsection: Sign Unsigned Builds
---

With every Mattermost mobile app release, we publish the Android unsigned apk in in the <a href="https://github.com/mattermost/mattermost-mobile/releases" target="_blank">GitHub Releases</a> page, this guide describes the steps needed to modify and sign the app, so it can be distributed and installed on Android devices.

#### Requisites

1. <a href="https://ibotpeaches.github.io/Apktool/" target="_blank">Apktool</a> is a tool for reverse engineering Android apk files.
2. <a href="http://xmlstar.sourceforge.net/doc/UG/xmlstarlet-ug.html" target="_blank">XMLStarlet</a> is a set of command line utilities (tools) which can be used to transform, query, validate, and edit XML documents and files using simple set of shell commands in similar way it is done for plain text files using UNIX grep, sed, awk, diff, patch, join, etc commands.
3. <a href="https://stedolan.github.io/jq/" target="_blank">JQ</a> is like sed for JSON data - you can use it to slice and filter and map and transform structured data with the same ease that sed, awk, grep and friends let you play with text.
4. Android SDK as described in the [Developer Setup](/contribute/mobile/developer-setup/#additional-setup-for-android)
5. Setup keys and Google Services as described
in steps 2, 3, 4 & 6 of the [Build your own App guide](/contribute/mobile/build-your-own/android/#build-preparations).
6. `sign-android` script to sign the Android app.

#### Signing Tool

```bash
Usage: sign-android <unsigned apk file>
		[-e|--extract path]
		[-p|--package-id packageID]
		[-g|--google-services path]
		[-d|--display-name displayName]
		outputApk
Usage: sign-android -h|--help
Options:
	-e, --extract path			    (Optional) Path to extract the unsigned APK file.
                                    By default the path of the unsigned APK is used.

	-p, --package-id packageID		(Optional) Specify the unique Android application ID.

	-g, --google-services path		(Optional) Path to the google-services.json file.
							        Will setup the Firebase to receive Push Notifications.
							        Warning: will apply only if packageID is set.

	-d, --display-name displayName	(Optional) Specify new application display name.
                                    By default "Mattermost" is used.

	-h, --help				        Display help message.
```

#### Sign the Mattermost Android app

Now that all requisites are met, it's time to sign the Mattermost app for Android. Most of the options of the signing tool are optional
but you should really be using your own `package identifier`, `google services settings` and maybe change the `display name`.

* Create a folder that will serve as your working directory to store all the needed files.

* Download the <a href="/scripts/sign-android" download>sign-android</a> script and save it in your working directory.

* Download the <a href="https://github.com/mattermost/mattermost-mobile/releases" target="_blank">Android unsigned build</a> and save it in your working directory.

* Open a terminal to your working directory, make sure the `sign-android` script it is executable.

```bash
$ ls -la
total 49756
drwxr-xr-x   4 user  staff       128 Oct  2 08:12 .
drwx------@ 59 user  staff      1888 Oct  1 14:12 ..
-rw-r--r--   1 user  staff  50685064 Sep 29 10:58 Mattermost-unsigned.apk
-rw-r--r--   1 user  staff      2597 Oct  2 08:19 google-services.json
-rwxr-xr-x   1 user  staff      7005 Sep 30 12:47 sign-android
```

* Sign the app

```bash
$ ./sign-android Mattermost-unsigned.apk -p com.example.test -g google-services.json -d "My App" MyApp-signed.apk
```

once the code sign is complete you should have a signed APK in the working directory with the name **MyApp-signed.apk**.

{{<note "Note">}}
The app name can be anything, use double quotes specially if the name has white spaces.

If you are using a `Google Services` json file, you need to specify a `package identifier` that has a corresponding
client in the json configuration file.
{{</note>}}
