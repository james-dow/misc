# How to convert MKV video with subtitles to MP4 + SRT on MacOS

Using [mkvtoolnix](https://en.wikipedia.org/wiki/MKVToolNix) and [MP4Box](https://github.com/gpac/gpac/wiki/MP4Box).

Tested on MacOS Catalina 10.15.6.

## Installation

```bash
brew install mkvtoolnix
brew install MP4Box
```

## Common case

Firstly you need to extract tracks from source file with conforming extension. Extensions is used by MP4Box for determining incoming format.

```bash
mkvmerge -i s01e01.mkv
```

Output be like:
```
File 's01e01.mkv': container: Matroska
Track ID 0: video (MPEG-4p10/AVC/H.264)
Track ID 1: audio (AC-3)
Track ID 2: audio (AC-3)
Track ID 3: subtitles (SubRip/SRT)
Track ID 4: subtitles (SubRip/SRT)
```

Accordingly to the track information here you can choose right file extension for export, like:

```bash
mkvextract tracks s01e01.mkv 0:s1e1.h264 2:s1e1.en.ac3 3:s1e1.ru.srt 4:s1e1.en.srt
```

Then just build `.mp4` like:
```bash
MP4Box -add s1e1.h264 -add s1e1.ac3 -new s1e1.mp4
```

or

```bash
MP4Box -add s1e1.h264 -add s1e1.ac3 -add s1e1.en.srt:lang=eng -new s1e1.mp4
```
