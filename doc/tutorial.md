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


##  시작

### 패키지 설치

메인 메뉴 File > Settings 를 클릭해 Project Interpreter 로 이동합니다.

**+ 버튼**을 누르면 Available Packages 팝업이 표시되는데, 여기서 새로운 패키지를 설치할 수 있습니다.  **Flask** 를 검색해서 선택 한후 **Install Package** 버튼을 눌러 설치하고 창을 닫고 Settings 다이얼로그도 OK 버튼을 눌러 닫습니다.


### 소스 작성

Project 탭 컨텍스트 메뉴에서 New 를 클릭해 src 폴더와 src/main.py 를 생성합니다.

    from flask import Flask

    app = Flask(__name__)


    @app.route('/')
    def home():
        return 'Hello, World!'


    app.run(debug=True)
    
    
### 앱 실행

메인 메뉴 Run > Run 'main' 메뉴를 클릭하면 앱이 실행되며 하단 콘솔창에 다음과 같은 메시지가 표시됩니다.

    pydev debugger: process 384 is connecting

    Connected to pydev debugger (build 143.1919)
     * Restarting with stat
    pydev debugger: process 4508 is connecting

     * Debugger is active!
     * Debugger pin code: 154-334-778
     * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)

로컬 사이트 <http://127.0.0.1:5000/> 을 접속하면 실행 결과를 확인 할 수 있습니다.


### 디버깅

실행 전 에러는 콘솔 창에서 확인 가능합니다. 예를 들어 home() 뒤에 : 을 빠뜨렸다면 아래와 같은 메시지가 표시됩니다.

      File "C:/Users/myevan/Projects/dev-chicken/src/main.py", line 7
        def home()
                 ^
    SyntaxError: invalid syntax

    Process finished with exit code 1
    
실행 후 에러는 웹 페이지에서 확인 가능합니다. 예를 들어 'Hello, World!' 뒤에 + 2 를 붙인다면 로컬 사이트 접속시 아래와 같은 화면이 표시됩니다.

    TypeError

        TypeError: cannot concatenate 'str' and 'int' objects


    Traceback (most recent call last)


        File "C:\Users\myevan\PythonEnvironments\mobile_game_server\lib\site-packages\flask\app.py", line 1836, in __call__

            return self.wsgi_app(environ, start_response)

            ... 중략 ...


        File "C:\Users\myevan\Projects\dev-chicken\src\main.py", line 8, in home

            return 'Hello, World!' + 2


        TypeError: cannot concatenate 'str' and 'int' objects

        ... 후략 ...
        
디버깅 페이지 각 소스 라인을 선택하면 콘솔 버튼이 표시되는데 해당 버튼을 누르면 변수 상태 확인이 가능합니다.     

첫번째 시도시에는 아래와 같은 팝업이 표시되는데 앱 실행시 콘솔창에 표시된 PIN 로그 `* Debugger pin code: xxx-xxx-xxx` 번호를 입력하면 됩니다.


    Console Locked

    The console is locked and needs to be unlocked by entering the PIN. You can find the PIN printed out on the standard output of your shell that runs the server. 


    PIN:            [Confirm]

웹 콘솔에서 변수를 입력하면 내용을 확인 할 수 있습니다.

    [console ready]    
    >>> app.config
    flask.config.Config({'JSON_AS_ASCII': True, 'USE_X_SENDFILE': False, 'SESSION_COOKIE_PATH': None, 'SESSION_COOKIE_DOMAIN': None,   })
    >>> 
    
    
