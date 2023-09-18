---
title: Deep Learning 개요 (feat. PyTorch)
date: 2023-03-13-09:58:00 +0900
categories: [DL Framework, PyTorch]
tags: [PyTorch, Overview]
pin: true
---
  
> 더 많이 배울수록 더 많이 잊어버리는 문제점을 해결하고자
> 개념들의 관계를 정립하기 위한 개요 글을 작성하게 되었습니다.
> 해당 게시글은 지속적으로 업데이트할 예정입니다.
{: .prompt-info }

## 모델 개요

## 구현 개요(PyTorch)

### 1. 데이터 준비

- [Tensor](https://www.notion.so/Tensor-b626c55dfd82419993d69a0f873c7f7a?pvs=21)
- [PyTorch Datasets & DataLoaders](https://www.notion.so/PyTorch-Datasets-DataLoaders-5b1bb513ae23495ea3bca27d8541e92d?pvs=21)

### 2. 모델 정의 ([torch.nn.Module](https://www.notion.so/torch-nn-Module-fc3f68055ff1435d9c0de1567fc852bb?pvs=21))

[PyTorch **모델 불러오기**](https://www.notion.so/PyTorch-8907c68e40d2445ca3452f1c4f26a00c?pvs=21)

- Input size, Output size 정의 [nn.Parameter](https://www.notion.so/nn-Parameter-53ff052828634ab198c57731649fe73f?pvs=21)
- Forward 연산 정의 [PyTorch Functions](https://www.notion.so/PyTorch-Functions-1547d3e39c754068a174bc68f84fa87b?pvs=21)
- [Backward](https://www.notion.so/Backward-bbfb5deede994f9f832d5ebe72e53955?pvs=21) 연산 정의

### 3. 하이퍼 파라미터 지정 [**Hyperparameter Tuning**](https://www.notion.so/Hyperparameter-Tuning-13b3e8b1be0146c9939fd58f466abb43?pvs=21)

### 4. 모델 평가 기준 및 Optimizer 설정

1. 모델 평가 기준 : loss를 어떻게 계산할 것인가? [손실 함수(Loss Function)](https://www.notion.so/Loss-Function-82e9c926f33a42a8a50ef8febd5c4ab6?pvs=21)
    - 가장 간단하게 |실제 값 - 예측 값|으로 하겠다! → MAE(Mean Absolute Error)
    - 값이 너무 큰가? MAE에 루트를 씌우자! → MSE(Mean Squared Error)
2. [Optimizer](https://www.notion.so/Optimizer-39716b1340f748e48152500d7c60f67e?pvs=21) 설정
    - 반영 방법 : loss의 미분값을 파라미터에 어떻게 반영할 것인가?
    - Learning rate : 한 번에 얼마나 반영할 것인가?

### 5. 모델 학습 (1 epoch에 일어나는 일)

1. `optimizer.zero_grad()` : 이전 epoch의 미분값 초기화
    - optimizer.zero_grad()를 안하면 어떤 일이 일어날까?
    - 매 batch step마다 항상 필요할까?
2. `outputs = model(inputs)` : 모델 예측 수행
3. `loss = criterion(outputs, labels)` : 손실 함수를 통한 loss 계산
4. `loss.backward()` :  loss의 미분값 계산
5. `optimizer.step()` : 미분값을 parameter에 반영

[PyTorch **Multi-GPU 학습**](https://www.notion.so/PyTorch-Multi-GPU-cddece8aedc84060ab5baceb59821da0?pvs=21) 

### 6. 모델 성능 평가

[**Monitoring tools for PyTorch**](https://www.notion.so/Monitoring-tools-for-PyTorch-f9c8625b26ab4dd0aa4d122d4deaac44?pvs=21)

### 7. 추론

- [AutoGrad 튜토리얼](https://pytorch.org/tutorials/beginner/blitz/autograd_tutorial.html)
- [Tensor와 AutoGrad 튜토리얼](https://pytorch.org/tutorials/beginner/examples_autograd/two_layer_net_autograd.html)
- [Pytorch로 Linear Regression하기](https://towardsdatascience.com/linear-regression-with-pytorch-eb6dedead817)
- [Pytorch로 Logistic Regression하기](https://medium.com/dair-ai/implementing-a-logistic-regression-model-from-scratch-with-pytorch-24ea062cd856)
- 한 epoch에서 이뤄지는 모델 학습 과정을 정리해보고 성능을 올리기 위해서 어떤 부분을 먼저 고려하면 좋을지 논의해보기
    1. 데이터 개선
    2. 모델 개선
    3. loss 개선
    4. optimizer 개선

[DL 모델 구현 예제](https://www.notion.so/DL-9c7cebfa869b40e0a88d48c071604065?pvs=21)

[**PyTorch Troubleshooting**](https://www.notion.so/PyTorch-Troubleshooting-c45a703ff84e453b87c31bba2311a578?pvs=21)