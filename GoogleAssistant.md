# [라즈베리파이에 구글 어시스턴트 설치하기 (model ID 포함)](https://diy-project.tistory.com/89)
- [Configure a Developer Project and Account Settings](https://developers.google.com/assistant/sdk/guides/library/python/embed/config-dev-project-and-account)


1. [Google Action Console](https://console.actions.google.com/u/0/)에 접속
  - 새로운 프로젝트 생성 : 이름을 넣고 생성
  - 그러면 아직 이 창을 닫지 말고 [Google API Console](https://console.developers.google.com/)에 접속
    + 결제
    + API 및 서비스 검색에서 Google assistant를 검색 : 사용설정을 눌러 활성화
- 왼쪽 메뉴의 사용자 인증 정보 클릭후 OAuth 동의 화면 클릭, 이메일 주소, 사용자에게 표시되는 제품의 이름 (영어)를 작성한뒤 아래의 저장 버튼을 누른다.
- 다음 https://myaccount.google.com/activitycontrols에 접속 하여 Web & App Activity, Device Information, Voice & Audio Activity를 활성화
- 이제 다시 Google Action Console로 돌아와서 왼쪽 메뉴바의 Device registration을 클릭
+ Product name
+ Manufacture name 
+ Device type는 적당하게 speaker로 설정
+ 자동으로 Device Model id가 생성되고 REGISTER MODEL을 클릭
- Download OAuth 2.0 credentials를 클릭해 .json파일을 내려받은 후 컴퓨터 적당한 곳에 저장
+ **반드시 파일의 이름을 변경해서는 안된다.**
- 다음으로 NEXT를 눌러 3단계가 나오면 SKIP 버튼을 눌러 빠져나온다. 
+ 그럼 본인의 Model ID를 확인할 수 있다. 이 ID를 잘 기억해두자.

2. json 파일 전송
- 컴퓨터에서 라즈베리파이로 파일을 전송하는 방법은 다양하지만 VNC viewer를 사용중이라면 내장된 파일 전송 기능을 이용

3. Credentials.json 파일 생성하기
```bash
$ google-oauthlib-tool --scope https://www.googleapis.com/auth/assistant-sdk-prototype \
                       --scope https://www.googleapis.com/auth/gcm \
                       --save --headless --client-secrets /home/pi/client_secret_23481444425-1gs9la9dli1kh1tb31lokmqd9be9ejfs.apps.googleusercontent.com.json
```
- Please visit this URL to authorize this application: https://... 허용 하면
- <u>Enter the authorization code:</u>에 들어갈 코드 생성

4. 실행
- Model ID : jmketri-97ef6-jmketri-9nrytf
- Project ID : project_id jmketri-97ef6
- Device ID : Jmketri
+ 왼쪽 위 톱니바퀴 모양 클릭
```
googlesamples-assistant-hotword --project-id your-id --device-model-id your-model-id
googlesamples-assistant-pushtotalk --device-id Your-dev-project --device-model-id Your-model-id

googlesamples-assistant-hotword --project_id jmketri-97ef6 --device_model_id jmketri-97ef6-jmketri-9nrytf

googlesamples-assistant-pushtotalk  --lang ko-KR --device-id Jmketri --device-model-id jmketri-97ef6-jmketri-9nrytf
```
