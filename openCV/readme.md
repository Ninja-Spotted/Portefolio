---
title: "OpenCV"
permalink: "/opencv"
layout: default
---


## OpenCV

OpenCV is an open-source computer vision and machine learning software library, aiming at providing a common infrastructure for accelerating the design of CV applications. OpenCV library provide basic tools for building CV applications, building on over 2500 optimized algorithms, including state-of-the-art computer vision and machine learning algorithms for a panoply of applications. Detecting and recognizing faces, classifying human actions in videos, track camera movements and moving objects, extracting 3D models of objects, producing 3D point clouds from stereo cameras, removing red eyes photos, following eye movements are just a few examples.

### Introduction

This document aims at introducing the concept of Computer Vision and some basic functionality of the OpenCV – Open Source Computer Vision Library, through a few illustrative examples building on its C++ libraries.  
In broad terms, Computer Vision comprises data acquisition (involving still images or video stream, sometimes mixed with audio), data compression, processing and classification, towards a (computer-based) decision or a new representation of the data. Note that Computer Vision relies on a binary representation of the data.  
\
OpenCV has C++, Python, Java and MATLAB interfaces and supports Windows, Linux, Android and Mac OS. In this case, C++ was opted to create the colour histogram of an image.

### Instalation

The installation is based on Debian 9 (Stretch), but should work in any other Debian-based OS. Firstly, do:

        sudo apt update
        sudo apt install build-essential
        sudo apt install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
        sudo apt install libopencv-dev python3-opencv
        
When compiling the C++ programs use: `g++ test.cpp –o test `pkg-config --cflags --libs opencv``

### Example 1: Loading an image file and visualizing it on screen

For this the program loads an image through a path and opens a window named `program1`, outputting the image:

        #include “opencv2/opencv.hpp”
        #include <iostream>
        
        using namespace cv;
        
        int main(int argc, char ** argv) {
          Mat img = imread(argv[1], -1);
          if (img.empty()) return -1;
          namedWindow("Program1", cv::WINDOW_AUTOSIZE);
          imshow("Program1", img);
          waitKey(0);
          destroyWindow("Program1");
          return 0;
        }
        
A ok




