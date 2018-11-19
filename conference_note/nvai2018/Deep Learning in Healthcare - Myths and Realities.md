
## Deep Learning in healthcare

*생각보다 많은 회사가 다양한 주제에서 노력을 하고있다.*

### 의학의 패러다임 변화의 시기가 왔다.
> Art of Medicine -> Evidence-based Medicine -> Data-driven Medicine

* 데이터를 기반으로 의학의 패러다임을 바꾼다.
    * 의사를 대체하는 것이 아니라 10-20년 걸리는 프로세스를 줄이는 데에 목표를 둠.
    * 엄청나게 많은 종류를 표준하 하는것이 선행되어야한다. 
        * Medical Image Diagnosis : CNN 을 기반으로 접근을 만힝 한다.
        * Diagnosis Prediction : RNN 을 기반으로 접근을 많이 한다.
        * Continuous Time Series (SLEEPNET)
            > 데이터가 없어서 연구를 못한다는 거짓말이다.
            >> Healthdata.gov
            github에도 많이 있다.
* Why 98% of Digital Health startups are zombies and what they can do about it?
    * 새로운 기술 도입에 대한 보수적인 분위기

* What's Different from usual deep leearning? 
    * 삶과 죽음과 관련된 디시젼
    * 디플로이먼트가 굉장히 중요하다. 
    * 알고리즘이 충분히 Fair 한지?
    * unsupervised learning 에서 많은 Question이 있다
    * 인과관계를 설명하는게 어렵다.
    * 레이블이 없는 데이터가 의외로 많다.
    * 샘플의 수가 적은 것도 많다.
    * 개인정보에 관한 문제    

* CASE STUDY : LUNIT
    * 알고리즘의 문제가 아니다. 데이터의 취득이 더 중요 -> 커며셜에서 메디컬쪽으로 방향을 돌림
    * Data Driven Imaging Biomarker
    * TB Detection (2016) 10848 CXRs (7020 normal + 3828 tuberculosis)
    * Unwanted Bias in Training Data : **Limitation**
        * 디바이스 벤더별로 이미지의 퀄리티가 천차만별.
        * 다양한 기계에서 얻은 데이터들을 노멀라이즈하는 기술이 굉장히 중요.
        * **솔루션** : Semi-Supervision
    * DIB 2nd Generation
        * 전문의들보다 단독으로도 좋지만 같이 사용하면 매우 훌륭하다.
    * Chest X-Ray DICOM Files... (앗...)
    * Interaction 도 좋아야한다. (편하게 의사들이 사용할 수 있어야 한다. 루닛은 웹에 풀어서 만들어두었다.) 
    * What's Next :RAD/pATH co-Analysis 
* 기술과 도메인 전문가의 조합이 중요하다.