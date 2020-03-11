---
title: "Developer Setup"
date: 2017-08-20T11:35:32-04:00
weight: 1
subsection: Mobile Apps
---

The following instructions apply to the mobile apps for iOS and Android built in React Native. Download the iOS version [here](http://about.mattermost.com/mattermost-ios-app/) and the Android version [here](http://about.mattermost.com/mattermost-android-app/). Source code can be found at https://github.com/mattermost/mattermost-mobile.

If you run into any issues getting your environment set up, check the [Troubleshooting](#troubleshooting) section at the bottom for common solutions.

A macOS computer is required to build the Mattermost iOS mobile app.

## Environment Setup

### iOS and Android

Install the following prerequisite software to develop and build the iOS or Android apps. For macOS, we recommend using [Homebrew](https://brew.sh/) as a package manager.

#### Install [NodeJS](https://nodejs.org/en/).
This includes NPM which is also needed. Currently version 10.11.0 is recommended with npm 6.4.1. 11.x is **not** working.

##### MacOS
- To install using Homebrew open a terminal and execute ..

```sh
    $ brew install node
```
-   Install using NVM by following the instructions [here](https://github.com/creationix/nvm#install-script)
-   Download and install the package from the [NodeJS website](https://nodejs.org/en/)
##### Linux
-	Install using your distributions package manager (Note that different distros provide
    different node versions which might be lower than 10.11.0 and may cause problems)
-   Install using NVM by following the instructions [here](https://github.com/creationix/nvm#install-script)
-   Download and install the package from the [NodeJS website](https://nodejs.org/en/)

#### Install [Watchman](https://facebook.github.io/watchman/). (minimum required version is 4.9.0)
##### MacOS
- To install using Homebrew open a terminal and execute ..
    ```sh
    $ brew install watchman
    ```
##### Linux
- On Linux you have to build Watchman yourself. See the official [Watchman guide](https://facebook.github.io/watchman/docs/install.html#installing-from-source).
    - Note that you need to increase your inotify limits for watchman to work properly
    - If you encounter a warning about a missing C++ compiler you need to install the c++
    extension from you distros package manager (Ubuntu: g++, RHEL/Fedora: gcc-g++)

#### Install ```react-native-cli``` tools

Use *npm* to install [React Native CLI Tools](http://facebook.github.io/react-native/docs/understanding-cli.html) globally (minimum required version is 2.0.1)

```sh
$ npm -g install react-native-cli
```

#### Install ```bundler --version 2.0.2``` gem
```sh
$ sudo gem install bundler --version 2.0.2
```

#### Obtaining the source code
We use GitHub to host the source code so we recommend that you install [Git](https://git-scm.com/) to get the source code. Optionally, you can also contribute by submitting [pull requests](https://help.github.com/articles/creating-a-pull-request/). If you do not have git installed you can do so with Homebrew by opening a terminal and executing:

##### MacOS

```sh
$ brew install git
```

##### Linux
Some distributions come with git preinstalled but you'll most likely have to install it yourself. For most distributions the package is simply called ```git```

### Additional setup for iOS

1.  Install [Xcode](https://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12) to build and run the app on iOS. (minimum required version is 10.0)
2.  Install [Cocoapods](https://cocoapods.org/) using the `gem` method. You'll need it to install the project's iOS dependencies. (required version is 1.7.5)

### Additional setup for Android

#### Download and install [Android Studio or the Android SDK command line tools](https://developer.android.com/studio/index.html#downloads).

#### Environment Variables
Make sure you have the following ENV VARS configured:
    - `ANDROID_HOME` to where Android SDK is located (likely `/Users/<username>/Library/Android/sdk` or `/home/<username>/Android/Sdk`)
    - Make sure your `PATH` includes `ANDROID_HOME/tools` and `ANDROID_HOME/platform-tools`
##### MacOS
-   On Mac, this usually requires adding the following lines to your `~/.bash_profile` file:

    ```sh
    export ANDROID_HOME=$HOME/Library/Android/sdk
    export PATH=$ANDROID_HOME/emulator:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools:$PATH
    ```
- Then reload your bash configuration:

    ```sh
    source ~/.bash_profile
    ```
##### Linux
-   On Linux the home folder is located under ```/home/<username>``` which results in a slightly different path

    ```sh
    export ANDROID_HOME=/home/<username>/Android/Sdk
    export PATH=$ANDROID_HOME/platform-tools:$PATH
    export PATH=$ANDROID_HOME/tools:$PATH
    ```
- Then also relead you configuration
    ```sh
    source ~/.bash_profile
    ```
    - Note that depending on the shell your using this might need to be put into a different file such as ```~/.zshrc```. Adjust this accordingly.
    - Also this documentation assumes you chose the default path for your Android SDK installation. If you chose a different path adjust accordingly.

### Installing the right SDKs and SDK Tools
In the SDK Manager using Android Studio or the [Android SDK command line tool](https://developer.android.com/studio/command-line/sdkmanager.html), ensure the following are installed
- SDK Tools (you may have to click "Show Package Details" to expand packages)
    ![image](/img/mobile/sdk_tools.png)
    - Android SDK Build-Tools 28.0.3
    - Android Emulator
    - Android SDK Platform-Tools
    - Android SDK Tools
    - Google Play services
    - Intel x86 Emulator Accelerator (HAXM installer)
    - Support Repository
        -   Android Support Repository
        -   Google Repository

- SDK Platforms (you may have to click "Show Package Details" to expand packages)
    ![image](/img/mobile/sdk_platforms.png)
    - Android 7 (Nougat) or above ([We've dropped Android 5/6 Support since December 2018, you may still continue to use 1.14 for Android 5/6 devices](https://github.com/mattermost/mattermost-mobile/issues/2480))
        - Google APIs
        - SDK Platform
            - For Android 7 or above -> Android SDK Platform 24 or above
            - For Android 5/6 -> Android SDK Platform 23 or below
        - Intel x86 Atom\_64 System Image
    - Any other API version that you want to test


## Obtaining the Source Code

In order to develop and build the Mattermost mobile apps you'll need to get a copy of the source code. Forking the `mattermost-mobile` repository will also make it easy to contribute your work back to the project in the future.

1.  Fork the [mattermost-mobile](https://github.com/mattermost/mattermost-mobile) repository on GitHub.

2. Clone your fork locally:
    - Open a terminal
    - Change to a directory you want to hold your local copy
    - Run `git clone https://github.com/<username>/mattermost-mobile.git` if you want to use HTTPS, or `git clone git@github.com:<username>/mattermost-mobile.git` if you want to use SSH

    **`<username>` refers to the username or organization in GitHub that forked the repository**

3.  Change the directory to `mattermost-mobile`.
    ```sh
    cd mattermost-mobile
    ```

4.  Run `make pre-run` in order to install all the dependencies.
