---
layout: post
title: NLP를 위한 딥러닝 가이드
---

<div class="message">
<p>2012년 이미지넷에서 토론토 대학의 알렉스 크리제브스키가 들고 나온 '알렉스넷(Alexnet)'은 기존의 참가자들을 현격한 차이로 따돌리며 놀랄만한 정확도를 보여주며 우승을 차지했다. 알렉스넷은 딥러닝이었다. 이후 불과 몇 년 사이 모든 참가자들이 딥러닝을 택할 정도로 이제 딥러닝은 비전 인식에 획기적인 변화를 주도 하고 있다. (아래 그래프 참조)</p>

<p>이후 다양한 양질의 문서가 하루가 멀다하고 출판되기 시작하며 배움의 속도보다 새로운 논문이 출판되는 속도가 훨씬 더 빠른 작금의 시점에 또 다른 문서를 작성하여 추가 하기 보다는 기존의 좋은 문서를 잘 엮어주는게 훨씬 더 중요하고 가치 있겠다는 판단에 따라 이번에는 그 동안의 글과는 달리 여러 딥러닝 자료들을 정리하고 부연 설명을 곁들여 정리해 본다.</p>

<p>특히 비전 인식을 제외하고, NLP에만 집중하여 자료의 범위를 좁히고 알고리즘 정리부터 시작하여, 밑바닥부터 시작하는(from scratch) 구현, 도구(TensorFlow, Keras)를 활용한 실제 서비스를 위한 구현까지, 단계별로 정리할 예정이다. 기존 Awesome 시리즈와 유사한 형태로 상세한 부연 설명을 곁들여 NLP를 위한 딥러닝을 구현하는데 도움이 되도록 한다.</p>
</div>

- *2017년 1월 11일 초안 작성*

<img src="https://c1.staticflickr.com/1/623/31406346824_682c223d93_o.png" width="300" />
*<sup>전통적인 CV방식(파란색)과 딥러닝 방식(초록색)의 이미지넷 정확도 결과[^1]</sup>*

