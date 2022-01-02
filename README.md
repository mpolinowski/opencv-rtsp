 # OpenCV for IP Cameras
 
Most of the IP cameras supports Real Time Streaming Protocol (RTSP) to control audio and video streaming. This 
tutorial provides example how to capture RTSP stream from IP camera using OpenCV and Python. OpenCV provides 
VideoCapture class which allows to capture video from video files, image sequences, webcams, IP cameras, etc. To 
capture RTSP stream from IP camera we need to specify RTSP URL as argument.

## INSTAR IP Cameras

Please use the [following URLs](https://wiki.instar.com/en/Outdoor_Cameras/IN-9008_HD/Video_Streaming/) to use your INSTAR camera with third-party software:

* __RTSP Stream 1__: rtsp://user:password@192.168.x.x:port/11
* __RTSP Stream 2__: rtsp://user:password@192.168.x.x:port/12
* __RTSP Stream 3__: rtsp://user:password@192.168.x.x:port/13

User and password are your camera login and the default RTSP port is `554` - e.g.:

```bash
rtsp://admin:instar@192.168.1.19:554/12
```

## Environment Setup

```bash
mkdir ./opencv-rtsp && cd opencv-rtsp
python -m venv .env
source .env/bin/activate
```

```bash
pip install opencv-python
```

## Python Code

```python
import cv2
import os

RTSP_URL = 'rtsp://admin:instar@192.168.2.117/11'

os.environ['OPENCV_FFMPEG_CAPTURE_OPTIONS'] = 'rtsp_transport;udp'

cap = cv2.VideoCapture(RTSP_URL, cv2.CAP_FFMPEG)

if not cap.isOpened():
    print('Cannot open RTSP stream')
    exit(-1)

while True:
    success, img = cap.read()
    cv2.imshow('RTSP stream', img)

    if cv2.waitKey(1) & 0xFF == ord('q'):  # Keep running until you press `q`
        break
```


