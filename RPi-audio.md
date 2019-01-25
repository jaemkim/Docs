라즈베리파이에서 USB 마이크, 스피커 설정하기
=========================================
https://diy-project.tistory.com/88

* 라즈베리파이에서 USB 마이크, 스피커 설정하기

    $ arecord -l
    $ aplay -l
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

    $ speaker-test -t wav 

    $ arecord --format=S16_LE --duration=5 --rate=16000 --file-type=raw out.raw