# video-stream-merger
Merge the video of multiple MediaStreams.   
Useful for sending composite videos across a single WebRTC MediaConnection.  
[Demo](https://rationalcoding.github.io/video-stream-merger/)

**Example:**
```javascript
// Create a new VideoStreamMerger with an output width, height and fps
var merger = new VideoStreamMerger({
  width: 300,
  height: 300,
  fps: 25
}) 

// Add one stream the full size of the stream
merger.addStream(inputStream)

// Add another stream at the top-left, 100 pixels wide and tall
merger.addStream(anotherStream, {
  x: 0,
  y: 0,
  width: 100,
  height: 100
}) 

// Or draw the frames yourself
merger.addStream(anotherStream, {
  draw: function (ctx, frame, done) {
    ctx.drawImage(frame, 5, 3, 100, 100)
    done()
  }
})

merger.start() // Begin merging the videos (the result is now available)

merger.result // The result is the composite MediaStream

merger.stop() // Stop merging (stream will freeze, can be restarted)

merger.destroy() // Clean up (stream will stop, cannot be restarted)
```

## Limitations:
- Output stream will have no audio. (Merge audio streams separately with WebAudio API)
