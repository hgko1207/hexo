---
title: 인공지능 개발준비 - 개발환경 구축(Windows)
categories:
  - Programming
  - AI
tags:
  - AI
  - TensorFlow
  - Python
date: 2020-06-30 11:34:28
thumbnail: /images/thumbnail/ai.png
---

인공지능(AI)을 통해 개발을 하기 위해 개발 도구들을 설치합니다.

## 1. Anaconda 설치

Anaconda는 여러가지 수학 및 과학 패키지들을 기본적으로 포함하고 있는 Python 배포판입니다. 그래서 머신러닝, 딥러닝, 데이터 분석에서 사용을 하려고 한다면 Anaconda를 통해 설치하는 것이 좋습니다.

[Anaconda Download](https://www.anaconda.com/products/individual) 사이트에 접속하여 아래로 내려가 보면 다운로드 화면이 보입니다.
현재 Windows 운영체제에 맞게 선택하여 다운로드를 합니다.

![](/images/ai/1.PNG)

다운로드가 완료되면 설치를 진행합니다.

`Next` 버튼을 클릭하다가 아래 그림처럼 `All Users`를 선택합니다.
간혹 Windows에서 사용자의 계정을 한글로 만들었을 경우 설치할 때 또는 개발할 때 에러가 날 수 있기 때문에 선택합니다.

![](/images/ai/2.png)

아래 그림처럼 체크박스도 선택을 하여 환경변수 설정이 되도록 합니다.

![](/images/ai/3.png)

`Install` 버튼을 클릭하면 설치가 됩니다.

설치가 잘 되었나 확인하려면 **workspace** 폴더에서 커맨드 창을 열고 아래 명령어를 입력합니다.

```bash
c:\workspace> jupyter notebook
```

Jupyter Notebook 페이지가 실행되고 Python 코드를 작성할 수 있습니다.

![](/images/ai/4.png)

## 2. TensorFlow 설치

> TensorFlow는 머신러닝을 위한 엔드 투 엔드 오픈소스 플랫폼입니다. 도구, 라이브러리, 커뮤니티 리소스로 구성된 포괄적이고 유연한 생태계를 통해 연구원들은 ML에서 첨단 기술을 구현할 수 있고 개발자들은 ML이 접목된 애플리케이션을 손쉽게 빌드 및 배포할 수 있습니다.
> 출처 : https://www.tensorflow.org/?hl=ko

[TensorFlow 2 설치](https://www.tensorflow.org/install) 사이트에 접속합니다.
설치 가이드에 따라 설치를 합니다.

```bash
# Current stable release for CPU and GPU
$ pip install tensorflow
```

설치가 완료되면 Jupyter Notebook에서 import를 하여 확인합니다.

![](/images/ai/5.png)

## 3. Pytorch 설치

> PyTorch는 Python을 위한 오픈소스 머신 러닝 라이브러리입니다. Torch를 기반으로 하며, 자연어 처리와 같은 애플리케이션을 위해 사용됩니다.
> 출처 : [위키백과](https://ko.wikipedia.org/wiki/PyTorch)

[Pytorch](https://pytorch.org/) 사이트에 접속합니다. 아래로 내려가 보면 여러가지 설정을 하여 설치하는 방법을 안내해줍니다.

Windows 버전이기 때문에 아래 그림 처럼 설정을 합니다.
만약에 GPU를 사용할 수 있으면 CUDA 버전에 맞게 설정하면 됩니다.

![](/images/ai/6.png)

설정이 완료되었으면 **Run this Command** 칸의 내용을 복사하여 Command 창에 붙여넣기 하고 실행을 합니다.

![](/images/ai/7.png)

TensorFlow와 마찬가지로 Jupyter Notebook에서 import를 하여 설치가 완료되었는지 확인합니다.

![](/images/ai/8.png)

**AI 개발 준비가 모두 완료 되었습니다.**
