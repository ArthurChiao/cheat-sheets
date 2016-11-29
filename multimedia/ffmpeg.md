FFmpeg Cheat-Sheet
================

# 1. decode
1. Decode to yuv

  | parameter | effect |
  | `-i <input_file>` | specify input file, could be any media format |
  | `-s <N>` | how many seconds to decode |


  ```shell
  # decode 1.5 seconds, from start
  $ ffmpeg -i in.mkv -s 1.5 out.yuv
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
