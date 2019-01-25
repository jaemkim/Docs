# [라즈베리파이에서 USB 마이크, 스피커 설정하기](https://diy-project.tistory.com/88)

### 사용 가능한 마이크 검색
```bash
$ arecord -l<br>
결과 card 1, device 0
```

### 스피커 검색
```bash
$ aplay -l
```

### ALSA 설정
```bash
$ vi .asoundrc
   
pcm.!default {
    type asym
    capture.pcm "mic"
    playback.pcm "speaker"
}
pcm.mic {
    type plug
    slave {
        pcm "hw:1,0"
    }
}
pcm.speaker {
    type plug
    slave {
        pcm "hw:1,0"
    }
}
```

### 스피커 테스트
```bash
$ speaker-test -t wav
```

### 녹음
```bash
$ arecord --format=S16_LE --duration=5 --rate=16000 --file-type=raw out.raw
```

> **오류**
```
record: main:788: audio open error: 그런 파일이나 디렉터리가 없습니다
```
> http://snowdeer.github.io/raspberry/2017/08/12/raspberry-aplay-and-arecord/
```bash
$ arecord -t raw -c 1 -D plughw:1,0 -f S16_LE -d 5 -r 16000 test.pcm
$ aplay -t raw -c 1 -f S16_LE -r 16000 test.pcm
```

### 실행
```bash
$ aplay --format=S16_LE --rate=16000 out.raw
```

### 소리조절
```bash
$ alsamixer
```

# [Snowboy를 이용한 음성인식 전용 마이크 만들기(1)(2018.7.28.)](https://m.blog.naver.com/cosmosjs/221328328264)

### 마이크 테스트
```bash
speaker-test -t wav
arecord -D plughw:1,0 -c 1 -f S16_LE -r 44100 test.wav
aplay test.wav
```

### 파이썬3 가상환경
```bash
sudo apt-get update
sudo apt-get install python3-dev python3-venv
python3 -m venv env
env/bin/python -m pip install --upgrade pip setuptools
source env/bin/activate
```

### Snowboy 설치
```bash
sudo apt-get install python-pyaudio python3-pyaudio sox
pip install pyaudio
```

> **오류**
```
arm-linux-gnueabihf-gcc -pthread -DNDEBUG -g -fwrapv -O2 -Wall -Wstrict-prototypes -g -fdebug-prefix-map=/build/python3.5-6waWnr/python3.5-3.5.3=. -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -fPIC -I/home/pi/env/include -I/usr/include/python3.5m -c src/_portaudiomodule.c -o build/temp.linux-armv7l-3.5/src/_portaudiomodule.o
src/_portaudiomodule.c:29:23: fatal error: portaudio.h: 그런 파일이나 디렉터리가 없습니다
    #include "portaudio.h"
                        ^
compilation terminated.
error: command 'arm-linux-gnueabihf-gcc' failed with exit status 1
```

> https://stackoverflow.com/questions/5921947/pyaudio-installation-error-command-gcc-failed-with-exit-status-1

```bash
sudo apt-get install portaudio19-dev
```

#### 테스트
```absh
rec temp.wav
```
> **오류**
```
rec FAIL formats: can't open input  `default': snd_pcm_open error: No such file or directory
```
> https://www.raspberrypi.org/forums/viewtopic.php?t=13088
```
sox default device 설정
export AUDIODEV=hw:1,0
```

### snowboy 다운로드 및 python3 코드 컴파일
```bash
git clone https://github.com/Kitt-AI/snowboy.git
cd ~/snowboy/swig/Python3/
make
```
> **오류**
```
/bin/sh: 1: swig: not found
```
> https://github.com/Kitt-AI/snowboy/issues/338
```
apt-get install swig
```

# [한국어 지원 라즈베리파이 구글 어시스턴트(Google Assistant Service)(2) : Snowboy (Hotword Detection Engine)(2018.7.8.)](https://blog.naver.com/PostView.nhn?blogId=cosmosjs&logNo=221314667019&categoryNo=83&parentCategoryNo=0&viewDate=&currentPage=4&postListTopCurrentPage=1&from=thumbnailList&userTopListOpen=true&userTopListCount=5&userTopListManageOpen=false&userTopListCurrentPage=4)

- Snowboy는 Kitt.air가 제공하는 클라우드 기반에서 학습된 핫워드 모델 데이터를 라즈베리파이등에 사용할 수 있도록 해주는 라이브러리

### snowboy 다운로드 및 python3 코드 컴파일 (2)
```
sudo apt-get install python-pyaudio python3-pyaudio sox
sudo apt-get install libatlas-base-dev
sudo apt-get install swig
pip install pyaudio
```
#### 
```
git clone https://github.com/Kitt-AI/snowboy.git
cd ~/snowboy/swig/Python3/
make
```

### 실행
```
python demo.py resources/models/snowboy.umdl 
```

> **오류**
```
Traceback (most recent call last):
  File "demo.py", line 1, in <module>
    import snowboydecoder
  File "/home/pi/snowboy/examples/Python3/snowboydecoder.py", line 5, in <module>
    from . import snowboydetect
ValueError: Attempted relative import in non-package
```
> snowboydecoder.py 파일 수정

```
vi  snowboydecoder.py

from . import snowboydetect
import snowboydetect
```
> **오류**
```
ImportError: dynamic module does not define init function (init_snowboydetect)
```
> https://github.com/Kitt-AI/snowboy/issues/424
```
Could you try to run this under Python3 virtual environment? Make sure you also compile swig/Python3 under Python3 virtual environment.

cd ~; source env/bin/activate
```
> **오류**
```
(env) pi@raspberrypi:~/snowboy/examples/Python3 $ python3 demo.py resources/models/snowboy.umdl 
Listening... Press Ctrl+C to exit
connect(2) call to /tmp/jack-1000/default/jack_0 failed (err=No such file or directory)
attempt to connect to server failed
Expression 'paInvalidSampleRate' failed in 'src/hostapi/alsa/pa_linux_alsa.c', line: 2048
Expression 'PaAlsaStreamComponent_InitialConfigure( &self->capture, inParams, self->primeBuffers, hwParamsCapture, &realSr )' failed in 'src/hostapi/alsa/pa_linux_alsa.c', line: 2719
Expression 'PaAlsaStream_Configure( stream, inputParameters, outputParameters, sampleRate, framesPerBuffer, &inputLatency, &outputLatency, &hostBufferSizeMode )' failed in 'src/hostapi/alsa/pa_linux_alsa.c', line: 2843
Traceback (most recent call last)::
  File "demo.py", line 33, in <module>
    sleep_time=0.03)
  File "/home/pi/snowboy/examples/Python3/snowboydecoder.py", line 177, in start
    stream_callback=audio_callback)
  File "/home/pi/env/lib/python3.5/site-packages/pyaudio.py", line 750, in open
    stream = Stream(self, *args, **kwargs)
  File "/home/pi/env/lib/python3.5/site-packages/pyaudio.py", line 441, in __init__
    self._stream = pa.open(**arguments)
OSError: [Errno -9997] Invalid sample rate
```
> .asoundrc 파일 수정
>> 변경 되어 있음
>> 원래 파일로 복구

### Hotword 생성
- https://snowboy.kitt.ai
- 로그인
    + google 계정 로긴
    + facebook 계정 로긴
- Create Hotword를 클릭 : 세번에 걸쳐 트레이닝을 한다음 파일을 다운로드 
- 라즈베리파이 스노우보이 models 폴더에 복사 후 실행

> **오류**
>> Chrome에서는 안됨
> **Fireefox 설치**
>> google 계정 로긴
