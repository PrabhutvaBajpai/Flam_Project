# 🔥 Real-Time Edge Detection Viewer (Android + OpenCV C++ + OpenGL ES + Web Viewer)

This project is a **real-time camera processing application** built for an RnD assessment.  
It integrates **Android Camera2**, **JNI**, **OpenCV (C++)**, **OpenGL ES**, and a small **TypeScript Web Viewer**.

The objective is to capture camera frames on Android, process them natively using OpenCV C++,  
render the output through OpenGL ES, and expose a processed sample frame to a web-based viewer.

---

## 🚀 Features Implemented

### ✅ Android App (Kotlin + C++)
- Live camera feed using **Camera2 API**
- Frame capture using **ImageReader**
- JNI bridge for sending frames to native C++
- Native processing using **OpenCV (C++)**
  - Grayscale filter
  - Canny Edge Detection
- Rendering processed output using **OpenGL ES 2.0**
- Ability to save processed sample frames for the web viewer

### ✅ Native C++ (JNI + OpenCV)
- Efficient `cv::Mat` conversion from YUV → RGBA
- Canny edge detection pipeline
- Returning processed bytes back to Kotlin
- Integration with `CMakeLists.txt` for OpenCV native bindings

### ✅ Web Viewer (TypeScript + HTML)
- Minimal TypeScript web page
- Loads a processed sample frame (PNG/JPEG)
- Basic UI overlay (resolution/FPS text placeholder)

---

## 📁 Project Structure

app/
├── src/main/java/ # Kotlin sources (Camera2, UI, JNI calls)
├── src/main/res/ # Layouts, drawables
├── src/main/jni/ # Native C++ code (OpenCV processing, JNI)
├── src/main/gl/ # OpenGL ES renderer (textures, shaders)
├── src/main/assets/ # (optional) Shaders or debug assets

web/
├── index.html # Minimal web UI
├── viewer.ts # Script to display processed frame
├── tsconfig.json # TS compiler settings
└── images/
└── sample.png # Saved processed frame from app

gradle/ # Gradle wrapper
build.gradle # Project-level build config
settings.gradle # Module linking
README.md # Project documentation


---

## 🧠 Architecture Overview

### 1️⃣ Camera Feed (Android)
- Using **TextureView** to display camera preview
- Using **Camera2 API** to capture frames
- The `ImageReader` receives YUV frames

### 2️⃣ JNI Bridge
- Frame bytes are passed to C++ using:
```kotlin
external fun processFrame(bytes: ByteArray, width: Int, height: Int): ByteArray
