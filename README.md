# Slint Rust Template

A template for a Rust application that's using [Slint](https://slint.rs) for the user interface.



## Setup

### Pre-req (copied from Tauri setup...may not need all this)

```bash
sudo apt update
sudo apt install libwebkit2gtk-4.1-dev \
  build-essential \
  curl \
  wget \
  file \
  libxdo-dev \
  libssl-dev \
  libayatana-appindicator3-dev \
  librsvg2-dev
```

### Install Rust

```bash
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

### Add android build target

```bash
rustup target add aarch64-linux-android armv7-linux-androideabi i686-linux-android x86_64-linux-android
```

### Install Cargo-Apk

https://github.com/rust-mobile/cargo-apk

```bash
cargo install cargo-apk
```

## Setup Android SDK Environment

1. Download & install Android Studio
    1. Unpack the Android Studio distribution archive that you downloaded where you wish to install the program. Extract `android-studio` to `$HOME`.
    2. To start the application, open a console, cd into `~/android-studio/bin` and type: `./studio.sh`
      This will initialize various configuration files in the configuration directory: `~/.config/Google/AndroidStudio2024.1.`
    3. Go to SDK Manager & install the following:
      * Android SDK Platform
      * Android SDK Platform-Tools
      * NDK (Side by side)
      * Android SDK Build-Tools
      * Android SDK Command-line Tools
    4. Go to Virtual Device Manager & add a device to emulate.
    5. Edit `~./bashrc`. (modified to make Slint compile to android too)
      ```bash
      export PATH=$PATH:$HOME/android-studio/bin:$HOME/android-studio/jbr/bin
      export JAVA_HOME=$HOME/android-studio/jbr
      export ANDROID_HOME="$HOME/Android/Sdk"
      export NDK_HOME="$ANDROID_HOME/ndk/$(ls -1 $ANDROID_HOME/ndk)"
      export ANDROID_NDK_ROOT="$ANDROID_HOME/ndk/$(ls -1 $ANDROID_HOME/ndk)"
      ```
    6. Restart shell to re-load `~./bashrc`
2. Unknown if this is actually needed
    ```
    sudo apt-get install adb
    sudo agp-get install google-android-platform-tools-installer
    ```

## Usage


* Run the application binary

    * Start Android Studio. Go to 'Virtual Device Manager'.  Select a device to emulate and start the device (play button).

     ```
     cargo apk run --target aarch64-linux-android --lib
     ```

* Build release cargo (requires release keystore for cargo-apk)
     ```
     cargo apk build --release --target aarch64-linux-android --lib
     ```
