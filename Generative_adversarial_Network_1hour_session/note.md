

#  1시간만에 GAN(Generative Adversarial Network) 완전 정복하기

**1시간만에 GAN(Generative Adversarial Network) 완전 정복하기** (*https://www.youtube.com/watch?v=odpjk7_tGY0&t=2839s*) 의 노트입니다.



## Probability DIstribution (확률 분포)

실제 이미지에 대한 확률 분포(확률밀도함수)가 존재할 때 아래의 분포를 갖는다고 가정한다면,

<center> <img src = "img/6.png"</center>





---



<center> <img src = "img/5.png"</center>



사람 얼굴 데이터 셋에서 *안경을 낀 남자*가 좀 상대적으로 적게 등장했다고 하면, 그 안경을 낀 남자에 해당하는 픽셀을 대표하는 값을 x1 의 어떤 벡터라고 했을때 그 x1에 해당하는 확률 밀도 값은 상대적으로 작게됩니다. 



<center> <img src = "img/4.png"</center>

흑발의 여자는 안경을 낀 남자보다 학습데이터에서 비교적 많이 등장을 했다면, 흑발의 여자 이미지에 해당하는 확률 밀도 값은 상대적으로 높게 됩니다. 



<center> <img src = "img/3.png"</center>

마찬가지로 금발의 여자 데이터가 많이 나왔다면 금발의 여자 데이터에 해당하는 벡터를 x3라고 했을 때 x3에 대한 확률 밀도값은 상당히 높게됩니다. (*예를 들어 1차원 상으로 설명되었지만, 실제로는 상당히 고차원입니다.*)





<center> <img src = "img/2.png"</center>

괴상한 이미지는 실제 학습 데이터에 존재할 수 없기 때문에 이를 x4라고 하면 이에 대한 확률밀도값도 굉장히 낮습니다. 이에 대한 64 x 64 x 3 크기의 고차원 벡터는 픽셀값이기 때문에 픽셀값들을 잘 조정하다보면, 이런 괴상한 이미지를 만들어 낼 수 있게 됩니다.





<center> <img src = "img/1.png"</center>

Generative Model 이 하고자 하는 목표가 이 시점에서 나오게 되는데, 파란 색이 실제 학습 데이터 셋의 분포이며, Generative Model은 실제 이 데이터의 분포를 잘 근사하는 모델을 만들고자 합니다. 빨간 색은 모델이 생성에 대한 이미지 데이터 분포라고 생각할 수 있습니다. **두개의 확률분포간의 차이를 줄여주는 게 이제 Generative Model의 목표입니다.**



## Generative Adversarial Networks (GAN)

### Discriminator Model

![](img/201.png)

진짜 이미지를 진짜 이미지로 구별하고 **가짜 이미지를 가짜로 구별할 수 있도록 학습**합니다. 

* 입력 : 64 x 64 크기의 고차원 벡터
* 출력 : binary classification

![](img/203.png)



### Generator

![](img/202.png)

랜덤한 코드를 입력 받아서 이미지를 생성하고 **Discriminator를 속여야합니다.** Discrimator의 출력이 1이 나오도록 학습을 시켜야합니다. Generator가 학습을 할 수록 진짜같은 가짜 이미지를 만들어 내게 됩니다. 

![](img/204.png)





### Code

![](img/code1.png)



![](img/code2.png)



![](img/code3.png)



![](img/code4.png)

![](img/code5.png)

![](img/code6.png)

![](img/code7.png)



실제로 돌아가는 코드는 https://github.com/yunjey/pytorch-tutorial 레포지토리에 있습니다.



### Non-Saturating Game

Generator는 처음에는 매우 형편없는 이미지를 만들게 됩니다. Discreminator의 입장에서는 이런 형편없는 이미지에 대해서 가짜임을 확신하게 됩니다. 그렇다면, **D(G(z))의 값이 0에 가깝게 된다.** 그런데 그때의 기울기가 생각보다 작습니다. (*아래의 그래프를 참고합니다.*)

![](img/301.png)

그래서 log(1 - x)를 최소화하는 것이 아니라 log(x)를 최대화하는 방향으로 바꾸게 됩니다. (Heuristically motivated)

![](img/302.png)

![](img/303.png)

기울기가 무한대로 나오게 됩니다. Generator 의 결과물이 안좋은 상황을 최대한 빨리 벗어나려고 노력하려고 해서 **Discreminator가 햇갈려할만한 데이터를 생성**해내려고 하게 됩니다.

![](img/304.png)

##### Theory in GAN

![](img/305.png)

이론적으로 왜 GAN이 잘 작동하는지 : 최적화하는 것은 실제로 두 확률분포 간의 차이를 줄여주는 것이기 때문에 Generator가 진짜와 가까운 이미지를 만들 수있다.



## Varient of GAN

### DCGAN(Deep Convolutional GAN, 2015)

Deep Convolutional Network를 통해서 Generator를 만들어냈다.

![](img/306.png)


![](img/307.png)

DCGAN에서의 핵심은 **Pooling Layer를 사용하지 않았다**는 것이다. Pooling Layer를 사용하게 되면 unpooling을 할 때의 결과물이 blocky하게 된다. 학습을 안정화시키기 위해서 Batch normalization을 적용하였으며, Adam optimizer를 사용하였다. 

64 x 64크기의 이미지를 만들 때 보통 4개의 Convolutional Layer를 이용해서 만들게 되는데, 저 term들의 결과가 좋게 나온다. 다른 논문들에서도 저 값을 고정적으로 사용한다.

![](img/308.png)

DCGAN에서 하나 더 재밌는 포인트는, Generator의 인풋으로 들어가는 Latent vector의 **산술적 연산이 가능하다**는 점이다. 



### LSGAN (Least Squares GAN)

기존 GAN같은 경우는 Discreminator만 속이면 됐지만... **Gradient Vanishing**

![lsgan01](img/lsgan01.png)

> 파란 선이 Discriminator의 Decision boundary를 의미합니다. 선 아래쪽이 Discriminator가 True 라고 예측한 이미지 데이터입니다. 빨간 점이 진짜 데이터고 파란 점이 가짜 데이터입니다. 빨간색에 가까운 파란색은 굉장히 잘 만들어진 가짜 이미지입니다. 핑크색 데이터는 Discriminator를 완벽하게 속인 이미지 데이터입니다.
>
> 그러나, *핑크색 데이터가 좋은 데이터냐?* 라고 했을 때는 그렇지 않습니다. 빨간 점 데이터랑 가까운 데이터가 실제로 좋은 데이터이다.  (Gradient Vanishing : Discriminator를 완벽해 속이더라도 실제 이미지 데이터랑 비슷하다고 보장할 수 없다.)



![lsgan2](img/lsgan02.png)



![lsgan3](img/lsgan03.png)



![lsgan4](img/lsgan04.png)



![lsgan5](img/lsgan05.png)



##### LSGAN의 결과 (LSUN DATASET)

![lsgan_r1](img/lsgan_r1.png)



##### LSGAN의 결과 (CelebA)

![lsgan_r2](img/lsgan_r2.png)



#### SEMI-SUPERVISED GAN

![ssgan1](img/ssgan1.png)

Discriminator가 더이상 진짜/가짜를 구별하는 것이 아니라 어떤 클래스를 구분하게 된다. 기존의 Supervised Learning의 경우 MNIST 데이터를 판별할 때 10개의 클래스로 판별하게 되지만, Semi-supervised GAN에서는 **10개 +  Fake 클래스**로 판별하게 됩니다.



![ssgan2](img/ssgan2.png)

2를 나타내는 One-hot 벡터를 Generator에 입력을 하면 가짜이미지 2를 생성합니다. 이 이미지를 Discriminator는 Fake클래스로 구분해내야 합니다. 반대로 Generator는 Discriminator를 속여야 하기 때문에 입력으로 준 One-hot벡터와 Discriminator의 출력이 같도록 학습을 진행합니다.



##### Result (Game character)

![dcgan_r1](img/dcgan_r1.png)





### ACGAN (Auxiliary Classifier GAN, 2016)

> Semi-supervised Learning 에 ACGAN을 적용시킬 수 있지 않는가..

![acgan01](img/acgan01.png)



Discriminator가 해야하는 테스크가 2가지가 있습니다. 

1. Training with real images

   ![acgan02](img/acgan02.png)

   > 1. FC Layer with sigmoid : **real or fake**
   > 2. FC Layer with softmax : 0 ~ 9

2. Training with fake images

   ![acgan03](img/acgan03.png)

   > Generator에 2에 해당하는 one-hot 벡터를 입력하면 가짜 이미지를 생성해내고, Discreminator는 이 이미지를 가짜라고 판단해야 합니다. 그럼에도 불구하고 Discreminator는 가짜이미지를 2로 분류해내야 합니다. 여태까지의 GAN은 Generator에 집중을 했지만, ACGAN은 Discreminator에 집중을 한다. **Generator는 Data Augmentation하는 역할을 하고  노이즈가 포함된 데이터를 입력하더라도 Classification이 되면 Discriminator의 성능이 좋아진게 아닌가.**

3. Loss Function : **loss of (1)** + **loss of (2)**



## EXTENSIONS OF GAN

### CycleGAN

*얼룩말을 일반 말로* 바꾸고, *겨울 풍경을 여름풍경으로* 바꾸고 .. 이미지 도메인을 바꾸는 것. *Parallel 데이터(Paired Example)가 없이 Unsupervised Learning을 하더라도 이런 것이 될 수 있지 않을까* 라는 의문을 품고 만들게 됨.

![cycle01](img/cycle01.png)





Latent code를 받지 않고 Real Image를 받게 됩니다. *Encoder & Decoder* 식으로 줄어들었다 늘어나게 됩니다.

![cycle02](img/cycle02.png)



![cycle03](img/cycle03.png)

##### Results

![cycler1](img/cycler1.png)

> 데이터가 두 도메인 당 10000개 이상은 있어야함. 논문에서만큼은 잘 나오지는 않지만 의미있는 결과는 볼 수 있다.



##### Result (SVHN & MNIST)

![cycler2](img/cycler2.png)



### StackGAN

![stack01](img/stack01.png)

> "새가 날라간다" **텍스트**-> **이미지** 로 변환되는 과정



##### 128 x 128 크기의 이미지를 생성 (그 이상의 해상도는 잘 된다는 보장이 없습니다.)

![stack02](img/stack02.png)

그래서 저해상도의 이미지를 upscale하는 방법을 택함.

![stack03](img/stack03.png)

##### Latest Work

![stack04](img/stack04.png)



![stack05](img/stack05.png)





## Future of GAN

### Boundary Equilibrium GAN (BEGAN)

*Convergence measure* : Supervised-Learning을 하게 되면 Cross-entropy Loss함수가 있어서 Loss함수가 줄어드는 것을 통해 학습이 잘 되고 있음을 판단할 수 있지만, GAN에는 그런 것이 없었습니다. 실제 이미지를 보고 사람이 학습이 잘 되는지 직접 보고 판단했어야만 했습니다. BEGAN이 처음으로 Convergence Measeure가 될만한 것을 제공합니다. BEGAN의 Discriminator가 Auto Encoder식으로 복잡하게 구현되어 있습니다. 복잡한 구조에서만 사용할 수만 있는 Convergence measure를 제공한다는 한계점을 갖고 있습니다.

![began01](img/began01.png)



Reconstruction Loss : batch normalization 이 아니라 VT Normalization이 GAN에서 쓰면 좋다는 논문이 발표되었다.  

**z값**

1. Generator의 Weight를 고정시키고 
2. z를 랜덤하게 샘플링하고
3. forward propagation을 해서 이미지를 만듭니다. *G(z)*
4. X와  G(z)를 빼서 L2 Loss(Reconstruction Loss)를 계산합니다.
5. 계산한 Loss를 Back propagation하고
6. *Generator를 학습하는 게 아니라 z값을 학습하는 중*
7. G(z)와 X가 비슷해지도록 z를 학습하는 것. (Gradient Descent를 활용하여)![began02](img/began02.png)

> 단점이 바로 보인다. **z를 학습해야한다.** (배보다 배꼽이 더 크게 된다.)
>
> 두번째 단점으로는 매우 느리다



### Deconvolution Checkboard Artifacts

*좀 더 좋은 Up-sampling 방법을 찾아야되지 않을까* 

![began02](img/dec01.png)

> 이런 식이면 불균형한 Output을 만들게 된다. (검은색(4) - 진회색 (2)- 회색(1))



![dec02](img/dec02.png)

	> 이런식이다.

Resize-Convolution : 단지 학습으로 업샘플링하는 deconvolution과는 달리 업샘플링 방식을 rule-based로 한다. (ex. nearest neighbor) 그 이후의 convolution layer (stride size = 1)로 쌓게 됩니다.



### Seq2Seq

![last1](img/last1.png)

![last2](img/last2.png)

Discriminator는 A, B 두개가 같은 뜻을 갖고 있으면 1에 가까운값을, 가짜 한글을 만들어내면 0에 가까운 값으로 판별합니다. 