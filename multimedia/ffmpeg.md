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
