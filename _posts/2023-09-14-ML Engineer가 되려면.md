---
title: ML Engineer가 되려면 이정도는 알아야지
categories: ['AI','ML Engineering']
date: 2023-09-14-13:50:00 +0900
tags: ['ML Engineer']
pin: true
---

> ML 엔지니어 취업을 위해 핵심이라고 생각하는 내용을 정리하는 공간입니다.  
> 지속적으로 업데이트할 예정이며, 저의 공부 계획이기도 합니다.  
> AI 취업을 목표로 하시는 분들에게 도움이 될 것이라 생각합니다.
{: .prompt-info }


## 모델은 어떻게 동작하는가?

- 기본적인 코드 흐름
    
    [Deep Learning 개요](https://www.notion.so/Deep-Learning-62ff59f06fad4a9aba4608d90c1e5bda?pvs=21)
    
    [DL 모델 구현 예제](https://www.notion.so/DL-9c7cebfa869b40e0a88d48c071604065?pvs=21)
    
    
- .cuda()가 붙으면 동작이 어떻게 달라지는가?
    
    ```python
    # Converting inputs and labels to Variable
        if torch.cuda.is_available():
            inputs = Variable(torch.from_numpy(x_train).cuda())
            labels = Variable(torch.from_numpy(y_train).cuda())
        else:
            inputs = Variable(torch.from_numpy(x_train))
            labels = Variable(torch.from_numpy(y_train))
    ```
    
- 모델 학습 형태 파악하기
    
    [ML — ipynb](https://www.notion.so/ML-ipynb-4583d3ccee854125a15a4c07e4efb58e?pvs=21)
    
    [DL — ipynb](https://www.notion.so/DL-ipynb-bb55e13e26364249b6fa10876022f95b?pvs=21)


## 모델을 어떻게 설계하는가?

- 논문 보고 모델 구현하기

- 오픈 소스 기여하기

## 모델을 어떻게 활용하는가?



3. 모델링 Scheme 구현하기
4. 나만의 ML 프로젝트 템플릿 만들기