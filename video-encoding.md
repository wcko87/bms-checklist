## BMS BGA Encoding Guide
Linked from the [BMS Production Checklist](https://wcko87.github.io/bms-checklist/).

# BMS BGA Video Formats and Compatibility
- If you want widespread support, use wmv or mpeg for your videos. This is as a typical LR2 setup can only play wmv or mpeg videos.
- People using beatoraja will be able to play BGAs using formats like mp4 and webm, which is significant as they allow much higher quality video for smaller file sizes.

I recommend using wmv (wmv2) for LR2 and mp4 (H.264) for beatoraja.

**TIP**: If you have both `_bga.wmv` and `_bga.mp4` in your bms folder, and you specify "\_bga.wmv" in your bms, LR2 will play the wmv, while beatoraja will play the mp4. (The same applies for .mpg instead of .wmv if you prefer to use .mpg)

Thus, it's possible to include both a wmv and mp4 version of your BGA in your bms.

Some people use the mp4 version for a high quality HD BGA with a huge file size. Howver, I think there is a much better purpose for mp4 BGAs - to include a decent mid-quality (480p) BGA with a low file size (10-30MB) that won't look out of place when viewed in a HD play skin.

As a rough guide, try to keep your BGA files below 40MB in size.

# Common BGA resolutions
Unfortunately there doesn't seem to be a consensus on this.

Some people pad their BGAs with black bars to 1:1 resolutions as many skins have square BGA windows and many people use the setting to stretch BGAs.
On ther other hand some skins have 4:3 BGA windows 

- **256x256**: Note that LR2SD can only render up to 256x256 for BGAs.
- **512x512**: A larger resolution for square BGAs. May be used for LR2HD, though 480p may be preferred.
- **640x480**: Possibly the most common resolution for rectangular BGAs.
- **(?)x720**: Usually only for mp4 BGAs targeting people on beatoraja.
  - I recommend using 480p for mp4 BGAs though. Use 720p only if your BGA is simple enough for it to have a relatively low file size
  - For example, encoding mp4 at 720p, crf 27, the [BGA for $trange Attraktor](https://www.youtube.com/watch?v=pJP54U-oK-I) is only 6.5MB, while the [BGA for R.I.P.](https://www.youtube.com/watch?v=QJakdR6FWdg) is 65.6MB.

BGAs with less motion from frame to frame usually result in much smaller file sizes. Try to experiment with different quality settings to keep your file size low while maintaining a decent looking quality.

# Converting BGA formats using FFmpeg
[FFmpeg](https://ffmpeg.org/download.html) is an excellent command line tool for re-encoding video files.
Using a command line tool may sound daunting, but I'll try to make the following guide as idiot-proof as possible.

FFmpeg can also be used to crop video files, I will explain how to do so in the advanced section.

## Using FFmpeg to convert video files
This guide is for windows, though things aren't too different on mac/linux.

1. [Download FFmpeg from here](https://ffmpeg.org/download.html)
    - DON'T DOWNLOAD THE SOURCE CODE! Look under "get packages and executable files", click windows -> windows builds by gyan.dev. `ffmpeg-git-essentials.7z` is enough for what you need.
    - Direct windows download for the lazy: [ffmpeg-git-essentials.7z](https://www.gyan.dev/ffmpeg/builds/ffmpeg-git-essentials.7z)
2. Look for ffmpeg.exe in the bin folder. This is the only file you need.
3. Put ffmpeg.exe and your raw video file (which I will be calling `raw_video.mp4` from now on) in the same folder.
4. Shift+rightclick somewhere in the folder, and click "open command window here" or "open powershell window here". This brings up the command window in the selected folder.
5. Now you can use ffmpeg by copy-pasting one of the commands below.

### Converting to WMV
256x256 wmv2 video (max resolution for LR2SD), padded with black bars to make it square. [[SAMPLE (R.I.P.), 11.4MB]](https://github.com/wcko87/bms-checklist/assets/27341392/8d53e726-a4c4-48ba-b3a1-a6a008728e57) [[SAMPLE (竹), 14.6MB]](https://github.com/wcko87/bms-checklist/assets/27341392/b2c5ab92-2369-4adf-aca8-4ca54e5aaa3d)

```
.\ffmpeg.exe -i raw_video.mp4 -vf "scale=256:256:force_original_aspect_ratio=decrease,pad=256:256:(ow-iw)/2:(oh-ih)/2,setsar=1" -an -c:v wmv2 -q:v 8 _bga.wmv
```

512x512 wmv2 video, padded with black bars to make it square. [[SAMPLE (R.I.P.), 37.0MB]](https://github.com/wcko87/bms-checklist/assets/27341392/5a8813b7-36db-4eb4-a050-8dcb8f2bd66b) [[SAMPLE (竹), 49.9MB]](https://github.com/wcko87/bms-checklist/assets/27341392/05301922-21a3-4cf3-9e32-0846f49bea8e)
```
.\ffmpeg.exe -i raw_video.mp4 -vf "scale=512:512:force_original_aspect_ratio=decrease,pad=512:512:(ow-iw)/2:(oh-ih)/2,setsar=1" -an -c:v wmv2 -q:v 8 _bga.wmv
```

640x480 wmv2 video, padded with black bars to make it 4:3. [[SAMPLE (R.I.P.), 54.2MB]](https://github.com/wcko87/bms-checklist/assets/27341392/8069b5d8-c5eb-46c0-ba9c-cfd949cec0c6) [[SAMPLE (竹), 70.6MB]](https://github.com/wcko87/bms-checklist/assets/27341392/357f8f80-6579-4ef2-b1a8-9873a5563005)
```
.\ffmpeg.exe -i raw_video.mp4 -vf "scale=640:480:force_original_aspect_ratio=decrease,pad=640:480:(ow-iw)/2:(oh-ih)/2,setsar=1" -an -c:v wmv2 -q:v 8 _bga.wmv
```

Replace `-q:v 8` with a larger number for a lower quality and smaller filesize (or a smaller number for the opposite).

Note: the output file will be `_bga.mp4`.

### Converting to MP4
(?)x480 (aka 480p) H.264 video (recommended) [[SAMPLE (R.I.P.), 22.9MB]](https://github.com/wcko87/bms-checklist/assets/27341392/634dc725-3151-4a34-8c99-43970b556570) [[SAMPLE (竹), 16.3MB]](https://github.com/wcko87/bms-checklist/assets/27341392/f3a66587-7d20-4072-a22d-4da961bd48f9)
```
.\ffmpeg.exe -i raw_video.mp4 -vf "scale=-2:480" -an -crf 30 _bga.mp4
```

(?)x720 (aka 720p) H.264 video [[SAMPLE (R.I.P.), 65.5MB]](https://github.com/wcko87/bms-checklist/assets/27341392/13c1d7c8-1f48-4f74-900d-312e84c812a7) [[SAMPLE (竹), 45.7MB]](https://github.com/wcko87/bms-checklist/assets/27341392/e82ce68c-b40b-46d0-8f7f-5616be765767)
```
.\ffmpeg.exe -i raw_video.mp4 -vf "scale=-2:720" -an -crf 27 _bga.mp4
```

Replace `-crf 27` with a larger number for a lower quality and smaller filesize (or a smaller number for the opposite).

Try to experiment with different crf values to optimize for file size. It is often the case that you can make the BGA much smaller with an indistinguishable drop in quality.

## Explanation of the commands
Let's explain how the command works:
```
.\ffmpeg.exe -i raw_video.mp4 -vf "scale=-2:720" -an -crf 27 _bga.mp4
```
- `.\ffmpeg.exe` run ffmpeg. This is always the same.
- `-i raw_video.mp4` the input file is raw_video.mp4.
- `-vf "scale=-2:720"` set the resolution. -2 for width and 720 for height means the width is automatically set to keep the aspect ratio.
- `-an` remove audio from the video
- `-crf 27` quality setting is 27 (lower is higher quality)
- `_bga.mp4` this is the output file. The output file is always at the end of the command. The extension of this output file specifies what format to convert to. In this case it's mp4.

Now let's explain this command:
```
.\ffmpeg.exe -i raw_video.mp4 -vf "scale=512:512:force_original_aspect_ratio=decrease,pad=512:512:(ow-iw)/2:(oh-ih)/2,setsar=1" -an -c:v wmv2 -q:v 8 _bga.wmv
```
- `-vf "scale=512:512:force_original_aspect_ratio=decrease,pad=512:512:(ow-iw)/2:(oh-ih)/2,setsar=1"`
  - This is a complicated command used to pad the video with black bars and resize it to 512x512.
  - As a short explanation, this command is split into three parts, separated by commas:
    - `scale=512:512:force_original_aspect_ratio=decrease`: scale the video fit in a 512x512 box. But the video isn't 512x512 yet.
    - `pad=512:512:(ow-iw)/2:(oh-ih)/2`: Pad the video so that it becomes 512x512. The `(ow-iw)/2:(oh-ih)/2` part is to offset the padding so that the video is centered.
    - `setsar=1`: Sets the video's pixel aspect ratio back to 1 because sometimes the earlier operations may mess it up. This is not necessary but it's good to be safe.
- `-c:v wmv2` sets the encoder to wmv2.
  - If not specified, it will use the default encoder for wmv, which is msmpeg4 (which tbh may be fine too).
  - Note that the default encoding for mp4 is already H.264, which is why we don't bother to manually specify the encoding.


It's good to understand how the command works if you want to properly control the output of ffmpeg.

Note that `.\ffmpeg.exe` must always be at the start, and the output file `_bga.mp4` must always be at the end. Also, the input file `-i raw_video.mp4` should be as early as possible. The order of the other commands usually doesn't matter.

### Trick: `-preset veryslow`
You can add `-preset veryslow` to your ffmpeg command to make the program try harder to compress the video for a better quality/filesize ratio. It will make it take longer to encode though.

Here is an example:
```
.\ffmpeg.exe -i raw_video.mp4 -vf "scale=-2:720" -an -crf 27 -preset veryslow _bga.mp4
```

## Other FFmpeg features

### Cutting a video by timestamp
Use `-ss` and `-to` to specify the start and end timestamps of the video. Place them right after ffmpeg.exe in the command.

Example:
```
.\ffmpeg.exe -ss 1:12.23 -to 2:50.41 -i raw_video.mkv output_video.mp4
```

This along with `-preset veryfast` can also be used to test video filters (e.g. cropping, scaling) by generating a short clip quickly.

### Cropping a video
Use the crop video filter to crop a video. The format is `crop=width:height:x_offset:y_offset`.

Example:
```
.\ffmpeg.exe -i raw_video.mkv -vf "crop=640:480:100:0" output_video.mp4
```

Note that you can't use `-vf` multiple times in a single command. To combine multiple video filters (e.g. crop and scale), use commas.


### Letterbox video with blurred background (instead of black bars)
This FFmpeg command letterboxes the video with a blurred version of itself instead of black bars.

[Image Example](https://github.com/wcko87/bms-checklist/assets/27341392/6c5cd665-4c45-4a18-9133-71bcd5cf3520)


Use `-filter_complex` instead of `-vf` if you want to apply more complex operations like this.
```
.\ffmpeg.exe -i raw_video.mkv -filter_complex "[0:v]scale=512:512:force_original_aspect_ratio=increase,crop=512:512:(ow-iw)/2:(oh-ih)/2,boxblur=20[v1];[0:v]scale=512:512:force_original_aspect_ratio=decrease[v2];[v1][v2]overlay=(main_w-overlay_w)/2:(main_h-overlay_h)/2[vid]" -map [vid] -an -c:v wmv2 -q:v 8 _bga.wmv
```
You can change the strength of the blur by editing replacing `boxblur=20` with a larger/smaller value. The resolution used in this complex filter is 512x512. It is repeated three times in the command, so make sure you change all of them if you want a different resolution.

Explanation of the above complex filter:
- `[0:v]scale=512:512:force_original_aspect_ratio=increase,crop=512:512:(ow-iw)/2:(oh-ih)/2,boxblur=20[v1]`
  - Take the input [0:v], scale to the smallest possible size that fully contains a 512x512 box (while maintaining the aspect ratio), crop to 512x512 (centered), then box blur with strength 20. Save as [v1].
- `[0:v]scale=512:512:force_original_aspect_ratio=decrease[v2]`
  - Take another copy of the input [0:v], scale to the largest possible size that fully contains a 512x512 box (while maintaining the aspect ratio). Save as [v2].
- `[v1][v2]overlay=(main_w-overlay_w)/2:(main_h-overlay_h)/2[vid]`
  - Overlay [v2] over [v1] centered. Save as [vid]
- `-map [vid]` (outside of filter_complex)
  - The output video will use [vid].
