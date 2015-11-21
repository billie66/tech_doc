之前想当然的把 videojs 写成这样一个组件，

```
Video = React.createClass({
  render() {
    return (
      <video id="example_video_1" className="video-js vjs-default-skin"
        controls preload="auto" width="640" height="264"
        poster="http://video-js.zencoder.com/oceans-clip.png"
        data-setup='{"example_option":true}'>
         <source src="http://video-js.zencoder.com/oceans-clip.mp4" type='video/mp4' />
      </video>
    );
  }
});
```

是错误的，reactjs 会报错

```
Uncaught Error: Invariant Violation: ReactMount: Two valid but unequal nodes with the same `data-reactid`
```

针对上述问题，SO 上面有相关讨论

http://stackoverflow.com/questions/26255344/reactjs-cant-change-video-and-poster-videojs

另外 videojs 项目 issue 中，也在探讨如何把 videojs 组件化

https://github.com/videojs/video.js/issues/2006

下面是一个 videojs 的 react 组件

https://gist.github.com/mikechau/5547c67d0dc2957e907d

参照下面 gist 中的代码，略加修改，可以满足项目需求

https://gist.github.com/ryanmcgrath/9e9757aa429b1684c9d0
