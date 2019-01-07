# Usage of gstreamer on jetson TX2

```bash
gst-launch-1.0 nvcamerasrc sensor-id=0 ! 'video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)I420, framerate=(fraction)30/1' ! nvvidconv flip-method=2 ! 'video/x-raw(memory:NVMM), format=(string)I420' ! nvoverlaysink -e   # terminal command to show camera output
```
`sensor-id=0` > camera 0 

`sensor-id=1` > camera 1 

`sensor-id=2` > camera 2 

`sensor-id=3` > camera 3 

```python
nvcamerasrc sensor-id=0 ! video/x-raw(memory:NVMM), width=(int)1280, height=(int)720, format=(string)I420, framerate=(fraction)30/1 ! nvvidconv ! video/x-raw, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink  # usage in OpenCV
```

```python
def open_onboard_camera(device_number, width, height):
    return cv2.VideoCapture("nvcamerasrc sensor-id=%s ! video/x-raw(memory:NVMM), width=(int)%s, height=(int)%s, format=(string)I420, framerate=(fraction)30/1 ! nvvidconv ! video/x-raw, format=(string)BGRx ! videoconvert ! video/x-raw, format=(string)BGR ! appsink" % (device_number, width, height))
```

reference
- [https://developer.ridgerun.com/wiki/index.php?title=Gstreamer_pipelines_for_Jetson_TX2](https://developer.ridgerun.com/wiki/index.php?title=Gstreamer_pipelines_for_Jetson_TX2)
- [https://blog.csdn.net/csdnhuaong/article/details/80172296](https://blog.csdn.net/csdnhuaong/article/details/80172296)
- [http://petermoran.org/csi-cameras-on-tx2/](http://petermoran.org/csi-cameras-on-tx2/)
- [https://github.com/peter-moran/jetson_csi_cam.git](https://github.com/peter-moran/jetson_csi_cam.git)

