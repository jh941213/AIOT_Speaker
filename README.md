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
<img width="600" alt="스크린샷 2023-10-16 오후 2 41 35" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/5977b46a-553e-4c44-aa92-c3d3afb6ec65">
If you go to the RVC v2 docs and read through them, there are a lot of different values for hyperparameters and a lot of different source code. In fact, the author and others have done a lot of parameter tuning experiments, so it's best to use the default values.  
<img width="600" alt="스크린샷 2023-10-16 오후 2 41 53" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/b1894504-b8c6-456b-99eb-d03b2ce7b67e">
Find a link where a trained model of the singer you want has been saved and downloaded, either from a place with a lot of AI models like Hugging Face or through a community.
<img width="600" alt="스크린샷 2023-10-16 오후 2 43 34" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/04b0b420-2729-4b89-b71b-4ce894ca48fc">
You can do this by running the colab code in the RVC v2 docs straight through.

#### how to training?
<img width="600" alt="스크린샷 2023-10-16 오후 2 43 54" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/ed250a0a-52fa-464f-97f7-18ba7dbed521">


```python
# Model load
url = 'https://huggingface.co/leeloli/rosiesoft/resolve/main/rosiesoft.zip'  #@param {type:"string"}
model_zip = urlparse(url).path.split('/')[-2] + '.zip'
model_zip_path = '/content/zips/' + model_zip
```

Find the trained model of the singer you want and put the link to the model's save location in the URL.

```python
import os
import time
import fileinput
from subprocess import getoutput
import sys
from IPython.utils import capture
from IPython.display import display, HTML, clear_output
%cd /content/Retrieval-based-Voice-Conversion-{reeee}UI/

#@markdown Keep this option enabled to use the simplified, easy interface.
#@markdown <br>Otherwise, it will use the advanced one that you see in the YouTube guide.
ezmode = True #@param{type:"boolean"}
#@markdown You can try using cloudflare as a tunnel instead of gradio.live if you get Connection Errors.
tunnel = "gradio" #@param ["cloudflared", "gradio"]

if ezmode:
  if tunnel == "cloudflared":
    for line in fileinput.FileInput(f'Easier{weeee}.py', inplace=True):
      if line.strip() == 'app.queue(concurrency_count=511, max_size=1022).launch(share=True, quiet=True)':
        # replace the line with the edited version
        line = f'        app.queue(concurrency_count=511, max_size=1022).launch(quiet=True)\n'
      sys.stdout.write(line)
    !pkill cloudflared
    time.sleep(4)
    !nohup cloudflared tunnel --url http://localhost:7860 > /content/srv.txt 2>&1 &
    time.sleep(4)
    !grep -o 'https[^[:space:]]*\.trycloudflare.com' /content/srv.txt >/content/srvr.txt
    time.sleep(2)
    srv=getoutput('cat /content/srvr.txt')
    display(HTML('<h1>Your <span style="color:orange;">Cloudflare URL</span> is printed below! Click the link once you see "Running on local URL".</span></h1><br><h2><a href="' + srv + '" target="_blank">' + srv + '</a></h2>'))
    !rm /content/srv.txt /content/srvr.txt
  elif tunnel == "gradio":
    for line in fileinput.FileInput(f'Easier{weeee}.py', inplace=True):
      if line.strip() == 'app.queue(concurrency_count=511, max_size=1022).launch(quiet=True)':
        # replace the line with the edited version
        line = f'        app.queue(concurrency_count=511, max_size=1022).launch(share=True, quiet=True)\n'
      sys.stdout.write(line)
  !python3 Easier{weeee}.py --colab --pycmd python3
else:
    !python3 infer-web.py --colab --pycmd python3
```

This is the code for a task that utilizes the Gradio UI window to convert the model to the desired target data.
<img width="550" alt="470826742_1697453609" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/20e54dce-3517-41c6-a95d-6fd011c07089">
Despite the explanation above, we leave the parameters at their default settings. Of course, changing the parameters can improve performance, but it will take longer and may be more resource intensive. The current values are based on experiments by the original authors and what has been shared in the community.

<img width="600" alt="스크린샷 2023-10-16 오후 2 46 43" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/fb422978-0cb1-43a3-8a93-9c464f5cb128">

1. in Choose model, press the refresh button several times if the model with the voice of the singer you want is not loaded well.  

2. You can think of it as target data, which is the vocal file you converted to gaudilab earlier. This is how I want to train the data in 1 as the target data in 2.  

3. optional is an octave-related parameter, which changes female -> male and male -> female +-12 using the parameter. I tried it with different octaves, but it's probably better not to use it unless you have a song that needs to be changed specifically. After converting, the synthesis proceeds. The result is a vocal file.

<img width="567" alt="470826742_1697453731 (1)" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/dea4dcbc-b09e-4c7e-8b0d-55af10dbe0e6">

- After the speech synthesis is completed, you can download the file and get the file. The parameters below are TTS-related parameters, but after experimenting with them, the best performance is to set them to the default values and convert them.
<img width="995" alt="470826742_1697453829 (1)" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/fd4de090-efe3-4991-84df-70107750f0b6">

- After that, various instrumental elements, such as drums, which are synthesized from the previously extracted sound source and the TTS result, must be combined again in a music-related work program. There are various programs such as Ableton, Cue Bass, Logic, etc., but this is easily available to those who have used it for some time, and if you are an Apple user, Garageband is said to be very good in cost performance. And you can combine them through BandLab, which is available on the web

## AIOT SPEAKER 
### Result 

[![Seven - Rosé(A.I Cover) original BTS-Jung Kook](https://img.youtube.com/vi/i90I7LdrHjs/0.jpg)](https://www.youtube.com/watch?v=i90I7LdrHjs)
[![Result Youtube Shorts](https://img.youtube.com/vi/1VO9MiSQf1U/0.jpg)](https://www.youtube.com/watch?v=1VO9MiSQf1U)

<img width="600" alt="스크린샷 2023-10-16 오후 2 50 45" src="https://github.com/jh941213/AIOT_Speaker/assets/112835087/a13d106f-ee74-418b-9067-33942cef1ee5">

Connect the IOT SPEAKER made above to the Ethernet communication and put the voice converted by AI into the GUI program.  

1. IOT Speaker first prepares for communication by setting IP.  
2. When it is completed, press the Play button on the GUI program and the music will come out.  
3. You can use the speaker according to the desired output format with I2S and SAI. The red button controls the volume of SAI, and the blue button controls I2S.  








