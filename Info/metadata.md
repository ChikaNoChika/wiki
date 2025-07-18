---
label: "Metadata"
icon: three-bars
order: 1800
---

# Metadata

Torrents must include specific metadata, such as sub level, video type, codec, and languages.

### Sub Levels

See the [Sub Levels](/info/sub-levels) page for details.

### Video Type

The **Video Type** tag indicates the video's source and any encoding applied.

| Type         | Description                                                                 | ID  |
|--------------|-----------------------------------------------------------------------------|-----|
| Hybrid       | An encode using various sources, most commonly WEB and BD.                  | 15  |
| BD - Remux   | Untouched, decrypted Blu-ray Disc copy in a playable format (mkv, mp4, etc).| 14  |
| BD - Encode  | An encode of the raw Blu-ray Disc.                                          | 13  |
| BD - Mini    | Blu-ray Disc encode with reduced quality to save space.                     | 12  |
| BD - BDMV    | Blu-ray Disc in the BDMV structure.                                         | 11  |
| BD - ISO     | Blu-ray Disc ISO image.                                                     | 10  |
| BD - ISO (Unpacked) | An unpacked Blu-ray Disc ISO image.                                  | 16  |
| WEB - Raw    | Direct copy from a streaming service (WEB-DL).                              | 9   |
| WEB - Encode | Re-encode of the WEB source.                                                | 8   |
| WEB - Mini   | WEB source encode with reduced quality to save space.                       | 7   |
| DVD - Encode | An encode of a DVD.                                                         | 6   |
| DVD - Remux  | Direct copy of a DVD in a playable format.                                  | 5   |
| TV - Raw     | Direct copy of a TV broadcast.                                              | 4   |
| TV - Encode  | TV broadcast, re-encoded.                                                   | 3   |
| Laserdisc    | Laserdisc source in a playable format.                                      | 2   |
| VHS          | VHS source in a playable format.                                            | 1   |
| Other        | Other source; see torrent description for details.                          | 0   |


### Video Codec

The **Video Codec** tag indicates the codec used for the video.

| Codec   | Description                        | ID  |
|---------|------------------------------------|-----|
| H264    | AVC, x264                          | 1   |
| H265    | HEVC, x265                         | 2   |
| AV1     | AV1                                | 3   |
| VP9     | VP9                                | 4   |
| MPEG-2  | MPEG-2                             | 5   |
| MPEG-4  | MPEG-4, but not Part 10/H264       | 6   |
| WMV     | Windows Media Video                | 7   |
| Other   | Other                              | 8   |


### Languages

There are 3 language tags: **Audio**, **Fansub**, and **Subtitle**.
- **Audio**: The language of the audio track(s).
- **Fansub**: The language of the fansub track(s).
- **Subtitle**: The language of any subtitle tracks from official sources.

You can choose any language from the [ISO 639 Set 1](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) list, Filipino (`fil`) and English Weeb (`enm`).


### MTL (Machine Translation)

The **MTL** tag indicates that the release uses machine translation for their fansubs.


### Auto Titles

The auto title is used by automation software (Sonarr, Radarr). It contains the title of the torrent, and a set of tags at the end, allowing users to add Custom Formats in their automation software to filter out and prioritize different releases, based on their preferences.

The possible tags that can be used in the auto title are:
- `MTL`: Machine Translation
- `L`: Sub level
- `V`: Video type
- `C`: Video codec
- `A`: Audio language
- `F`: Fansub language
- `S`: Subtitle language

#### Example:

Here is an example of an auto title:
```
[RandomGroup] Sousou no Frieren - 01-16 (WEB 1080p) {Tags:L3;V8;C2;A-ja;F-en;S-en,fr,es;}
``` 

Lets break it down:
- `L3`: Sub level 3
- `V8`: Video type 8 (WEB - Encode)
- `C2`: Video codec 2 (H265)
- `A`: Audio languages:
    - `ja`: Japanese
- `F`: Fansub languages:
    - `en`: English
- `S`: Subtitle languages:
    - `en`: English
    - `fr`: French
    - `es`: Spanish

So from these tags, we can conclude that this is a Sub Level 3 release, encoded from a WEB source, using H265 codec, with Japanese audio, English fansubs, and English, French, and Spanish subtitles from official sources.

You might ask, "How is this useful?"<br>
Now, in Sonarr/Radarr, we can create Custom Formats to prioritize releases based on their tags.

Let's say we only want to download releases containing English fansubs that are at least Sub Level 2.<br>
We can create a Custom Format with the following rules:
- Release Title matches the regex: `{Tags:.*L[2-9];.*}` (Sub Level 2 or higher)
- Release Title matches the regex: `{Tags:.*F-[^;]*\b(en)\b[^;]*\b.*}` (Fansub tag contains "en")

These regex's might look complicated, but we have a guide you can follow [here](/info/sonarr-radarr#3-optional-add-custom-formats) to help you out.
