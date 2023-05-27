# Things to look out for during BMS production

### Encode BMS files in SHIFT-JIS
If using ubmsc, go to Options -> General Options and change the Text Encoding option to SHIFT-JIS. This matters if you are using japanese or otherwise non-ASCII characters in your title/artist etc.

### Make sure your maximum grid partition is high enough in ubmsc
If you are using ubmsc for your charts and are getting the **"Warning: Note overlapping detected. Increasing Maximum Grid Partition will resolve this."** error, don't ignore it.

If you get this warning despite not having overlapping notes, you should go to `Options -> General Options` and increase "Max Grid Partition in BMS" to a large value like 10000. 


# Things to look out for before submission
This a checklist of things to watch out for when submitting a BMS.

### Do not submit an incomplete BMS
A BMS is incomplete if the keysounds have not been fully cut or there isn't at least one complete chart.

Sometimes, people try to register (aka submit) their BMS before it is done in order to get in before the deadline or to get their entry in a higher ranked position on the page (to make their entry more visible). They will then amend the download link later with the completed BMS.
Often, this goes against the rules of the event and will cause you to get disqualified.

Note that it is alright to add the BGA or additional charts later in an update. However this may mean that your BGA or additional charts won't make it into the initial song pack, so many players end up never having them.

### No keysound should exceed 60s in length
BMS with keysounds exceeding 60s in length are automatically blocked from LR2IR. Try to cut up keysounds where possible, even if they are not used in the chart. If you need to use long keysounds (e.g. vocal tracks), split them into \~40 segments.

### Zip the BMS in a folder
Do not place the your files directly into the zip. They should be placed in a folder, then zipped (like the example below).
```
songname.zip
 '-> songname
      '-> songnameN.bms
      '-> songnameH.bms
      '-> songnameA.bms
      '-> keysound1.ogg
      '-> keysound2.ogg
      '-> keysound3.ogg
      '-> keysound4.ogg
      '-> bga.wmv
```

### Do not use non-ASCII characters in your file names
This applies to both file and folder names. For example, use kyokumei.bms and gabberkick.ogg instead of 曲名.bms and ガバーキック.ogg.

