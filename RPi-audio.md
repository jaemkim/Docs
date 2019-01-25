라즈베리파이에서 USB 마이크, 스피커 설정하기
=========================================
https://diy-project.tistory.com/88

> 사용 가능한 마이크 검색<br>
$ arecord -l
>> 결과 card 1, device 0<br>

> 스피커 검색<br>
$ aplay -l

> ALSA 설정<br>
$ vi .asoundrc
```    
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

> 스피커 테스트<br>
$ speaker-test -t wav

> 녹음<br>
$ arecord --format=S16_LE --duration=5 --rate=16000 --file-type=raw out.raw
```
_arecord: main:788: audio open error: 그런 파일이나 디렉터리가 없습니다_
http://snowdeer.github.io/raspberry/2017/08/12/raspberry-aplay-and-arecord/

$ arecord -t raw -c 1 -D plughw:1,0 -f S16_LE -d 5 -r 16000 test.pcm
$ aplay -t raw -c 1 -f S16_LE -r 16000 test.pcm
```

> 실행<br>
$ aplay --format=S16_LE --rate=16000 out.raw

> 소리조절<br>
$ alsamixer
