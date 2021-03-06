FFmpeg Cheat-Sheet
================

# 1. decode
1. Decode to yuv

    | parameter | effect |
    | :------ | :------|
    | `-i <input_file>` | specify input file, could be any media format |
    | `-t <seconds>` | how many seconds to decode |

    ```shell
    # decode 1.5 seconds, from start
    $ ffmpeg -i in.mkv -t 1.5 out.yuv
    ```

# 2. Audio

1. extract audio clip

    Extract the first 15s of input.mp3:

    ```shell
    $ ffmpeg -ss 0 -t 15 -i input.mp3 out.mp3

    # save to wav format instead of mp3
    $ ffmpeg -ss 0 -t 15 -i input.mp3 out.wav
    ```

1. Speedup / Slow down audio/video

    [wiki:How to speed up / slow down a video](https://trac.ffmpeg.org/wiki/How%20to%20speed%20up%20/%20slow%20down%20a%20video)

    ```shell
    # double speed of audio
    $ ffmpeg -i input.mkv -filter:a "atempo=2.0" -vn output.mkv

    # slow down speed of audio
    $ ffmpeg -i input.mkv -filter:a "atempo=0.5" -vn output.mkv

    # atempo is between 0.5~2.0, to get out of this limit, you can chain multiple
    # "atempo=2.0"
    $ ffmpeg -i input.mkv -filter:a "atempo=2.0,atempo=2.0" -vn output.mkv
    ```

    **for video:**
    ```shell
    # speed up by 2 times
    $ ffmpeg -i input.mkv -filter:v "setpts=0.5*PTS" output.mkv

    # slow down by 20 times
    $ ffmpeg -i input.mkv -filter:v "setpts=20.0*PTS" output.mkv

    # speedup both audio & video by 2 times
    # `add -strict experimental` for workaround `aac` encoding warning
    $ ffmpeg -i the_3rd_polar.mp4 -strict experimental -filter:a "atempo=2.0"  \
    -filter:v "setpts=0.5*PTS" the_3rd_polar_speedup_x2.mp4
    ```