### Please convert your keysounds to ogg
wav keysounds usually have ridiculously large file sizes. Use a tool like [oggdropXPd](https://www.rarewares.org/ogg-oggdropxpd.php) or [oggenc2](https://www.rarewares.org/ogg-oggenc.php) to convert the keysound files to ogg to reduce the total file size.

As a rough guide, try to keep the total size of your keysounds below 40MB if possible.

### Do not make separate BMS files for wav and ogg
It doesn't matter if you specify it as `#WAV01 keysound.wav` or `#WAV01 keysound.ogg`. If there is no keysound.wav in the folder, the BMS client will automatically load keysound.ogg instead.

Thus, you can convert the keysounds from wav to ogg while not changing the BMS.

### Use wmv or mpg for BGAs for LR2 compatibility
See [Video Encoding](video-encoding) for details on how to encode your BGAs. As a rough guide, please try to keep your BGA files within 40MB if possible.

If you are making an mp4 version of the BGA for beatoraja users, **do not make separate BMS files for the mp4 BGA**. Continue to specify the BGA as `_bga.wmv` (or `_bga.mpg`) in the BMS, and LR2 will load `_bga.wmv` (or `_bga.mpg`) while beatoraja will preferentially load`_bga.mp4` if it exists.

### Do not make a separate BMS file when updating a placeholder BGA
If the BGA has not been completed on time, you can use an image file (e.g. `_bga.png`) as a placeholder.

**Do not make separate BMS files for the placeholder/final versions of the BGA**. If you specify your BGA as `_bga.wmv` or `_bga.mpg` but there is no \_bga.wmv or \_bga.mpg in the folder, the game will load \_bga.png instead if it exists.

### Check if you have filled in your BMS metadata correctly
See [Chart Metadata Tips](#chart-metadata-tips) below.

### Avoid modifying BMS files after release
Every time you make any small change to a bms file (a chart), the file hash changes, so it is identified as a different chart.

If you modify a chart after release (even if it's like 30 minutes after release) and update your download link, it is often the case where there will be two different versions of your chart floating around - some people download your new version directly, while others will still have your old version (especially if your old version made it into the song pack which is often compiled immediately after release).
This can make it quite confusing for players down the road as people don't often update their chart versions.

Thus, it is good to check that you have done everything right before the initial release, so that an update to fix the charts won't be necessary down the road.

Note that updating the keysounds, the BGA, or adding new charts is completely fine as long as no edits are made to existing bms files.

### Check for errors using Anzu BMS Diff
This is a recommendation and isn't absolutely necessary.

When making charts of different difficulties using ubmsc, make sure that you have `Disable vertical moves (D)` checked when moving notes around. This is to prevent accidental upward/downward shifting of keysounds when charting.

Before submitting, use a BMS diff tool to check that your keysounds have not been shifted upward/downward by accident between charts. The diff tool can also be used to check that the metadata isn't different between charts (for example, specifying a stagefile in one chart but forgetting to do so in another).

- [Anzu BMS Diff](https://yuinore.net/2015/12/difftool/)
  - Search (ctrl+f) for "Anzu BMS Diff Toolをダウンロード" if you can't find the download link.
- [Online BMS diff tool](https://stairway.sakura.ne.jp/smalltools/minibmsplay/diff.htm)


# Chart Metadata Tips
- **Title**: Title of the song
- **Artist**: Composer name
- **Genre**: Genre of the music
- **Player**: Leave it as 1-Single Play. See [Play Modes](#play-modes) below for more information.
- **Rank**: Judge difficulty. Most people set it to `3 - Easy`. Avoid using Very Easy as LR2 does not support it.
- **Play Level**: Numerical level shown on the chart. See [Difficulty and Levels](#difficulty-and-levels) below for more information
- **SubTitle**: The subtitle is often used for the chart-specific name. For example, if your chart is named "My Song [SP INSANE]", My Song would be the title and [SP INSANE] would be the subtitle. It is not necessary to add a subtitle for beginner/normal/hyper/another charts.
- **SubArtist**: often used to credit the BGA and chart maker.
    - The chart maker is often specified with the prefix "obj: " or "obj. ". If no chart maker is specified, it is assumed that the composer made the chart.
- **Stage File**: A 640x480 thumbnail file (usually png) for your song that can be seen in the music select and score screens. It's not necessary to include one, but can help improve the visibility of your BMS.
- **Banner**: A 300x80 banner file (usually png) for your song that can be seen in the music select screen. Not commonly used as some skins don't even display the banner file.
- **Difficulty**: To specify BEGINNER, NORMAL, HYPER, ANOTHER or INSANE.
- **Total**: Remember to specify a TOTAL value for your charts. See [TOTAL Value](#total-value) below for more information on how to do so.
- **LnObj**: See [LNObj](#lnobj) below for more information on what this means.

### Difficulty and Levels
There are five difficulties you can set for a chart. BEGINNER, NORMAl, HYPER, ANOTHER and INSANE.

Difficulty levels are on a scale of 1-12. These are called the normal scale levels and are used for BEGINNER, NORMAL, HYPER and ANOTHER charts. However, if you label the chart as INSANE, it may be assumed to use a different scale (1-25, where insane 1 is above normal 12).

See [this link](https://github.com/wcko87/beatoraja-english-guide/wiki/Difficulty-Tables#difficulty-rating-system) for a reference on difficulty levels.

### Play Modes
The most common playmode is 7keys (which includes the scratch).
- If you only use the leftmost 5 lanes, your chart will be detected as a 5keys chart.
- If you use any of the additional 7 lanes that are used in 14keys, the chart will be detected as a 14keys chart.
- If you want your chart to be detected as a 9keys (pms) chart, use the extension .pms instead of .bms.

### TOTAL Value
Remember to set a TOTAL value. The TOTAL value determines the speed of gauge (hp) recovery when playing on the easy or normal gauges in game. Having a higher TOTAL makes the chart easier to clear.

For example, if you have a TOTAL value of 400 on the normal gauge, you will recover 400% gauge in total if you hit every note with at least a GREAT (another way of seeing it is that you recover 400/(number of notes) per note).

If you are not sure what to set your TOTAL value to, use the [BMS #TOTAL Calculator](https://hitkey.nekokan.dyndns.info/total.htm), input your song's notecount, and use the value in IIDX #TOTAL supposition 1.

If the TOTAL value is not set, the TOTAL value will be automatically set by the game, but this automatic value may be different depending on which bms client the player is using (LR2, beatoraja).

### LNObj
BMS charts have multiple LN formats because of competing implementations of LN support in the early days of the format. Assuming that you are using ubmsc for charts, I personally recommend keeping it as "None (#LnType 1)".
- This option has no effect on gameplay. It only affects how LN format in the .bms file.
- Using "None (#LnType 1)" treats an LN as a single note of a different type. This is the simplest to work with. Use SHIFT+drag in ubmsc to convert a note between a regular note and a long note.
- If it is set to any other option, then each LN is made out two notes - a regular note and an LN ending note. For example, let's say LnObj is set to "ZZ". Then objects of label ZZ will be used to designate the endings of long notes.


### Preview File
You can specify a preview file for your BMS by adding this to the expansion code:
```
#PREVIEW preview.wav
```
Where preview.wav (or preview.ogg) is the file name of your preview file. Record a short highlight clip of your song to use as the preview file.

If you are using beatoraja, the preview file will play when you hover over the song during music select. This can help increase your song's visibility.



# Charting Tips
Charts in general can be very subjective. But there are some pointers (you don't have to follow them always!) that you might want to take note of:
1. The scratch key is not an 8th note ([video example of how scratches typically look](https://www.youtube.com/watch?v=nFnoSCTNWY0))
2. The scratch key is usually bound to vocal samples, scratch sounds, or cymbal crashes. Using piano notes as scratches may feel odd.
3. Try to keep the kick drum on a consistent key (key 1 is the most popular). It's okay to swap the kick lane around during the chart, but it may feel awkward if the kick keysounds is spread over arbitrarily lanes, especially if it's a consistent kick every 4/4 beat). I sometimes swap the kick key every 4 or 8 measures.
4. Long scratch notes on a controller requires the player to use a hand to constantly rotate the turntable. Beware of potential impossible patterns that can result from improper use of these.
5. Please test play the chart or get someone else to test play them if you are unable to.
