# 4분이면 충분한 딥러닝 파키슨병 진단기 제작기

## 파킨슨 병 : 알츠하이머 병 다음으로 노인에게 빈번하게 발견되는 증상

* 진단하기에 까다롭다. 확정적인 테스트가 없는 편이고 의사의 주관으로 판단하게 되는 경우가 많다. 오진확률 (47%)
* 머신 러닝을 이용한 파킨슨병 진단 : 5만개의 목소리로 진단. 
    > ex. 모음을 길게 발음하는 것을 머신러닝으로 판단.

* 한국인 피쳐를 위한 모델을 만들어야 한다 : 영어권 보다 국내에는 의료데이터가 적다. (한국 500개 + 터키어 5000개)
    * 소규모 언어 데이터로 파킨슨병 진단 모델을 만들어보자.
* Data Augmentation (Rolling, Stretching, Adding Noises, Pitch Shift)
* Transfer Learning : 대규모 데이터에서 얻은 인사이트 활요하기
    * 언어간의 차이를 무시할 수 없음을 가시적 데이터를 통해 확인할 수 있다.
    * -> Transfer Learning 의 반대방향으로 가닥을 잡게된다.
* Modified Incremental Training 
    * 대규모 데이터에서 얻은 인사이트 활용하기

* GAN Domain Transfer
    * 대규모 데이터에서 얻은 인사이트 활용하기

    Ref |-> |  Target
    -|-|-
    Photograph | -> |monet, VanGogh
    Other Language | -> | Korean

* 4클래스 진단모델 ; VGG-16, Inception V3, 3Layer CNN, MobileNet
    * input : 음성
    * network 
    * output : 병의 경도

* VoiceDoc
    * 디바이스가 필요하다. 진단 기구 및 모바일 앱 개발 기획
    * 모델 경량화 필요성

* Deep Learning Hardware
    > 딥러닝 모델 하드웨어로 현실로 꺼내기.
    * Embedded Deep Learning 의 사례는 매우 많다. 
    * GPU / TPU Embedded Board.

* 두가지 개발방식
    * Local Type : TF -> TFLite
    * Server Type : embedded Device -> Server -> embedded Device
        * 재학습을 할 수 있는 장점이 있다.

* Convert to TF.Lite
    1. Get a Model
    2. Exporting the Inference Graph
        1. Graph def. (.pb)
        2. Check Point (.ckpt)
    3. Freezing Exported Graph
        * `CLI Interface` or `In Python Code`
    4. Convert Frozne Graph to .tflite

* Raspberry Pi ; Android 를 이용하기 위해선 `Android Things` OS 를 설치해야한다.
    * Android API를 모두 사용할 수는 없다.

    *후략*