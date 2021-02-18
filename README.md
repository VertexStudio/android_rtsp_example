# Android GStreamer sample player application

Use JAVA 8 for best performance.

Download and extract the universal GStreamer Android binaries to
a directory of your choice.

<https://gstreamer.freedesktop.org/data/pkg/android/>

Edit line 83 of gstreamer-1.0-android-universal-1.18.3/armv7/share/gst-android/ndk-build/gstreamer-1.0.mk
and replace for this:

```bash
GSTREAMER_LD                  := -fuse-ld=bfd$(EXE_SUFFIX) -Wl,-soname,lib$(GSTREAMER_ANDROID_MODULE_NAME).so
```

Set path of this binaries.

Edit gradle.properties in order to set gstAndroidRoot to point to the
unpacked GStreamer Android binaries.

## Download SDK and NDK of Android

NDK-r21e is the best to use for it
<https://developer.android.com/ndk/downloads>
Set path of your SDK and NDK.

## Build apk on the command line

To build the apk for rtsp example to your device, use this command:

```bash
./gradlew assembleDebug
```
 
## Build and run from Android Studio

Launch Android-studio, opening this folder as a project.

The project should build automatically, once it has done successfully,
it should be possible to run the project with Run > Run 'app', provided
a device is attached and USB debugging enabled.

The logs can be seen in the logcat tab.

## Modify the GStreamer pipeline

Go to line 159 in app/jni/rtsp-example.c and the replace the pipeline for:

```bash
rtspsrc location=rtsp://192.72.1.1/liveRTSP/av2 latency=200 ! rtph264depay ! avdec_h264 ! fpsdisplaysink
```
Go to line 29 in app/jni/Android.mk and add new GStreamer Plugins

```bash
$(GSTREAMER_PLUGINS_NET) $(GSTREAMER_PLUGINS_SYS) $(GSTREAMER_PLUGINS_CODECS_RESTRICTED) $(GSTREAMER_PLUGINS_EFFECTS) $(GSTREAMER_PLUGINS_NET_RESTRICTED)
```


