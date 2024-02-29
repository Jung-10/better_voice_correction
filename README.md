# better_voice_correction
청각장애인 영어발음 교정 서비스

여러분께서 요청하신 내용을 깃허브 README 파일 형식에 맞게 수정해드렸습니다. 아래는 수정된 내용입니다:

---

# 2022 데이터청년캠퍼스 장관상 수상 프로젝트

서비스 시연영상: [YouTube 링크](https://www.youtube.com/watch?v=t5yRbs3hdSM)

페이지 접속: [example-server.shop](http://example-server.shop/) (aws ec2 비용 문제로 인해 현재 배포 중단)

Repository: [chestnut1717/voice_correction_deploy](https://github.com/chestnut1717/voice_correction_deploy)

## 1. 필요 라이브러리 및 프로그램 (로컬에서 실행할 경우에만 필요)

### 환경
- **로컬 환경**: Windows 10, Python 3.7, Conda 가상 환경
- **배포 환경**: Ubuntu(18.04), Python 3.7

### 라이브러리
- `librosa == 0.8.1`
- `pydub == 0.25.1`
- `noisereduce == 2.0.1`
- `transformers == 4.21.1`
- `phonemizer == 3.2.1`
- `torch`
- `Flask == 2.1.2`
- `flask-restx == 0.5.1`
- `SoundFile == 0.10.3.post1`

### 추가 설치 프로그램
- **phonemizer 라이브러리 사용을 위해서는 설치가 필요합니다.**
  - **Windows**: [espeak 다운로드](http://espeak.sourceforge.net/download.html) 후 설치
    - 환경변수 입력 후 재부팅
      1. `PHONEMIZER_ESPEAK_LIBRARY="c:\Program Files\eSpeak NG\libespeak-ng.dll"`
      2. `PHONEMIZER_ESPEAK_PATH ="c:\Program Files\eSpeak NG"`
  - **리눅스(ubuntu 18.04)**: 명령어를 통해 설치
    ```
    sudo apt-get install python-espeak
    sudo apt-get update && sudo apt-get install espeak
    ```

### 추가 다운로드 파일
- [Wav2Vec2.0 사전학습된 모델](https://drive.google.com/drive/folders/1wpFX_3H1GbcvgyXMHtObtKp3U5v2nwVS?usp=sharing)
- [Tokenizer](https://drive.google.com/drive/folders/1nuXzOSj4Xxh9emfi19NxEwUwkICtVMYf?usp=sharing)
  
  각각을 다운로드하여 `web_flask` 폴더에 저장해주세요.

## 2. 사용 시 유의사항
### 2.1 마이크 사용 관련
- HTTPS 보안 연결이 되지 않은 사이트이기 때문에 Chrome, Edge 등의 브라우저에서는 마이크 작동이 불가능합니다.
  따라서 HTTPS를 연결하여 마이크 제한을 해제해야 합니다.
  - [chrome://flags/#unsafely-treat-insecure-origin-as-secure](chrome://flags/#unsafely-treat-insecure-origin-as-secure)에 접속하여 "insecure origins treated as secure"에 `http://example-server.shop/` url을 등록해주세요.

### 2.2 서버 속도 관련
- 딥러닝 모델을 사용하여 개별화된 목소리를 생성하고 있으며, 무료 서버를 사용하고 있기 때문에 음성을 받아오는 데에 어느 정도의 시간이 소요됩니다. (30초 ~ 1분)
- Torch GPU 버전을 설치한 후 GPU 환경에서 작동하면 비교적 빠른 속도로 음성을 받아올 수 있습니다.

## 3. 서버 / DB
### 3.1 voice cloning 서버
- **FastAPI** 기반, **Heroku**로 배포 (CPU * 1 / RAM : 512MB)
- 개별화된 목소리 서비스 제공을 위해 다음과 같은 서버로 요청 및 응답을 받고 있습니다.
  - Encoder: [https://better-encoder.herokuapp.com/inference/](https://better-encoder.herokuapp.com/inference/)
  - Synthesizer: [https://better-synthesizer.herokuapp.com/inference/](https://better-synthesizer.herokuapp.com/inference/)
  - Vocoder: [https://better-vocoder.herokuapp.com/inference/](https://better-vocoder.herokuapp.com/inference/)

### 3.2 웹 + 분석모델 서버
- **Flask** 기반, **AWS EC2**로 배포 (CPU * 1 / RAM : 1G)

### 3.3 DB
- **MySQL**, **AWS RDS**

## 4. License
- **입모양 영상 파일**: [BBC Learning English](https://www.bbc.co.uk/worldservice/learningenglish/grammar/pron/sounds/)
- **Template**: FlexStart
  - Template Name: FlexStart
  - Template URL: [https://bootstrapmade.com/flexstart-bootstrap-startup-template/](https://bootstrapmade.com/flexstart-bootstrap-startup-template/)
  - Author: BootstrapMade.com
  - License: [License](https://bootstrapmade.com/license/)

--- 
