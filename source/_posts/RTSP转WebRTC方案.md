---
title: RTSP转WebRTC方案
date: 2024-08-09 16:22:36
tags:
  - RTSP
  - WebRTC
category: Javascript
author: Xavier
summary: 方案一：RTSP转WebRTC，再用video播放；方案二：用MediaMtx先把监控的RTSP转成其他格式，然后再用对应的播放器播放
---

# 方案一：RTSP转WebRTC，再用video播放

> https://blog.csdn.net/qq_20937557/article/details/129879697

```javascript
<template>
  <div>
    <video :id="videoId" :autoplay="true" :height="height" :width="width" :controls="false" :muted="true"></video>
  </div>
</template>

<script>
import { getUUID } from '@/utils'
export default {
  data () {
    return {
      webRtcServer: null,
      videoId: `dahua_video_player_${getUUID()}`
    }
  },
  props: {
    rstpUrl: {
      default: '',
      type: String
    },
    height: {
      default: 240,
      type: Number
    },
    width: {
      default: 320,
      type: Number
    },
    webStreamerUrl: {
      default: 'http://localhost:8000',
      type: String
    }
  },
  mounted () {
    this.$nextTick(() => {
      // eslint-disable-next-line no-undef
      this.webRtcServer = new WebRtcStreamer(this.videoId, this.webStreamerUrl)
      this.webRtcServer.connect(this.rstpUrl)
    })
  },
  beforeDestroy () {
    this.webRtcServer.disconnect()
    this.webRtcServer = null
  }
}
</script>

```

# 方案二：用MediaMtx先把监控的RTSP转成其他格式，然后再用对应的播放器播放

> https://github.com/bluenviron/mediamtx?tab=readme-ov-file#rtsp-clients

Most IP cameras expose their video stream by using a RTSP server that is embedded into the camera itself. In particular, cameras that are compliant with ONVIF profile S or T meet this requirement. You can use MediaMTX to connect to one or multiple existing RTSP servers and read their video streams:

```
paths:
  proxied:
    # url of the source stream, in the format rtsp://user:pass@host:port/path
    source: rtsp://original-url
```

The resulting stream will be available in path /proxied.

The server supports any number of source streams (count is just limited by available hardware resources) it's enough to add additional entries to the paths section:

```
paths:
  proxied1:
    source: rtsp://url1

  proxied2:
    source: rtsp://url1
```