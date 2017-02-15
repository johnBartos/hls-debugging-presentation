# HLS, and How to Debug It

## How HLS Works
The Player plays HLS content by downloading a `master manifest`, which contains links to one or more `child manifests`, which contain links to several `.ts` files. These files are `demuxed` into their elementary audio and video components and then `remuxed` into an `.mp4`. The player then passes these files to the browser, forming a coherent `stream`. This process is repeated until the stream ends, the user quits, or the player crashes.


#### Manifests
Manifests are just text files. Honest. How they're used depends on what they contain. There are currently two types of manifests: `master` and `child`. Each manifest also contains `EXT-X metadata` which tells the player how to put it all together.

#### Master Manifest
The `Master Manifest` is the most top-level part of an HLS stream. It describes the stream and is used by the player to coordinate playback. In addition to `metadata`, it contains one or more links to `child manifests`. 

#### Child Manifests
`Child manifests` represent a small chunk of the overall HLS stream. They contain links to the actual pieces of media. This media can be in the form of `video`, `audio`, or `VTT subtitles`. Child manifests representing video contain links to `.ts` files. Each video manifest is considered a quality level. Audio manifests represent `alternate audio track` and can contain . VTT manifests represent subtitles. 

##### .ts File
The `.ts` file, or transport-segment file, is the lowest
 








### Terminology
