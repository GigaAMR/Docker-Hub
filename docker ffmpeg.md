docker版无人值守推流直播：
先把视频剪辑合并成一个视频，视频需MP4格式，然后放入/home/videos目录下


```
mkdir /home/videos && cd /home/videos
```



```
docker run -d --restart always -v /home/videos:/tmp/video jrottenberg/ffmpeg \
  -re -stream_loop -1 -i /tmp/video/视频名称.mp4 \
  -c:v libx264 -preset veryfast -b:v 3000k \
  -c:a aac -b:a 128k \
  -f flv rtmp://推流地址/live/密钥
```




