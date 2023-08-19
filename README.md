# ThinkBell Project :bell:
ThinkBell project, which is made from 2021 Woongjin Thinkbig Industry-Academic Cooperation Project Team.

## 1. 실행 방법
#### 요약: 각자 python 클라이언트를 키고, 브라우저로 접속

1. 클라이언트별로 python 클라이언트를 구동해야 합니다. flask 폴더로 진입하여 python server.py 커맨드를 입력해 주세요.

2. 만약 서버를 오픈해야 한다면, webrtc 폴더로 진입하여 npm이 설치되어있지 않다면 먼저 npm install 커맨드를 입력 후에 npm start를 입력합니다. 이렇게 함으로써 서버가 오픈되게 됩니다.

3. 서버를 열고 나서, 혹은 누군가가 서버를 열었다면 해당 ngrok 주소를 브라우저에 입력하여 브라우저 상에서 화상 회의 통신이 이루어집니다. 만약 로컬에서만 테스트하고 싶다면, https://localhost:3012 를 입력하세요. 크롬 브라우저를 권장합니다.

4. 접속이 되었다면, python 클라이언트에서 통신이 잘 되고 있는지 로그를 확인해 주세요.

## 2. 전체적인 시스템 구조
#### 요약: 각자 실행한 python 클라이언트가 영상 인식과 음성 인식을 진행하고, 결과값을 js webrtc를 통해 영상과 함께 주고받음

![workflow](https://user-images.githubusercontent.com/33966473/134840473-2aa66fff-76f6-4e1a-9d4c-94ac5dee86bc.jpg)

시스템은 webrtc 통신을 중심으로 구동되며, js webrtc 모듈은 python 영상 처리 클라이언트에게 처리할 이미지를 Frame 단위로, js 상에서 구동되는 AI Agent 모듈에게 Stream 리소스를 제공합니다. 영상 처리 클라이언트가 분석을 마치고 결과값을 js AI Agent에 리턴하면, AI Agent가 Front-End와 통신하며 결과값을 시각적으로 표현합니다.

## 3. 포함된 모듈 세부

현재 리포지토리에 담겨 있는 코드는 python 클라이언트를 담당하는 flask 폴더와, js 클라이언트와 서버를 담당하는 webrtc 폴더 크게 두 가지 파트로 구분되어 있습니다.

flask 폴더는 다음과 같이 구성되어 있습니다.

- MediaPipeProcess.py: Google MediaPipe 모듈을 이용하는 모든 영상 처리 모듈이 이곳에서 이루어집니다.
- VoiceActivityDetection.py: VAD 알고리즘을 활용해 발화 인식이 이곳에서 이루어집니다.
- daiseecnn.py: DAiSEE 데이터셋을 활용해 Engagement를 측정합니다.
- object_detection_api.py: 앞에서 나왔던 처리 결과값들을 모두 한데 모아 Threshold와 각종 몰입도 측정 알고리즘을 이용하여, flask 서버에 json 형식으로 최종 몰입도 결과값을 리턴하는 핵심 python 파일입니다.
- server.py: flask 서버를 오픈합니다. 이 flask 서버는 로컬 전용으로 webrtc 모듈과 통신하기 위해서만 존재하며, 외부 클라이언트와 통신하지 않습니다.
할합니다.
