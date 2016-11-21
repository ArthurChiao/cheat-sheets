HDRTools
========

1. convert yuv420p 10bit YUV to yuv444b 10bit

  Use the `HDRTools/bin/HDRConvertYUV.cfg`, change the input and out file
  names in it:

  ```shell
  $ ./HDRTools -f HDRConvertYUV.cfg
  ```

  View the input and out files with vooya.

1. convert yuv420p 10bit YUV to tiff

  Use the `HDRTools/bin/HDRConvertYCbCr420ToTiff.cfg`, change the input
  and out file names in it:

  ```shell
  $ ./HDRTools -f HDRConvertYCbCr420ToTiff.cfg
  ```
1. yuv420p 10bit to exr

  `HDRTools/bin/HDRConvertToEXR.cfg`


1. exr to avi/yuv

  `HDRTools/bin/HDRConvertV210.cfg`

1. exr to avi/yuv

  `HDRTools/bin/HDRConvertUYVY.cfg`

1. exr to tiff

  `HDRTools/bin/HDRConvertToTiff.cfg`

1. tiff to exr

  `HDRTools/bin/HDRConvertTiff.cfg`

1. tiff to yuv444p 10bit

  `HDRTools/bin/HDRConvertTiff2.cfg`

1. exr to yuv420p 8bit

  `HDRTools/bin/HDRConvertRGB8.cfg`

1. yuv420p 10bit ictcp to 444_bt2020 tiff

  `HDRTools/bin/HDRConvertICtCpToBt2020Tiff.cfg`

1. yuv420p 10bit ictcp to 444_bt2020 exr

  `HDRTools/bin/HDRConvertICtCpToBt2020EXR.cfg`

1. yuv420p 10bit to exr

  `HDRTools/bin/HDRConvertHLGToEXR.cfg`

1. 444 bt2020 exr to yuv420p 10bit

  `HDRTools/bin/HDRConvertHLGToEXR.cfg`

1. yuv420p 10bit bt709 to 444 bt709 exr

  `HDRTools/bin/HDRConvertEXR.cfg`


1. 444 bt2020 exr 444 P3D56 exr

  `HDRTools/bin/HDRConvertEXR2.cfg`


1. 709 tif to 444 10bit yuv

  `HDRTools/bin/HDRConvertDPX.cfg`


1. bt2020 tiff to yuv420p 10bit
  `HDRTools/bin/HDRConvertBT2020TiffToICtCp.cfg`

1. bt2020 exr to yuv420p 10bit

  `HDRTools/bin/HDRConvertBT2020EXRToICtCp.cfg`


1. ct2020 exr to 420p 8bit avi/yuv

  `HDRTools/bin/HDRConvertAVI8.cfg`

1. ct2020 exr to 420p 8bit UYVY

  `HDRTools/bin/HDRConvert8.cfg`

1. ct2020 exr to 420p 10bit UYVY

  `HDRTools/bin/HDRConvert.cfg`
