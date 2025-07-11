---
layout: post
title:  "📝 High speed spelling with a noninvasive brain-computer interface"
date:   2025-07-11
categories: BCI Biocomputing
use_math: true
---
Paper Review : High speed spelling with a noninvasive brain-computer interface

[High-speed-spelling-with-a-noninvasive-brain-computer-interface.pdf](/assets/posts/0711/chen-et-al-high-speed-spelling-with-a-noninvasive-brain-computer-interface.pdf)

## Abstract/ Keyword

- SSVEP(Steady-State Visual Evoked Potentials)
- ITR(Information Transfer Rates)
- JFPM(Joint Frequency Phase Modulation)

## Intro

SSVEP 기반 방식으로 더 빠른 BCI 구현

기존 P300 방식은 낮은 정보전달률(ITR) : 1초에 0.5비트(0.5 bps)

### Hypo

single-trial에서 SSVEP 주파수, 위상이 안정적이라면 매우 빠르고 정확한 spelling 가능

### Contribution

JFPM 도입→ 서로 가까운 주파수 자극 구별 가능

사용자 맞춤 알고리즘

0.5초 자극으로 spelling → 최대 60자/min 5.32bps

## Results

### Spelling with an SSVEP-based BCI

![image.png](/assets/posts/0711/image.png)

![image.png](/assets/posts/0711/image1.png)

![‘H’와 ‘I’ spelling 과정](/assets/posts/0711/image2.png)

‘H’와 ‘I’ spelling 과정

⇒ ITR: 최대 5.32bps // Spelling rate: 60 char /min

### Stimulation Signal and Elicited SSVEPs

40개 시각 자극 어떻게 설계되었는지, 그에 따른 SSVEP 분석

![12.2 / 12.4 / 12.6 Hz 세가지 신호와 그에 대한 SSVEP(A,B는 freq / C,D는 phase, angle(complex))](/assets/posts/0711/image3.png)

12.2 / 12.4 / 12.6 Hz 세가지 신호와 그에 대한 SSVEP(A,B는 freq / C,D는 phase, angle(complex))

둘이 높은 일치도 보임 → synchronous demodulation

### JFPM

Phase coding + frequency coding

adjacent frequencies 사이에 phase간격을  넣어서 타겟 간 구분 가능성 높임

위상 간격은 SSVEP 파형 간 차이를 최대화하도록

0.5 $\pi$ 일 때, SSVEP 상관계수가 음수로 바뀌어서 구분 가능성 높아짐

### Optimization of phase interval and stimulation duration

Phase interval은 인접 주파수 성분 간 구분 정도 결정

자극 시간은 SNR(Signal-to-noise ratio)에 영향

최적 → 0.5 $\pi$간격, 0.5초

### Online Spelling Performance

### Discussion

낮은 통신 속도가 BCI Speller에서 큰 문제

이 연구가 가장 높은 정보 전송률(ITR)을 보임

성능 향상 방향

- 자극시간 최적화
- 필터뱅크의 서브밴드 수 늘리기
- 주파수+위상 결합 전략 최적화