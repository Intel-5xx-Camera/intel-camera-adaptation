# Intel-Camera-Adaptation

_intel-camera-adaptation_ contains the user space components to enable the use of MIPI camera that are not distributed as source code.

## camera3hal
This library implements the android v3 camera HAL interface. Module API version 2.3, device API version 3.2. For more details on this interface check android official documentation:

- [Interface header](http://androidxref.com/6.0.1_r10/xref/hardware/libhardware/include/hardware/camera3.h)
- [Metadata documentation](http://androidxref.com/6.0.1_r10/xref/system/media/camera/docs/docs.html)

The intel-camera-dev-support package provides source code examples on how to use this library. It also provides a wrapper library to use a gstreamer camera source on top of this library.

This library depends on other libraries also present in this repository:

### cameralibs
Internal support libraries for the HAL. Encapsulates the following functionality
- Parsing of Non Volatile Memory records from sensor internal memory. This is normally used to store calibration data that is specific for a particular sensor part.
- Parsing of binary record based data in tuning file.

### libiacss
Required by camera HAL library. It implements a generic pipeline framework that exposes the Intel IPU
as a graph of nodes from sensor to final sinks. Not usable directly.

### libiaimaging
Required by camera HAL library. The libraries in this folder implement the Intel 3A+ algorithms. These include:
- Auto Exposure
- Auto White Balance
- Auto Focus
- The + in 3A+ is a set of other algorithms that improve these 3 basic algorithms.

## aiqb
The files in this directory contain the binary tuning files produced by Intel IQ-Studio. These are binary files that contain tunning values for the ISP pipeline and 3A algotrithms.
Creating these files is almost a form of art since some of the choices are subjective.
CameraHAL requires a tuning file to properly expose RAW sensors.

## fw-ipu4
This directory contain the binary blobs that implement the FW that the Intel IPU execute.
These FW executable are loaded by the kernel driver.

## pvl-libs
This directory contains the libraries that implement the Photographic Vision Libraries:
- Face Detection (FD),
- Face Recognition (FR)

Two components depend on these libraries:
- The Camera HAL library, since the android interface defines metadata to expose the FD
- The PVL gstreamer filters that exposes each of the algorithms in isolation. These gstreamer elements are available as source code in the intel-camera-dev-support repository.

# Dependencies

https://github.com/01org/meta-intel-camera

https://github.com/01org/intel-camera-drivers

https://github.com/Intel-5xx-Camera/intel-camera-dev-support
