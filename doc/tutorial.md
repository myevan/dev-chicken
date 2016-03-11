# 모바일 게임 서버 만들기

안녕하세요~ myevan 입니다 >ㅇ<)/ 오랜만에 시간적 여유가 생겨(...) 1 인 개발자 분들의 서버 개발 고민을 해소시켜드릴 겸 간단하게 서버 만들기 강좌를 진행해보도록 하겠습니다.


## 준비

온라인 게임 서버는 퍼포먼스가 중요하다보니 거의 대부분 c/c++ 을 사용했는데, 모바일 게임 서버는 퍼포먼스보다는 생산성이 중요하다보니 정말 다양한 언어들로 개발되고 있습니다. 일단 제가 제일 자신있는 언어인 **python** 으로 강좌를 진행하고 향후 시간이 남거나 후원(?)이 들어오면 다른 언어도 다루어보도록 하겠습니다. 

### 개발 환경 선택

개발 환경은 실제 게임을 서비스하는 환경(이하 프로덕션 환경)과 동일하게 만드는 것이 가장 좋습니다. 온라인 게임 시절에는 윈도우 데스크탑에서 개발한 다음 윈도우 서버에서 실행해서 참 좋았는데, 웹 기반의 모바일 게임 서버는 안타깝게도 대부분 리눅스 서버에서 운영되는 일이 많습니다. 다시 말해 개발 환경도 가상 머신을 이용해서 리눅스로 맞추는 것이 최상인데, 아마 그렇게 하면 바로 강좌를 닫아버리실테니 여기서는 **윈도우** 환경에서 개발해보도록 하겠습니다.

### 파이썬 설치

파이썬은 <https://www.python.org/downloads/> 에서 다운로드 받으실 수 있습니다. 문제는 다운로드 버튼이 3.x 와 2.x 2개라는 겁니다 <(-ㅇ-)> 왜 이런 일이 생겼는지에 대해서는 나중에 설명드리도록 하고, 일단 **2.x** (아마 2.7.11) 을 다운로드 받아주시면 감사하겠습니다. 설치 옵션은 꺼져있는 것 모두 켜주시고 설치가 완료되면 로그아웃했다가 다시 로그인하거나 리붓해야합니다. 

### 파이참 설치

파이참은 JetBrains 에서 개발한 IDE 로 <https://www.jetbrains.com/pycharm/download/#section=windows> 에서 다운로드 받으실 수 있습니다. 상업용이라면 Professional 버전을 받으시고, 비상업용이라면 Community 버전을 받으시면 됩니다. 

처음 실행시 물어보는 초기 설정은 Keymap scheme 는 VisualStudio, IDE theme 랑 Editor color and fonts 는 Darcula 추천드립니다.

### 가상 환경 생성

메인 메뉴 File > Settings 에서 Interpreter 로 검색하면 Project Interpreter 를 설정할 수 있습니다. 오른쪽 **톱니바퀴 버튼**을 클릭해서 **Create VirtualEnv 메뉴**를 누릅니다. 

가상 환경 생성 팝업(Create Virtual Environment)이 표시되는데, Name 에는 mobile_game_server 라고 입력하고, Location 에는 C:\Users\xxxx\PythonEnvironments\mobile_game_server 라고 입력합니다.

새로운 가상 환경이 생성되면 패키지 목록에 pip, setupstools, wheel 정도만 표시됩니다. 

