HDRTools
========

# 1. Example: convert yuv420p 10bit YUV to tiff

Use the `HDRTools/bin/HDRConvertYCbCr420ToTiff.cfg`, specify input and output
file in it, then run:

```shell
$ ./HDRConvert -f HDRConvertYCbCr420ToTiff.cfg
```

# 2. Configuration Files
## 2.1. convert EXR to other format

  * `HDRTools/bin/HDRConvert.cfg`

    exr 12bit BT.2020 --> yuv420p 10bit BT.2020 (PQ)

  * `HDRTools/bin/HDRConvert8.cfg`

    exr 12bit BT.2020 --> yuv420p 8bit BT.2020 (PQ)

  * `HDRTools/bin/HDRConvertAVI8.cfg`

    exr 10bit BT.2020 --> avi/yuv420p 8bit BT.2020 (PQ)

  * `HDRTools/bin/HDRConvertBT2020EXRToICtCp.cfg`

    exr 12bit BT.2020 --> avi/yuv420p 10bit **ICtCp** (Dolby) (PQ)

    **TODO: ICtCp??**

  * `HDRTools/bin/HDRConvertEXR.cfg`

    exr 10bit BT.709 **CM_RGB** --> exr 10bit 444 BT.709 **CM_YUV**

    **TODO: ???**


  * `HDRTools/bin/HDRConvertEXR2.cfg`

     exr 12bit BT.2020 444 --> exr 10bit 444 **P3D56**

     **TODO: P3D56**


  * `HDRTools/bin/HDRConvertHLGToEXR.cfg`

    exr 12bit BT.2020 --> yuv420p 10bit BT.2020 (TF_HLG)

  * `HDRTools/bin/HDRConvertRGB8.cfg`

    exr 10bit BT.2020 --> yuv420p 8bit BT.2020 (PQ)

  * `HDRTools/bin/HDRConvertToTiff.cfg`

    exr 10bit BQ.2020 (PQ) --> tiff 16bit BT.2020 (PQ)

  * `HDRTools/bin/HDRConvertUYVY.cfg`

    exr 10bit BT.2020 --> avi/yuv 8bit BT.2020 (PQ)

  * `HDRTools/bin/HDRConvertV210.cfg`

    exr 12bit BT.2020 --> avi/yuv 10bit BT.2020 (PQ)

## 2.2. convert TIF to other format
  * `HDRTools/bin/HDRConvertBT2020TiffToICtCp.cfg`

    tiff BT.2020 12bit --> yuv420p 10bit ICtCp (Dolby) (PQ)

  * `HDRTools/bin/HDRConvertDPX.cfg`

    tiff BT.2020 10bit (PQ) --> yuv420p 10bit BT.2020 (PQ)

  * `HDRTools/bin/HDRConvertTiff.cfg`

    tiff 10bit BT.2020 (PQ) --PQ--> exr 10bit BT.2020

  * `HDRTools/bin/HDRConvertTiff2.cfg`

    tiff 10bit BT.2020 (PQ) --> exr 10bit BT.2020 (PQ)

## 2.3. convert YUV to other format
  * `HDRTools/bin/HDRConvertHLGToEXR.cfg`

    yuv420p 10bit BT.2020 (TF_HLG) --> exr 8bit BT.2020

  * `HDRTools/bin/HDRConvertICtCpToBt2020EXR.cfg`

    yuv420p 10bit iCtCp (PQ) --> exr 12bit BT.2020

  * `HDRTools/bin/HDRConvertICtCpToBt2020Tiff.cfg`

    yuv420p 10bit iCtCp (PQ) --> tif 12bit BT.2020 (PQ)

  * `HDRTools/bin/HDRConvertToEXR.cfg`

    yuv420p 10bit (PQ) --> exr 10bit BT.2020

  * `HDRConvertYCbCr420ToTiff.cfg`

    yuv420p 10bit BT.2020 (PQ) --> tiff 12bit BT.2020 (PQ)

  * `HDRConvertYUV.cfg`

    yuv420p 10bit BT.2020 (PQ) --> yuv444 10bit BT.2020 (PQ)

## 2.4 Some Configuration Parameters
1. FourCCCode

  https://www.fourcc.org/yuv.php

  ```shell
  PF_UNKNOWN = -1,     //!< Unknown color ordering
  PF_UYVY    =  0,     //!< UYVY (YUV 4:2:2 ,U and V sampled at every second pixel horizontally on each line)
  PF_YUY2    =  1,     //!< YUY2 (YUV 4:2:2 as for UYVY but with different component ordering within the u_int32 macropixel.)
  PF_YUYV    =  2,     //!< YUYV (Duplicate of YUY2)
  PF_YVYU    =  3,     //!< YVYU (YUV 4:2:2 as for UYVY but with different component ordering within the u_int32 macropixel.)
  PF_BGR     =  4,     //!< BGR
  PF_RGB     =  5,     //!< RGB
  PF_V210    =  6,     //!< V210 (planar 10-bit 4:2:2 YCrCb)
  PF_UYVY10  =  7,     //!< UYVY10
  PF_V410    =  8,     //!< V410 (10 bit Packed YUV 4:4:4)
  PF_R210    =  9,     //!< R210 (10 bit RGB)
  PF_R10K    =  10,    //!< R10K
  PF_XYZ     =  11,    //!< XYZ
  ```

  **`SourceFourCCCode` needs to be configured only if `SourceChromaFormat` is
  `422` or `444`.**
