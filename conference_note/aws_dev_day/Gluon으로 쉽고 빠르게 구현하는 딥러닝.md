
## Netowrk 구현 방식
* 플레이스홀더 ; 사전에 네트워크를 디파인

1. Symbolic 방식
    1. placeholde값에 function을 우선 정의
    2. MXnet, Tensorflow, theano
   
2. Imperative 방식
    1. 동적 네트워크 구축 가능 (define by run)
    2. 최근에는 Imperative 방식으로 만힝 구현
    3. Tensorflow eagermode, pytorch, gluon, chainer
    4. Network를 구현하면서 중간결과를 즉시 확인이 가능함

## MXNet/Gluon 주요 특징
1. NDArray 방식 적용
    * Gluon에서 활용하는 주요 방식
    * 해당 형태로 데이터를 선언하면 별도의 변수선언없이 네트워크 입출력이 가능
2. Autograd지원
    * backpropagation수행시 gradient 를 자동으로 계산해줌
3. Symbolic / Imperative 변환이 용이함
    * Hybrid함수 사용을 통해 간편하게 변환이 가능함

## NDArray 활용방안
NXnet에서 활용하는 데이터방식

### 주요 특징
* CPU/GPU변환이 쉬움
* 기본적인 문법이 NumPy와 유사
* 계산결과를 넘파이 형태로 변환하는 것이 용이함.

## Automatic Differentaition /w autograd
Gluon에서는 autograd가 gradient를 계산해줌.

## Deep learning 구현 프로세스
1. 사용 데이터 정의
    1. `DataSet` : Data 를 수집 로드 파싱
    2. `DataLoader` : 미니배치 자동생성, 멀티프로세싱 지원
2. Build Network
    1. `Block`
    2. `Sequential`
    3. `Hybridize`
        1. Block -> HybridBlock
        2. Sequential -> HybridSequential
    4. preTrained network도 있다.
3. Train
    1. `autograd`
4. 모형 Deploy
    1. `json`형태로 저장
    2. `ONNX`

## GluonCV / GluonNLP
매우 쉽게 Computer Vision, Natural Language Processing 이 가능하다.

