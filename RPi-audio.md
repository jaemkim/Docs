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

> 오류 
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

# [Snowboy를 이용한 음성인식 전용 마이크 만들기(1)(2018. 7. 28.)](https://m.blog.naver.com/cosmosjs/221328328264)

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

> 오류
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

