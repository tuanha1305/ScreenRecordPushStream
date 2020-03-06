# ScreenRecordPushStream
这是一个基于 rtmp 协议的 Android 录屏推流demo 


## 使用方法

##### 一、 服务器搭建
玩玩可以使用这个[https://github.com/illuspas/Node-Media-Server](https://github.com/illuspas/Node-Media-Server)，Node 的库自己玩玩行，用于生产差点意思。
```
mkdir nms
cd nms
npm install node-media-server
vi app.js
```
修改下 app.js里面的配置，改下 rtmp的端口就行了，你也可以使用它默认的1935
```
const NodeMediaServer = require('node-media-server');

const config = {
  rtmp: {
    port: 1935,
    chunk_size: 60000,
    gop_cache: true,
    ping: 30,
    ping_timeout: 60
  },
  http: {
    port: 8000,
    allow_origin: '*'
  }
};

var nms = new NodeMediaServer(config)
nms.run();
```
运行

```
node app.js
```

##### 二、安装 FFmpeg 和 FFPlay
安装这两个的目的呢是可以很方便的测试，利用 FFmpeg 推流，FFPlay 播放

以mac 系统为例:

* FFmpeg

```
brew install ffmpeg
```

* FFPlay

```
brew install ffmpeg --with-ffplay
```

##### 三、测试

运行 node app.js 成功后运行如下命令：

* 推流
```
ffmpeg -re -i https://github.com/mabeijianxi/ScreenRecordPushStream/raw/master/test_source/xxx.mp4  -c copy -f flv rtmp://localhost:1935/rtmplive/xxx.flv
```

* 拉流
```
ffplay rtmp://localhost:1935/rtmplive/xxx.flv
```
依次执行完成后将弹出 FFplay 的视频播放页面,里面会有一只很可爱的狗狗哈哈。

##### 四、安卓客户端上推流

运行demo以后输入相应地址，本地 IP 用 ifconfig 获取下即可。

<video src="https://github.com/mabeijianxi/pic-trusteeship/raw/master/pic/record_v.mp4" width="800px" height="600px" controls="controls"></video>



