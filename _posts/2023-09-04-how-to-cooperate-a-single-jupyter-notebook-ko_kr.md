---
layout: post
title: 실시간으로 `하나의 Jupyter Notebook 을 여려명이서 공동으로 작업` 하는 방법
---

*****

# `JupyterLab` ー `Real-Time collaboration` 플러그인의 소개

안녕하세요. 여러분! 잘 지내고 계시나요? 벌써 가을로 접어들어가는 날씨가 찾아오는 것 같습니다.
다들 `Jupyter Notebook`을 사용하시다 보면, 특히 대회나 협업을 할 때에는 공동으로 작업을 해야할 때가 있는데 기억이 나실까요?
네, 맞습니다. 때로는 좋지만, 때로는 불편하기도 한 이 **`Runtime`** 이라는 친구가 있죠.
기본적으로 이 `Runtime` 이라는 친구는 각자가 하나의 `.ipynb` 라는 `Jupyter notebook` 파일을 열었을 때에 하나의 브라우저 (단, 여기서 하나의 브라우저는 하나의 웹 사이트에 대하여 하나의 세션만을 공유한다고 가정합니다.)
에서 열때 마다, 주어지는 브라우저의 세션 별로 Token 값마다 다르게 주어 집니다.

즉, 다르게 이야기 하자면 `상대방의 환`경과 `나의 환경`은 `독립적인 환경`이라는 뜻이 됩니다.
상대방에서 실행한 내용이나, 불러오기한 작업이 내가 열고있는 웹 브라우저에서는 반영이 되지 않는다는 이야기 입니다... 안타까운 이야기죠.

하지만 우리는 대회를 나가거나 협업을 할 때에, 한정된 H/W 리소스를 이용해 같이 호흡을 맞춰가며 모니터링 해보는 것이 더 중요한 상황이 있을 수도 있습니다.
이럴 때를 위해 나온 것이 `Jupyter Lab`의 `Real-Time collaboration` 플러그인 입니다.


# 설치부터 시작까지
앞선 내용에서 눈치를 채신 분들도 계시겠지만, 사실 이 기능은 `Jupyter Notebook`이 아닌 `Jupyter Lab` 에서 제공하는 기능입니다.
간략 하게 소개를 드리면 `Jupyter Notebook`과 `Jupyter Desktop`의 개념을 더 확장하여 더 많은 작업과 기능을 처리하는 것을 목표로 하는 `Project Jupyter`의 일환(일부분) 입니다.
그럼, `Jupyter Lab`의 설치부터 시작해 볼까요?

*****

## 1. `Jupyter Lab` 설치
[Reference](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html)

사용하시는 환경에 따라서, 설치방법이 조금씩 다릅니다.
-  **conda**
   - `conda` 를 사용하시는 분들은 아래의 명령어로 터미널 창에서 입력하여 설치해주세요.
        ```shell
        conda install -c conda-forge jupyterlab
        ```
- **mamba**
   - `mamba` 를 사용하시는 분들은 아래의 명령어로 터미널 창에서 입력하여 설치해주세요.
        ```shell
        mamba install -c conda-forge jupyterlab
        ```

- **pip**
  - `pip` 를 사용하시는 분들은 아래의 명령어로 터미널 창에서 입력하여 설치해주세요.
       ```shell
       pip install jupyterlab
       ```
  - macOS를 사용중인 환경이고, python2가 기본값인 경우에는 `pip` 대신에 `pip3` 로 대체하여 사용해 주세요.


만약, 설치시에 에러가 발생한다면, 아래의 링크를 참고하여 에러를 해결해보세요! <br/>
- [설치시 발생하는 문제들의 해결방법](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html#installation-problems)

*****

## 2. `Jupyter Lab` 실행 테스트

자, 이제 실행을 해보겠습니다!
- 터미널에서 아래와 같이 입력해 주세요!
  ```shell
  jupyter lab
  ```

그리고, 잠시만 기다리면... 두근두근 두근!

브라우저로 아래와 같은 탭이 열리게 됩니다!<br/>
![Jupyter Lab](https://cellularhacker.github.io/public/images/jupyterlab_startup-001.png)

*****

## 3. `Jupyter Lab` ー `Real-Time collaboration` 플러그인 설치
[Reference](https://jupyterlab-realtime-collaboration.readthedocs.io/en/latest/)

이번에도 역시, 사용하시는 환경에 따라서 설치방법이 조금씩 다르지만 앞선 방법과 거의 다르지 않습니다.
- **conda**
  - `conda` 를 사용하시는 분들은 아래의 명령어로 터미널 창에서 입력하여 설치해주세요.
       ```shell
       conda install -c conda-forge jupyter-collaboration
       ```
- **mamba**
  - `mamba` 를 사용하시는 분들은 아래의 명령어로 터미널 창에서 입력하여 설치해주세요.
       ```shell
       mamba install -c conda-forge jupyter-collaboration
       ```
- **pip**
  - `pip` 를 사용하시는 분들은 아래의 명령어로 터미널 창에서 입력하여 설치해주세요.
       ```shell
       pip install jupyter-collaboration
       ```
  - macOS를 사용중인 환경이고, python2가 기본값인 경우에는 `pip` 대신에 `pip3` 로 대체하여 사용해 주세요.
## 4. `Jupyter Lab` - `Real-Time collaboration` 플러그인의 정상 동작 실행 테스트

*****

### 4-1. `Jupyter Lab`을 실행하여 웹브라우저에서 확인하기

자, 이제 실행을 해보겠습니다!
- 터미널에서 기존에 실행했던 `Jupyter Lab`을 완전히 종류해주신 후에 다시 한번 아래의 명령어로 `Jupyter Lab`을 실행해 주세요.
     ```shell
     jupyter lab
     ```

![Jupyter Lab - RTC](https://cellularhacker.github.io/public/images/jupyterlab_rtc-001.png)

어라, 아까와는 전혀 다른 내용을 볼 수 있습니다.


네. 그렇습니다. **`RTC`** 라는 글자가 정면의 `Launcher` 탭의 화면에 있는 것을 확인 할 수 있습니다.
바로, `Real-Time Collaboration`을 줄인 말이겠죠.

*****

### 4-2. `Jupyter Lab`에서 새로운 `.ipynb` 파일을 생성하고, 다른 브라우저에서 확인해보기

[![Jupyter Lab - RTC Demo](https://cellularhacker.github.io/public/images/jupyterlab_rtc-001.png)](https://cellularhacker.github.io/public/images/jupyterlab-rtc_demo.mp4)

*****

### 4-3. `Jupyter Lab`에서 `Real-Time Collaboration`을 사용한 결과보기
![Jupyter Lab - RTC Result](https://cellularhacker.github.io/public/images/jupyterlab_rtc-002.png)

*****

감사합니다!
