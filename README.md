## DJI video sample app modified for RosettaDrone 

This is a slightly modified version of the original DJI video sample app.
I just added the code used by RosettaDrone for doing RTP streaming.

All video code in Rosetta should be replaced in the future with the code used here.

See: https://github.com/The1only/rosettadrone/issues/131

## How to test RTP Streaming

* Change the destination host and port in `app/src/main/java/com/dji/videostreamdecodingsample/media/DJIVideoStreamDecoder.java` in `initRosetta()`
* Set the `com.dji.sdk.API_KEY` in `app/src/main/AndroidManifest.xml`
* Build and run the app
* Press the "custom decoder" button
* To receive the stream, on the destination host, run the command:
`gst-launch-1.0 udpsrc port=5600 caps="application/x-rtp, media=video, clock-rate=90000, encoding-name=H264" ! rtph264depay ! avdec_h264 ! videoconvert ! autovideosink`
* If you experience issues, try reducing the video resolution using the DJI Fly App or similar.
* Also make sure your drone is not overheated. As I explained in my [Hacking on Rosetta Tutorial](https://docs.google.com/document/d/1wR56Mvd2OsT82kxMOD7f_3-c6yJGBtLaT8LuVrmC5wI/edit?usp=sharing) it is common that video fails and crashes if you don't use a fan.
* Please report your results commenting here: https://github.com/The1only/rosettadrone/issues/131

The rest of this document is a copy of the original version.

---

Based on https://github.com/DJI-Mobile-SDK-Tutorials/Android-VideoStreamDecodingSample but updated frequently. 

# Android-VideoStreamDecodingSample

## Introduction

This sample code demonstrates how to use [FFmpeg](https://ffmpeg.org) for video frame parsing and to use the `MediaCodec` for hardware decoding. It will help to parse video frames and decode the raw video stream data from DJI Camera and output the [YUV](https://en.wikipedia.org/wiki/YUV) data. 

## Requirements

 - Android Studio 2.0+
 - Android System 4.2+
 - DJI Android SDK 4.15

## IMPORTANT: Install `git lfs`

This repository uses Git Large File Storage (`git lfs`) for JNI lib storage. Please install `git lfs` from [here](https://github.com/git-lfs/git-lfs/wiki/Installation).

After `git lfs` installation, you can clone or pull just like normal repository.

Click [here](https://github.com/git-lfs/git-lfs/wiki/Tutorial) for more information on `git lfs`.

>NOTE: You CANNOT use **DOWNLOAD** feature because it does not automatically pull from `git lfs`. Please use `git clone`. If you want to clone only latest commit, you can use `--depth 1` option of `git clone`.

## Explanation

For this sample code's explanation, please refer to <https://developer.dji.com/mobile-sdk/documentation/sample-code/index.html>.

## Feedback

We’d love to hear your feedback on this demo and tutorial.

Please use **Github Issue** or **email** [oliver.ou@dji.com](oliver.ou@dji.com) when you meet any problems of using this demo. At a minimum please let us know:

* Which DJI Product you are using?
* Which Android Device and Android system version you are using?
* Which Android Studio version you are using?
* A short description of your problem includes debugging logs or screenshots.
* Any bugs or typos you come across.

## License

Android-VideoStreamDecodingSample is available under the MIT license. Please see the LICENSE file for more info.

## Join Us

DJI is looking for all kinds of Software Engineers to continue building the Future of Possible. Available positions in Shenzhen, China and around the world. If you are interested, please send your resume to <software-sz@dji.com>. For more details, and list of all our global offices, please check <https://we.dji.com/jobs_en.html>.

DJI 招软件工程师啦，based在深圳，如果你想和我们一起把DJI产品做得更好，请发送简历到 <software-sz@dji.com>.  详情请浏览 <https://we.dji.com/zh-CN/recruitment>.
