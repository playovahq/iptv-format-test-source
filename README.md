# IPTV format test source

A free test line for IPTV players. Each item is a 30-second clip of *Big Buck Bunny*
(Blender Foundation, CC BY 3.0) encoded in one stream format that real IPTV providers
send — 231 formats in all, from H.264 in MPEG-TS to HEVC Main 10 with Dolby Vision,
PGS subtitles and several audio tracks.

## Add it to any player

| | |
|---|---|
| Xtream Codes server | `https://demo.playova.app` |
| User name | `formats` |
| Password | `formats` |
| M3U playlist | `https://demo.playova.app/get.php?username=formats&password=formats&type=m3u_plus&output=ts` |
| XMLTV guide | `https://demo.playova.app/xmltv.php?username=formats&password=formats` |

`output=m3u8` in the M3U address gives the live MPEG-TS channels as HLS instead.

Every item is named after its format, for example:

```
MKV · HEVC Main 10 3840×1604 23.98 fps 10-bit HDR10 · E-AC-3 5.1 + AC-3 (3 tracks) · PGS + SRT subtitles (4)
```

The full list is in [`formats.csv`](formats.csv): 64 live channels and 167 films. The guide with
results on real devices is at https://playova.com/guides/format-testing/#test-source.

## What is covered

Containers MKV, MP4, MPEG-TS, HLS, AVI, FLV, MP3 and AAC; video H.264 (Baseline to High 4:4:4),
HEVC (Main, Main 10, RExt), AV1, VP9, VP8, MPEG-2, MPEG-4 Part 2 and older codecs; HDR10, HLG
and Dolby Vision profile 8.1; interlaced pictures; AAC (LC, HE, HE v2, LATM), AC-3, E-AC-3, DTS,
TrueHD, MP2, MP3, Opus, FLAC, PCM and WMA; SRT, ASS, WebVTT, MP4 text, PGS, DVB, DVD and teletext subtitles; Vorbis and AAC Main/LTP;
up to dozens of audio and subtitle tracks in one file.

## What is not

Formats that need a licensed encoder are left out rather than faked: Dolby Atmos (E-AC-3 JOC and
TrueHD), DTS-HD MA/HRA, DTS:X, DTS Express, 7.1 E-AC-3 and TrueHD, and VC-1, plus a few that free encoders cannot
reproduce exactly. [`missing.csv`](missing.csv) lists each one with the reason.

## How it was made

The formats come from a survey of real provider catalogues. Each clip was re-encoded from the
open film and then read back with ffprobe; a clip that did not read back as exactly the same
format was discarded. Bitmap subtitles were drawn and written as PGS, then converted to DVB and
DVD; teletext pages were written by our own EN 300 706 writer; Dolby Vision metadata was added with
dovi_tool.

Made with free and open-source tools: [FFmpeg](https://ffmpeg.org) (x264, x265, SVT-AV1, libvpx,
Opus, LAME), [Vorbis tools](https://xiph.org/vorbis/), [dovi_tool](https://github.com/quietvoid/dovi_tool),
[MKVToolNix](https://mkvtoolnix.download) and [Playwright](https://playwright.dev) for drawing subtitle bitmaps.

## Licence

The clips are cut from *Big Buck Bunny* (2008) by the Blender Foundation, licensed
[CC BY 3.0](https://creativecommons.org/licenses/by/3.0/). This README and the lists are CC0.
The test line carries no channels and no provider content.

Made by the developer of [Playova](https://playova.com), an IPTV player for your own sources.
The test line works with any player.
