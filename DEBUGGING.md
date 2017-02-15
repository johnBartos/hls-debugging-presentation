# HLS, and How to Debug It

## How HLS Works
The Player plays HLS content by downloading a `master manifest`, which contains links to one or more `child manifests`, which contain links to several `.ts` files. These files are `demuxed` into their elementary audio and video components and then `remuxed` into an `.mp4`. The player then passes these files to the browser, forming a coherent `stream`. This process is repeated until the stream ends, the user quits, or the player crashes.


#### Manifests
Manifests are just text files. Honest. How they're used depends on what they contain. There are currently two types of manifests: `master` and `child`. Master manifests contain links to child manifests, and child manifests contain links to media. Each manifest also contains `EXT-X metadata` which tells the player how to put it all together.

#### Master Manifest
The `Master Manifest` is the most top-level part of an HLS stream. It describes the stream to the player and is used to coordinate playback. In addition to `metadata`, it contains one or more links to `child manifests`. 

#### Child Manifest
`Child manifests` represent a small chunk of the overall HLS stream. They contain links to the actual pieces of media. This media can be in the form of `video`, `audio`, or `VTT subtitles`. Child manifests representing video contain links to `.ts` files. Each child video manifest within the master is considered a quality level. Audio manifests represent `alternate audio track`. VTT manifests represent subtitles. 

##### .ts File
The `.ts` file, or transport stream, is the container for audio and video of a stream. It also contains information about when the media is supposed to be played. However, the browser cannot natively understand what to do with it. It's up to the player to transform this file into an .mp4 the browser can understand.

## Tools
#### The Console
The console is your best friend and should always be monitored while investigating a stream. **Open the console and keep it open while debugging.**

Tips:
- Use the filters to see just `errors` or `warnings`, or both
 - Errors are usually bad
    - Network: `4xx`, `5xx`, crossdomain error
    - Uncaught Exceptions
 - Warnings are not always bad
 


#### The Network Tab
The network tab is also your best friend.

Tips:
- Filter by `.ts` to see video segments
- Filter by `.m3u8` to see  manifests
- Filter by `.vtt` to vtt subtitles
- Only starts recording when opened - do a hard refresh to see everything downloaded from the start of the stream

#### Safari
Safari is our gold standard. If it works in Safari it should work in our player; if not, we will not pursue a solution.

Tips:
- Streams which crash after a certain duration in our player will often play for longer in Safari (but will still crash). Always test longer in Safari

#### Hls.js Reference Page
The Hls.js reference page is useful for zeroing in on where a problem is: our player, our version of hls.js, or all versions of hls.js.

Tips:
- Start by testing the stream in the latest reference player
- If it works in the latest reference player, test our version of the reference player
- If it doesn't work in our version of the reference player, test increasing versions inbetween our version and the latest to find the first working version

## Debugging Checklist
1. Are there any errors in the console?
    - Network
2. Does it work in Safari?
3. Does it work in the latest version of the Hls.js reference player?
4. Does it work in our version of the Hls.js reference player?


## Common Error Types
### Encoding Errors
- Check the codec
### Customer Errors
### Player Errors

## Reports
[ ]


## Help! My Stream Doesn't Work!

#### The stream does not start

#### The stream freezes after a while

#### The stream freezes soon after playback

#### The stream doesn't start where it should

#### The stream takes forever to upswitch

#### The stream is buffering a lot

#### The stream isn't Live/DVR/VOD when it should be

#### The player crashes


## Case Studies

