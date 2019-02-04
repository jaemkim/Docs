

# [최신 매직 미러 설치 2018.12.31](https://github.com/makepluscode/rpi-tutorial-advanced/tree/master/006-raspbian-magicmirror-google-assistant-latest)

### [#006 _ Install with the Latest](https://www.youtube.com/watch?v=UBgH5hejYtM&feature=youtu.be)

### Rasbian 설치
1. Download the latest image from the RazBian website. (2018-11-13-raspbian)
2. Download Rufus to write images to SD card.
3. Run Rufus and select the downloaded image to burn the SD card.
### Insert SD card + LCD + Power connection
1. Insert SD card and keyboardㆍmouse dongle into raspberry pi.
2. Connect LCD to raspberry pi on HDMI.
### 1. First Boot
1. Connect the USB power cable to the raspberry pi
2. After boot is done, connect to the Internet with WIFI
3. Update packages
```sh
sudo apt-get update
```
### 2. Magic Mirror 설치
```sh
Install the Magic Mirror using a script on the Internet
sudo apt-get install npm
sudo npm install -g npm@latest # 6.5.0 -> 6.7.0
bash -c "$(curl -sL https://raw.githubusercontent.com/MichMich/MagicMirror/master/installers/raspberry.sh)"
```

### 3. Magic Mirror Modules 설치
1. MMM-Hotword
```sh
cd ~/MagicMirror/modules/
sudo apt-get install libmagic-dev libatlas-base-dev sox libsox-fmt-all
git clone https://github.com/eouia/MMM-Hotword.git
cd MMM-Hotword
npm install

cd ~/MagicMirror/modules/MMM-Hotword/node_modules/snowboy
npm install --save-dev electron-rebuild
npm install nan
./node_modules/.bin/electron-rebuild
```

2. MMM-AssistantMk2
```sh
cd ~/MagicMirror/modules/
sudo apt-get install mpg321 libasound2-dev
git clone https://github.com/eouia/MMM-AssistantMk2
cd MMM-AssistantMk2
npm install

cd scripts
chmod +x *.sh
cd ~/MagicMirror/modules/MMM-AssistantMk2
npm install --save-dev electron-rebuild
./node_modules/.bin/electron-rebuild
```

### 4. Google Assistant Module 구성
1. Open the Google Action Console and create a new project
```sh
https://console.actions.google.com
```

2. Open the Google Cloud Platform Console and select the generated project
```sh
https://console.cloud.google.com
```

3. Search for the Google Assistant API and click Enable.
4. Click CONFIGURE ... of Credentials and put the name and e-mail.
5. Generate Other credentials with the OAuth Client ID in Create Credentials
6. Download generated OAuth client ID in json format
7. Move the downloaded OAuth client ID to modules/MMM-AssistantMk2/credentials.json
```sh
mv ~/Download/cre.... credentials.json
```
8. Run auth_and_test.js to verify the generated client ID
```sh
node auth_and_test.js
```
9. 상기 프로그램 실행을 하면 브라우져가 뜸. 
Accept the client verification process and copy and enter your Google account key
10. Move the generated token.json
```sh
mv token.json ./profiles/default.json
```
* [참고](https://github.com/eouia/MMM-AssistantMk2/blob/master/INSTALL.md)


### 5. Google assistant module config 에디팅

1. Open the Magic Mirror configuration file with TextEditor and modify it with the contents of github

https://github.com/makepluscode/rpi-tutorial-advanced/tree/master/006-raspbian-magicmirror-google-assistant-latest

https://github.com/makepluscode/rpi-tips/blob/master/003-magicmirror-assistant-how-to-change-lang/config.js

https://github.com/makepluscode/rpi-tutorial-advanced/tree/master/003-raspbian-magicmirror-google-assistant



### 6. 실행
```sh
cd ~/MagicMirror
npm start
```

### 7. 디버깅
```sh
npm start dev
```