---
icon: merge
---

# Compositor

The Compositor Server is a 3U workstation running windows that runs OBS.  This computer will take in all the video feeds on the field and produce a single feed that gets sent to the Ultra Encode and to the Pits.  The underlying technology is NDI for Pit distribution, if not a private feed on YouTube if the network cannot reach that far.&#x20;

## OBS

Open Broadcast Software or OBS is the underlying software that runs the video feeds. it will take in all the Camera feeds based on the RTSP feed produced in the camera.  Additionally this will also layout  the camera feeds similar to an actual competition&#x20;

{% embed url="https://obsproject.com/" %}

### Plugins

#### GStreamer

Gstreamer is an required plugin to provide low latency RTSP streams from the cameras. This also requires the install of the GStreamer runtime. The pipeline is based on the string below

```
rtspsrc location=rtsp://[RTSPUSERNAME]:[RTSPPassword]@[IPofCamera]:554/cam/realmonitor?channel=1&subtype=0 latency=100 ! application/x-rtp, payload=96 ! rtph264depay ! h264parse ! avdec_h264 ! video.
```

{% embed url="https://obsproject.com/forum/resources/obs-gstreamer.696/" %}

#### Distro-AV&#x20;

This is the plugin for OBS for distribution of NDI to the Pits and other areas. This also requires the NDI 5.0 Runtime which is included in the NDI Tools in the link below.

{% embed url="https://obsproject.com/forum/resources/distroav-network-audio-video-in-obs-studio-using-ndi-technology.528/" %}

{% embed url="https://ndi.video/tools/" %}

## In-between matches

The Compositor in-between matches can Highlight Sponsors or play words on stream to fill in the time.



