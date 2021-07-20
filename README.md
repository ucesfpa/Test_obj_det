# Run real time object detection with YOLOv5 on live video feed from GoproHero 9 black.

## 1. Run the GoproHero 9 as webcam on Linux
```
$ sudo apt install ffmpeg v4l2loopback-dkms # installs dependencies
$ sudo su -c "bash <(wget -qO- https://cutt.ly/PjNkrzq)" root # installs required scripts
$ gopro webcam -p enx -n -a # runs the scripts # connect and switch on the Gopro first
```
You will notice an output similar to this:
```
Running GoPro Webcam Util for Linux [0.0.3]

       Launch Options     
==========================
 * Non-interactive:  1
 * Autostart:        1
 * Preview:          0
 * Device Pattern:   enx
==========================

v4l2loopback is loaded!
v4l2loopback was unloaded successfully.
v4l2loopback was successfully loaded.
Using provided device pattern enx

Discovered: enx9a298ab0cdea.
Using enx9a298ab0cdea to discover the GOPRO_IP.
Found 172.23.165.54
To control the GoPro, we need to contact another interface (GOPRO_IP ending with .51).. Adapting internally..
Now using this GOPRO_IP internally: 172.23.165.51
{ "status": 2, "error": 0 }
Sucessfully started the GoPro Webcam mode. (The icon on the Camera should have changed)
Starting ffmpeg..
ffmpeg version 4.2.4-1ubuntu0.1 Copyright (c) 2000-2020 the FFmpeg developers
  built with gcc 9 (Ubuntu 9.3.0-10ubuntu2)
  configuration: --prefix=/usr --extra-version=1ubuntu0.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-avresample --disable-filter=resample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librsvg --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opencl --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-nvenc --enable-chromaprint --enable-frei0r --enable-libx264 --enable-shared
  WARNING: library configuration mismatch
  avcodec     configuration: --prefix=/usr --extra-version=1ubuntu0.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-avresample --disable-filter=resample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librsvg --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opencl --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-nvenc --enable-chromaprint --enable-frei0r --enable-libx264 --enable-shared --enable-version3 --disable-doc --disable-programs --enable-libaribb24 --enable-liblensfun --enable-libopencore_amrnb --enable-libopencore_amrwb --enable-libtesseract --enable-libvo_amrwbenc
  libavutil      56. 31.100 / 56. 31.100
  libavcodec     58. 54.100 / 58. 54.100
  libavformat    58. 29.100 / 58. 29.100
  libavdevice    58.  8.100 / 58.  8.100
  libavfilter     7. 57.100 /  7. 57.100
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  5.100 /  5.  5.100
  libswresample   3.  5.100 /  3.  5.100
  libpostproc    55.  5.100 / 55.  5.100
[mpegts @ 0x5628ce6c7800] Could not find codec parameters for stream 2 (Unknown: none ([128][0][0][0] / 0x0080)): unknown codec
Consider increasing the value for the 'analyzeduration' and 'probesize' options
[mpegts @ 0x5628ce6c7800] Could not find codec parameters for stream 3 (Audio: ac3 ([129][0][0][0] / 0x0081), 0 channels, fltp): unspecified sample rate
Consider increasing the value for the 'analyzeduration' and 'probesize' options
Input #0, mpegts, from 'udp://@0.0.0.0:8554?overrun_nonfatal=1&fifo_size=50000000':
  Duration: N/A, start: 0.320000, bitrate: N/A
  Program 1 
    Stream #0:0[0x1011]: Video: h264 (High) ([27][0][0][0] / 0x001B), yuvj420p(pc, bt709, progressive), 1920x1080 [SAR 1:1 DAR 16:9], 29.97 fps, 29.97 tbr, 90k tbn, 59.94 tbc
    Stream #0:1[0x1100]: Audio: aac (LC) ([15][0][0][0] / 0x000F), 48000 Hz, stereo, fltp, 191 kb/s
    Stream #0:2[0x200]: Unknown: none ([128][0][0][0] / 0x0080)
    Stream #0:3[0x201]: Audio: ac3 ([129][0][0][0] / 0x0081), 0 channels, fltp
Stream mapping:
  Stream #0:0 -> #0:0 (h264 (native) -> rawvideo (native))
[swscaler @ 0x5628ce85e140] deprecated pixel format used, make sure you did set range correctly

Output #0, video4linux2,v4l2, to '/dev/video42':

  Metadata:
    encoder         : Lavf58.29.100
    Stream #0:0: Video: rawvideo (I420 / 0x30323449), yuv420p, 1920x1080 [SAR 1:1 DAR 16:9], q=2-31, 745750 kb/s, 29.97 fps, 29.97 tbn, 29.97 tbc
    Metadata:
      encoder         : Lavc58.54.100 rawvideo
```
This means that the camera is working now as webcam (notice there should be an icon on the camera screen confirming this).
For more options follow the instructions given [here](https://github.com/jschmid1/gopro_as_webcam_on_linux).


## 2. Clone YOLOv5 repository (credits to [Ultralytics](https://github.com/ultralytics/yolov5))
```
$ git clone https://github.com/ultralytics/yolov5.git
$ cd yolov5
```
## 3. Run the detection
From the output of step 1 notice the output line:
```ruby
Output #0, video4linux2,v4l2, to '/dev/video42':
```
run detection selecting 42 as source:
```
$ python3 detect.py --source 42
```