[^1]: [2012년 이미지넷에서 알파고까지… 딥 러닝의 모든 것](https://forums.geforce.co.kr/index.php?document_srl=222723&mid=news)

## 문서 

### 이론
- [머신러닝 Coursera](https://www.coursera.org/learn/machine-learning/)  
앤드류 응 교수의 머신러닝 Coursera 대표 강의
- [스탠포드 CS 딥러닝 튜토리얼](http://deeplearning.stanford.edu/tutorial/)  
CS 자료이며 수식 중심 알고리즘 중심으로 정리. 실무 적용보다는 이론을 체계적으로 익히는데 유용. CNN 까지 설명되어 있음.

### 튜토리얼
- [모두를 위한 머신러닝/딥러닝 강의](https://hunkim.github.io/ml/)  
한글로 가장 잘 정리된 문서
- [모두를 위한 머신러닝/딥러닝 정리 노트](http://pythonkim.tistory.com/notice/25)  
매우 깔끔하게 잘 정리
- [Get Started with Machine Learning](http://suriyadeepan.github.io/2016-06-06-ml-basics-course/)  
각종 머신러닝 개념을 Cheat Sheets 형태로 깔끔하게 정리. 인도의 한 과학자가 정리. 인도는 영어가 되니 이렇게 영문서도 깔끔하게 잘 정리한다. 부러운 부분.
- [THE NEURAL NETWORK ZOO](http://www.asimovinstitute.org/neural-network-zoo/)  
새로운 신경망이 빠르게 등장하고 있기 때문에 약어만 듣고 구조를 일일이 파악하기란 매우 힘든 일이 되었다. 이 문서에서는 DCIGN, BiLSTM, DCGAN 같은 약어들의 신경망 구조를 한 눈에 알아볼 수 있도록 시각화하여 제공한다.
- [세상에 있는 (거의) 모든 머신러닝 문제 공략법](http://keunwoochoi.blogspot.kr/2016/08/blog-post.html)

### 신경망
- [Single-Layer Neural Networks and Gradient Descent](https://sebastianraschka.com/Articles/2015_singlelayer_neurons.html)  
단일 신경망을 구현하여 신경망의 원리를 알기쉽게 잘 설명한 글. Sebastian Raschka의 글로 아래 책 섹션에서 소개한 그의 저서 Python Machine Learning의 두 번째 챕터에 나오는 내용과 동일하다.
- [IMPLEMENTING A NEURAL NETWORK FROM SCRATCH IN PYTHON – AN INTRODUCTION](http://www.wildml.com/2015/09/implementing-a-neural-network-from-scratch/)

### NLP
- [CS224d: Deep Learning for Natural Language Processing](http://cs224d.stanford.edu/syllabus.html)  
Richard Socher의 스탠포드 강의 자료. 이 사람은 매닝과 응의 제자로 메타마인드를 창업했고 스탠포드에서 지도 교수였던 매닝과 함께 NLP 강의도 진행하고 있다.
- [Deep Learning Research Review Week 3: Natural Language Processing](https://adeshpande3.github.io/adeshpande3.github.io/Deep-Learning-Research-Review-Week-3-Natural-Language-Processing)  
NLP를 위한 딥러닝 기법, CNN, RNN, GRU, LSTM등을 총 망라.
- [Deep Learning for NLP](http://lxmls.it.pt/2014/socher-lxmls.pdf)  
Richard Socher가 2014년 리스본 ML 섬머 스쿨에서 발표한 자료. NLP를 위한 딥러닝 기술을 설명하는 자료인데 너무 길어서 아직 다 읽어보진 못함. 다른 얘기지만 상당히 매력적으로 생긴 사람. AI For Everyone이란 주제로 진행된 [세일즈포스 키노트](https://www.salesforce.com/video/282547/)에서 발표(메타마인드는 세일즈포스에 합병됨)한 영상에 40분부터 등장. 재킷이 어색하다며 웃는데 상당히 매력적. 여기서 마지막에 QA 시스템을 소개. 아마도 세일즈포스는 자사의 ERP, CRM에 고품질 QA를 탑재할 예정인듯.
- [Deep Learning for NLP](https://media.wix.com/ugd/142eb4_7581cfcf090e4e31a52599315f77c648.pdf)  
Richard Socher가 비슷한 내용으로 [2016년 딥러닝 스쿨에서 발표](https://www.bayareadlschool.org/schedule)한 내용. 여기에 소위 딥러닝 본좌들이 모여 이틀간 발표를 했는데 유튜브 발표 영상도 있으니 반드시 보는 것을 추천. [1일차](https://www.youtube.com/watch?v=eyovmAtoUx0), [2일차](https://www.youtube.com/watch?v=9dXiAecyJrY) 각각 10시간 짜리.
- [Natural Language Processing (almost) from Scratch](https://blog.acolyer.org/2016/07/04/natural-language-understanding-almost-from-scratch/)  
2011년에 arXiv에 올라온 같은 제목의 논문을 소개. 참고로 이 블로그는 운영자인 Adrian Colyer가 CS 논문을 하나씩 선별하여 소개하는 블로그인데 좋은 논문들이 많이 올라온다. 블로그 제목도 the morning paper.
- [Deep Learning, NLP, and Representations](http://colah.github.io/posts/2014-07-NLP-RNNs-Representations/)

### CNN
- [Convolutional Neural Networks for Sentence Classification](https://arxiv.org/abs/1408.5882)  
문장 분류 작업을 CNN으로 학습한 워드 벡터를 이용하여 분류 실험을 진행한 논문
- [UNDERSTANDING CONVOLUTIONAL NEURAL NETWORKS FOR NLP](http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/)  
위 논문을 기반으로 NLP 문제를 CNN으로 해결하려는 시도이며 이후에 이어지는 문서에서 텐서플로우로 직접 구현. 아래 문서에서 나 또한 직접 구현해서 적용해 보았는데 다른 기법에 비해 리콜이 매우 높음. 높은 리콜이 필요한 문장 분류에 적용하면 효과적일듯.
- [합성곱 신경망(CNN) 딥러닝을 이용한 한국어 문장 분류](http://docs.likejazz.com/cnn-text-classification-tf/)

### RNN, LSTM
- [INTRODUCTION TO RNNS](http://www.wildml.com/2015/09/recurrent-neural-networks-tutorial-part-1-introduction-to-rnns/)  
이 글 이후에 시리즈로 GRU/LSTM까지 소개한다. 앞서 CNN 샘플과 함께 구글 브레인에 근무하는 Denny Britz가 운영하는 훌륭한 블로그.
- [Recurrent Neural Network (RNN) Tutorial - Part 1](http://aikorea.org/blog/rnn-tutorial-1/)  
마침 찾아보니 AI Korea의 번역이 있다. 총 4개의 시리즈 문서가 모두 번역되어 있음. 하지만 아쉽게도 최근 블로그 운영은 중단된 상태다.
- [The Unreasonable Effectiveness of Recurrent Neural Networks](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)  
Karpathy의 Char-RNN 소개
- [Unfolding RNNs](http://suriyadeepan.github.io/2017-01-07-unfolding-rnn/)  
마찬가지로 인도의 한 과학자가 정리한 내용. 깔끔한 다이어그램이 돋보인다.
- [초보자를 위한 RNNs과 LSTM 가이드](https://deeplearning4j.org/kr/kr-lstm)
- [DL4J와 RNNs (Recurrent Neural Networks)](https://deeplearning4j.org/kr/kr-usingrnns)
- [Understanding LSTM Networks](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)

### TensorFlow, Keras
- [텐서플로우(TensorFlow)를 이용해 자연어를 처리하기(NLP)](http://solarisailab.com/archives/374)  
텐서플로우로 워드 임베딩을 처리한 자료와 코드 제공
- [Bidirectional LSTM for IMDB sentiment classification](https://transcranial.github.io/keras-js/#/imdb-bidirectional-lstm)  
LSTM을 이용한 IMDB 댓글의 감정 분류를 js로 구현. 예전 Karpathy의 [ConvNetJS](http://cs.stanford.edu/people/karpathy/convnetjs/)는 CNN 이미지 처리에 특화되어 있고 학습 자체도 js에서 직접 해야 하는 한계가 있었는데 이 라이브러리는 서버의 Keras에서 학습을 진행하고 학습셋을 js에서 가져와 사용하므로 훨씬 유용하다. 
- [Theano, Keras 튜토리얼 중국어 자료](http://blog.csdn.net/niuwei22007/article/category/5868745)  
- [Keras로 Multi Layer Perceptron 구현하기](http://iostream.tistory.com/111)
- [Deep Language Modeling for Question Answering using Keras](http://benjaminbolte.com/blog/2016/keras-language-modeling.html)

### 강화 학습
- [Simple reinforcement learning methods to learn CartPole](http://kvfrans.com/simple-algoritms-for-solving-cartpole/)  
OpenAI gym에서 만나는 가장 쉬운 강화학습 샘플인 카트폴을 상세히 풀이하여 소개. 놀랍게도 작성자가 고등학생이다.
- [강화학습 튜토리알 - 인공 신경망으로 '퐁' 게임을 학습시키자](http://keunwoochoi.blogspot.kr/2016/06/andrej-karpathy.html)  
Karpathy의 Pong 강화학습 튜토리얼을 한글로 훌륭하게 번역
- [Simple Reinforcement Learning](https://medium.com/@awjuliani)  
텐서플로우를 이용한 강화학습 자료를 올리고 있는 Arthur Julinani의 미디엄

## 책
NLP를 위한 딥러닝을 실제 서비스에 적용하면서 매우 다양한 책을 구매하여 읽어보았다. 구매하여 읽었던 책 목록과 간략한 소감을 정리해본다.

- [마스터 알고리즘](http://book.daum.net/detail/book.do?bookid=KOR9791185459547)  
인공지능으로 나아가는 마스터 알고리즘이 존재할 것이다 라는 전제하에 각 문파들의 각종 기술과 최고 수준의 필살기를 하나씩 소개하며 끄집어 내는 책. 비개발자를 위한 책이지만 각 알고리즘의 명칭을 들어본 적이 전혀 없다면 이해하기가 쉽지 않음. 이미 알고리즘과 머신러닝에 대해 잘 알고 있다면 재밌게 읽을 수 있다.
- [불멸의 이론](http://book.daum.net/detail/book.do?bookid=KOR9788958626190)  
마찬가지로 재밌게 읽을 수 있는 역사책(?)이다. '베이즈 정리는 어떻게 250년 동안 불확실한 세상을 지배하였는가' 부제가 딱 어울리는 책.
- [인공지능 현대적 접근방식](http://book.daum.net/detail/book.do?bookid=KOR9791185890418)  
가뜩이나 책 내용이 복잡한 수식으로 가득찬 어려운 이론서인데, 번역 또한 이해하고 풀어쓴게 아니라 원문의 직역에 가깝기 때문에 한국어로 읽었을때 도무지 무슨 말인지 이해할 수가 없다. 차라리 원서를 보는 편이 이해가 더 빠르다. 개인적으로 직역은 절대 피해야 한다는 지론을 갖고 있는데 아래에 소개하는 '텐서플로 첫걸음'이 완벽하게 이해하고 의역한 모범 사례를 보여준다면 이 책은 이해하지 못한 상태에서 번역하면 어떻게 되는지를 보여준 나쁜 사례로 볼 수 있다. 안타까운 부분이다.
- [밑바닥부터 시작하는 딥러닝](http://book.daum.net/detail/book.do?bookid=BOK00031872854YE)  
라이브러리를 사용하지 않고 직접 알고리즘을 구현하며 원리를 설명하는 좋은 책. 실제 서비스에서는 결국 라이브러리를 사용할 수 밖에 없지만 이렇게 원리를 밑바닥 부터 이해해야 제대로 된 서비스 구현이 가능하다.
- [Building Machine Learning Systems with Python](http://book.daum.net/detail/book.do?bookid=KOR9788960777613)  
scikit-learn을 이용, 따라하기 식으로 구현하는 있는 머신러닝 책. 딥러닝은 아니지만 머신러닝을 직접 구현해보고 이해하는데 큰 도움이 된다.
- [텐서플로 첫걸음](http://book.daum.net/detail/book.do?bookid=KOR9788968484902)  
바르셀로나의 카탈루냐 공과대학교 교수인 Jordi Torres가 적은 튜토리얼을 번역한 책. 한글로 된 매우 훌륭한 블로그인 [텐서플로우 코리아 블로그](https://tensorflow.blog/)의 운영자가 직접 번역한 책. 기술을 이해하고 번역한 책이라 그런지 번역이 매우 자연스럽고 번역서 부록인 RNN, LSTM 섹션도 읽을만함. 딥러닝 개념을 이해한 상태에서 텐서플로우 활용법을 처음 접하기에 좋은 책
- [집단지성 프로그래밍](http://book.daum.net/detail/book.do?bookid=KOR9788979145625)  
이 책의 원서는 출간된지 거의 10여년이 지났는데 놀랍게도 랭킹 구현에 딥러닝을 사용하고 있다. 물론 당시에는 딥 하진 않았지만 신경망의 개념을 그대로 사용하고 있고 역전파도 직접 구현했다.
- [파이썬 라이브러리를 활용한 데이터 분석](http://book.daum.net/detail/book.do?bookid=KOR9788968480478)  
데이타 시각화에 관한 책
- [인공지능, 머신러닝, 딥러닝 입문](http://book.daum.net/detail/book.do?bookid=KOR9791158390419)  
번역서가 아닌 빠르게 나온 국내서로 머신러닝의 역사와 개념을 잡는데는 도움이 된다. 그런데 본격적인 알고리즘 설명 책도 아니면서 수식을 함께 나열하는 것은 다소 무리가 있다는 생각.
- [Python Machine Learning](http://book.daum.net/detail/book.do?bookid=BOK00027563049YE)  
앞서 신경망 섹션에서 소개한 Raschka가 적은 책. 블로그를 참 잘 적는데 책 내용도 깔끔하게 정리되어 있다. 아쉽게도 번역서는 나오지 않았다.
- [Data Science from Scratch](http://shop.oreilly.com/product/0636920033400.do)  
국내에는 '데이타 과학'이란 이름으로 번역서가 나왔으나 아직 원서만 읽어본 상태. 선형대수, 확률, 통계등 이론적 기반을 주로 다룬다.
- [Artificial Intelligence](https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/)  
깃북에 있는 내용이다 보니 이걸 책으로 분류해야 할 지 문서로 분류해야 할 지 헷갈리는데 다루는 내용이 방대하고 길기 때문에 일단 책으로 분류. 여러가지 개념들을 알기쉽게 상세히 소개하고 있다.
- [Python Data Science Cookbook](https://www.packtpub.com/big-data-and-business-intelligence/python-data-science-cookbook)  
마찬가지로 이론적 기반을 주로 다루고 scikit-learn을 이용해 따라해보는 예제들로 구성되어 있다. 번역서는 나오지 않음.
- [Think Bayes: Bayesian Statistics Made Simple](http://www.greenteapress.com/thinkbayes/html/index.html)  
온라인에서 전문을 볼 수 있으며 PDF로 전체를 다운로드 할 수 있다. 주로 베이즈를 중심으로 한 이론적 기반을 다루지만 복잡한 수식보다는 파이썬 코드로 쉽게 따라해 볼 수 있는데 중점을 둔 책.