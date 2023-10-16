# AIOT_Speaker
AI TTS 음성합성 기술을 활용하여 IOT 스피커로 출력

# PROJECT DESCRIPTION
## Overview
Voice technology has many applications in the modern world. Consumers have come to expect voice interactions in smartphones, home devices, and services. In addition, a project that uses AI to learn the voices of popular singers to recreate their songs has recently attracted attention. Based on these trends, we have started a new project using WIZnet IoT speaker with AI TTS technology and singer voice recreation technology.  

**The following is the original description, not mine. I used it because it is more descriptive.**  

## [IOT SPEAKER](https://github.com/chcbaram/wiznet-iot-speaker)
<img width="934" alt="스크린샷 2023-10-16 오후 2 37 21" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/3e77584e-7f89-41df-b1c6-a98904b6d533">

[Buy Device](https://smartstore.naver.com/higenis/products/9179803239)

**Hopefully you can utilize the above devices and github code to build your own IOT speaker.**

## AI Solution

### Requirements
- mp3 file original
- CUDA GPU or Colab Pro
- pretrained artist voice
- ChatGPT
- Bandlab
- GaudiStudio

### Making

The first step is to download an MP3 file of the music you want and split the instrumental and vocals in GAUDIO STUDIO.  
<img width="759" alt="스크린샷 2023-10-16 오후 2 41 35" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/5977b46a-553e-4c44-aa92-c3d3afb6ec65">
If you go to the RVC v2 docs and read through them, there are a lot of different values for hyperparameters and a lot of different source code. In fact, the author and others have done a lot of parameter tuning experiments, so it's best to use the default values.  
<img width="597" alt="스크린샷 2023-10-16 오후 2 41 53" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/b1894504-b8c6-456b-99eb-d03b2ce7b67e">
