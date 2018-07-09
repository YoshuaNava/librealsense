# NOTE: This repository has been modified to support catkin.

**Changes compared to the official librealsense2 package:**

- Renamed package librealsense2 to any_librealsense2 (avoid name conflicts when installing from ppa).
- Renamed folder include/librealsense2 to include/any_librealsense2 (avoid name conflicts when installing header files)
- Renamed executables in examples, tools, unit-tests and wrappers (avoid conflicts when installing official and any librealsense2)

<p align="center"><img src="doc/img/realsense.png" width="70%" /><br><br></p>

-----------------

Linux/MacOS | Windows |
-------- | ------------ |
[![Build Status](https://travis-ci.org/IntelRealSense/librealsense.svg?branch=development)](https://travis-ci.org/IntelRealSense/librealsense) | [![Build status](https://ci.appveyor.com/api/projects/status/6u04bgmpwfejpgo8?svg=true)](https://ci.appveyor.com/project/dorodnic/librealsense-s4xnv) |

-----------------

## Overview
**Intel® RealSense™ SDK 2.0** is a cross-platform library for Intel® RealSense™ depth cameras (D400 series and the SR300). 

> :pushpin: For other Intel® RealSense™ devices (F200, R200, LR200 and ZR300), please refer to the [latest legacy release](https://github.com/IntelRealSense/librealsense/tree/v1.12.1).

The SDK allows depth and color streaming, and provides intrinsic and extrinsic calibration information.
The library also offers synthetic streams (pointcloud, depth aligned to color and vise-versa), and a built-in support for [record and playback](./src/media/readme.md) of streaming sessions.

Developer kits containing the necessary hardware to use this library are available for purchase at [realsense.intel.com/buy](https://realsense.intel.com/buy).
Information about the Intel® RealSense™ technology at [realsense.intel.com](https://realsense.intel.com)

> :open_file_folder: Don't have access to a RealSense camera? Check-out [sample data](./doc/sample-data.md)

## Download and Install
* **Download** - The latest releases including the Intel RealSense SDK, Viewer and Depth Quality tools are available at: [**latest releases**](https://github.com/IntelRealSense/librealsense/releases). Please check the [**release notes**](https://github.com/IntelRealSense/librealsense/wiki/Release-Notes) for the supported platforms, new features and capabilities, known issues, how to upgrade the Firmware and more.

* **Install** - You can also install or build from source the SDK (on [Linux](./doc/distribution_linux.md) \ [Windows](./doc/distribution_windows.md) \ [Mac OS](doc/installation_osx.md)), connect your D400 depth camera and you are ready to start writing your first application.

> **Support & Issues**: If you need product support (e.g. ask a question about / are having problems with the device), please check the [FAQ & Troubleshooting](https://github.com/IntelRealSense/librealsense/wiki/Troubleshooting-Q%26A) section.
> If not covered there, please search our [Closed GitHub Issues](https://github.com/IntelRealSense/librealsense/issues?utf8=%E2%9C%93&q=is%3Aclosed) page,  [Community](https://communities.intel.com/community/tech/realsense) and [Support](https://www.intel.com/content/www/us/en/support/emerging-technologies/intel-realsense-technology.html) sites.
> If you still cannot find an answer to your question, please [open a new issue](https://github.com/IntelRealSense/librealsense/issues/new).

## What’s included in the SDK:
| What | Description | Download link|
| ------- | ------- | ------- |
| **[Intel® RealSense™ Viewer](./tools/realsense-viewer)** | With this application, you can quickly access your Intel® RealSense™ Depth Camera to view the depth stream, visualize point clouds, record and playback streams, configure your camera settings, modify advanced controls, enable depth visualization and post processing  and much more. | [**Intel.RealSense.Viewer.exe**](https://github.com/IntelRealSense/librealsense/releases) |
| **[Depth Quality Tool](./tools/depth-quality)** | This application allows you to test the camera’s depth quality, including: standard deviation from plane fit, normalized RMS – the subpixel accuracy, distance accuracy and fill rate. You should be able to easily get and interpret several of the depth quality metrics and record and save the data for offline analysis. |[**Depth.Quality.Tool.exe**](https://github.com/IntelRealSense/librealsense/releases) |
| **[Other Debug Tools](./tools/)** | Device enumeration, FW logger, etc as can be seen at the tools directory | Included in [**Intel.RealSense.SDK.exe**](https://github.com/IntelRealSense/librealsense/releases)|
| **[Code Samples to Start Prototyping Quickly](./examples)** |These simple examples demonstrate how to easily use the SDK to include code snippets that access the camera into your applications. Check some of the [**C++ examples**](./examples) including capture, pointcloud and more and basic [**C examples**](./examples/C) | Included in [**Intel.RealSense.SDK.exe**](https://github.com/IntelRealSense/librealsense/releases) |
| **[Wrappers](https://github.com/IntelRealSense/librealsense/tree/development/wrappers)** | [Python](./wrappers/python), [.NET](./wrappers/csharp), [Node.js](./wrappers/nodejs) API, as well as integration with the following 3rd-party technologies: [ROS](https://github.com/intel-ros/realsense/releases), [LabVIEW](./wrappers/labview), [OpenCV](./wrappers/opencv), [PCL](./wrappers/pcl), [Unity](./wrappers/unity), and more to come, including Matlab and OpenNI. | |


## Ready to Hack!

Our library offers a high level API for using Intel RealSense depth cameras (in addition to lower level ones).
The following snippet shows how to start streaming frames and extracting the depth value of a pixel:

```cpp
// Create a Pipeline - this serves as a top-level API for streaming and processing frames
rs2::pipeline p;

// Configure and start the pipeline
p.start();

while (true)
{
    // Block program until frames arrive
    rs2::frameset frames = p.wait_for_frames(); 
    
    // Try to get a frame of a depth image
    rs2::depth_frame depth = frames.get_depth_frame(); 

    // Get the depth frame's dimensions
    float width = depth.get_width();
    float height = depth.get_height();
    
    // Query the distance from the camera to the object in the center of the image
    float dist_to_center = depth.get_distance(width / 2, height / 2);
    
    // Print the distance 
    std::cout << "The camera is facing an object " << dist_to_center << " meters away \r";
}
```
For more information on the library, please follow our [examples](./examples), and read the [documentation](./doc) to learn more.

## Contributing
In order to contribute to Intel RealSense SDK, please follow our [contribution guidelines](CONTRIBUTING.md).

## License
This project is licensed under the [Apache License, Version 2.0](LICENSE). 
Copyright 2017 Intel Corporation
