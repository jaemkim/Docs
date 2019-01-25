# [한국어 지원 라즈베리파이 구글 어시스턴트(Google Assistant Service-gRPC) 설치(1)(2018. 7. 4.)](https://m.blog.naver.com/cosmosjs/221312669747)
- 최근 Google Assistant Library에서도 한국어를 지원 하므로 핫워드를 지원하는 Library 버전을 설치하면 됩니다.
- 구글 어시스턴트 Service에 대한 자세한 가이드는 [링크](https://developers.google.com/assistant/sdk/guides/service/python/)를 참조 하자.
- 구글 어시스턴트는 사용자가 선택해서 설치할 수 있는 두가지 옵션을 제공
  + Google Assistant Library와 Service
  + 차이점

|  | Library | Service |
|---|:---:|---:|
| Hands-free activation(Ok google) | Yes | No |
| Visual output of Assistant response | No | Yes |
  + Service의 제일 눈의 띄는 차이가 다 이해를 할 수 없지만 ... gRPC 플랫폼을 이용하고 Ok Google 같은 핫워드의 사용 못하는 등의 차이가 보인다
  + 그외 차이는 표를 참고 하자. 

1. SD카드 준비하자.
- sudo raspi-config 
- WiFi 설정
```
sudo chmod 777 /etc/wpa_supplicant/wpa_supplicant.conf
sudo wpa_passphrase "SSID name" password >> /etc/wpa_supplicant/wpa_supplicant.conf
sudo reboot
```
- samba 설정
```
sudo apt-get install samba samba-common-bin
sudo smbpasswd -a pi
sudo nano /etc/samba/smb.conf

[pi] 
comment = Raspberry pi 
path = /home/pi 
valid user = pi 
browseable = yes 
writable = yes 

sudo service smbd restart
```

2. 오디오 설정
```
arecord -l
aplay -l
```
- 사운드카드와 마이크가 어쩐 장치로 연결 되어 있는지 확인한다. 
- card 0, device 0 
- card 1, device 0 을 사용중인것을 확인했다. 어떤 장치를 사용하는냐에 따라 다를 수 있다.
```
alsamixer
sudo alsactl store
```
- 보륨과 마이크 민감도를 최대로 높여 주고 저장해 준다.
```
vi ~/.asoundrc
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
    pcm "hw:0,0"
  }
}
```
- 테스트
```
speaker-test -t wav
arecord --format=S16_LE --duration=5 --rate=16000 --file-type=raw out.raw
aplay --format=S16_LE --rate=16000 out.raw
```

3. 구글 클라우드 프로젝트 설정
- https://console.actions.google.com/

4. 디바이스 모델 등록
- 액션 콘솔화면의 왼편 하단 메뉴에서 Device registration 메뉴를 클릭하여 디바이스를 등록 해준다. 
- [구글 클라우드 플랫폼](https://console.developers.google.com)에 가서 Google Assistant API를 사용가능으로 세팅한다.
- https://myaccount.google.com/activitycontrols?pli=1 에 가서 음성 및 오디오 사용등 필요한 항목의 체크박스를 사용가능으로 해준다. 


5. 어시스턴트 SDK와 샘플코드 설치하기
```
sudo apt-get update
sudo apt-get install python3-dev python3-venv 
python3 -m venv env
env/bin/python -m pip install --upgrade pip setuptools wheel
source env/bin/activate


python -m pip install --upgrade google-assistant-library
python -m pip install --upgrade google-assistant-sdk[samples]
```

6. Generate credentials
```
python -m pip install --upgrade google-auth-oauthlib[tool]
google-oauthlib-tool --scope https://www.googleapis.com/auth/assistant-sdk-prototype --scope https://www.googleapis.com/auth/gcm   --save --headless --client-secrets /home/pi/credential.json
```
- https://로 시작되는 부분부터 복사해서 웹브라우저에 넣고 실행하여 구글 계정을 연결하도록 한다. 마지막에 나오는 인증코드를 위 터미널 화면에 넣어 주고 엔터를 치자. 이렇게 해주면 모든 과정이 끝이 난다.

7. 샘플을 실행해 보자.
```
googlesamples-assistant-hotword --project-id your-id --device-model-id your-model-id

googlesamples-assistant-pushtotalk --device-id Your-dev-project --device-model-id Your-model-id
```
- 기존에 했었던 핫워드로 하는 것을 해보고 싶다면 ...
```
python -m pip install --upgrade google-assistant-library 
```
먼저 라이브러리를 설치해 주자. 샘플코드는 이미 설치 되어 있다.


8. **한국어로 대화하기**
```
googlesamples-assistant-pushtotalk  --lang ko-KR
```
- 실행시 lang 옵션을 주고 한국어를 지정해 주면 한국어 구글 어시스턴트로 작동이 된다. 
