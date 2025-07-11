---
layout: post
title:  "📝 Frequency recognition based on canonical correlation analysis for SSVEP based BCIs"
date:   2025-07-11
categories: BCI CCA Biocomputing
---
Paper Review : Frequency recognition based on canonical correlation analysis for SSVEP based BCIs

[1_Frequency_recognition_based_on_canonical_correlation_analysis_for_SSVEP_based_BCIs.pdf](/assets/posts/0711-2/1_Frequency_recognition_based_on_canonical_correlation_analysis_for_SSVEP_based_BCIs.pdf)

-IEEE, 2007

## Introduction

- frequency-coded selection by SSVEP

 BCI 사용자는 해당 LED(X Hz로 깜빡임)를 응시함으로써 '음악 끄기'라는 명령을 표현할 수 있다. 

이때, 깜빡이는 LED의 기본 주파수와 유사한 주파수를 가진 SSVEP가 사용자의 EEG에서 유도되고 관찰된다. 

따라서 사용자가 의도한 명령은 EEG 신호를 분석하고, SSVEP와 관련된 주파수 정보를 추출하여 결정할 수 있다.

- PSDA(Power Spectral Density based Analysis)

사용자 EEG 신호 peak가 시각 자극 freq

Periodogram은 DFT로 바로 계산할 수 있는 non-parametric method

FFT(fast Fourier transform)가 사용됨

  
*Parametric vs Non-parametric

모집단으로부터 계산한 수치일 경우 **모수(parameter)** 

표본집단으로부터 계산한 수치일 경우 **통계량(statistic)**

Parametric method : Central limit theorem

Non-parametric: 

사전 순서 선택 필요 없고 구현 쉬움

데이터가 노이즈에 오염됐을 때도 덜 민감함

단점! 단일 채널에서 분석될 때 여전히 노이즈에 민감함
  
CCA 같은 Array signal processing으로 SNR 개선할 수 있음

paper → 다중 채널에서 CCA 기반 freq recognition approach 제안

- CCA

두 데이터 세트 간에 일정한 상관이 있을 때 사용되는 multivariable statistical method

Canonical Variable: 한쪽 독립 변수 집단을 선형 결합으로 표현

1. 선형 결합 쌍을 찾는다(상관 최대화)
2. 첫 번째 쌍과 상관없는( $Cov=0$) 두 번째 쌍을 찾음(다음 최대화)
3. canonical variable 쌍 개수가 작은 세트의 변수 개수 될 때까지

paper → 가장 큰 상관 계수만 고려
  
일반적인 상관 관계는 두 변수 간 관계

CCA는 두 세트의 변수 간 관계

![image.png](/assets/posts/0711-2/image.png)

```math
w=(a_1, a_2, ... , a_p)^T, v=(b_1, b_2, ..., b_q)^T
```

$$
z_x=Xw,z_y=Yv
$$

$z_x$와 $z_y$의 상관을 최대화하는 $w,v$를 구하는 것

$$
\begin{equation}
\begin{split}
w^*,v^*=\argmax_{w,v}corr(Xw, Yv)\\
=\argmax_{w,v}\frac{w^T\sum_{xy}v}{\sqrt{w^T\sum_{xx}w}\sqrt{v^T\sum_{yy}v}}
\end{split}
\end{equation}
       
$$

Pearson Correlation Coefficient(피어슨 상관계수)

$\rho_{XY}=\frac{Cov(X,Y)}{\sigma_X\sigma_Y}$

$Cov(X,Y)=E[(X-\mu_X)(Y-\mu_Y)]=E[XY]-\mu_X\mu_Y$

[https://elementary-physics.tistory.com/188](https://elementary-physics.tistory.com/188)

$w_i^T\sum_{ij}w_j=w_i^TX_i^TX_jw_j=(X_iw_i)^TX_jw_j=z_i^Tz_j$

$$
w^*,v^*=\argmax_{z_x,z_y}\frac{z_x^Tz_y}{\sqrt{z_x^Tz_x}\sqrt{z_y^Tz_y}}
$$

$$
||z_x||_2=||z_y||_2=1
$$

$$
w^*,v^*=\argmax_{z_x,z_y}(z_x^T z_y)
$$

$Cov(z_x^i,z_x^j)=Cov(z_y^i,z_y^j)=0$   for  $i{=}\mathllap{/\,}j$ 

: canonical variable 쌍끼리 독립(상관 없음) 전제

출처: [https://pyromaniac.me/entry/Canonical-Correlation-Analysis-CCA](https://pyromaniac.me/entry/Canonical-Correlation-Analysis-CCA)

## Method

### Subjects & Settings

CRT 화면  가상 키보드가 시각 자극기로 사용됨

각 키가 특정 주파수로 깜빡이고 이걸 응시할 때 SSVEP 발생

10/20 시스템 사용

sampling rate : 2048 Hz → Downsampling 256 Hz까지

9개의 자극 주파수(27, 29, 31, 33, 35, 37, 39, 41, 43 Hz)

11명 9개 자극 9번 (within subject)

22-48 Hz bandpass filter

### EEG Frequency Component Analysis based on CCA

set 1은 여러 채널에서 기록된 signals, $x(t)$/ set 2는 자극 신호

periodic signal → Fourier series

$$
y(t)=\begin{pmatrix}
y_1(t)\\
y_2(t)\\
y_3(t)\\
y_4(t)\\
y_5(t)\\
y_6(t)
\end{pmatrix}
=\begin{pmatrix}
sin(2\pi ft)\\
cos(2\pi ft)\\
sin(4\pi ft)\\
cos(4\pi ft)\\
sin(6\pi ft)\\
cos(6\pi ft)
\end{pmatrix},
t=\frac{1}{S}, \frac{2}{S}, \frac{T}{S}
$$

$f$는 base freq,  $T$는 number of sampling points, $S$는 sampling rate

brain dynamics는 low-pass filter 수행, high harmonic components는 필터링됨(위 6개 남음)

the largest coefficient 갖는 freq가 SSVEP 주파수로 인식

![image.png](/assets/posts/0711-2/image1.png)

### Recognition Strategy

Detect the frequency of the SSVEP component in EEG

K stimulus freq, N channels within Ls window

stimulus frequency,  $f_s=max_{f}\rho(f)$,  for  $f=f_1, f_2, ...,f_K$

where $\rho(f)$ is the CCA coefficient of $x_{LN}$ and $y$

### Channel Selection

SSVEP는 localized potential

너무 넓은 영역은 주파수 성분 찾기 어려움

CCA 기반 채널 선택 방법

각 채널에 대해 M nearest neighboring channels까지 선택해서  M+1개 채널 영역 구성함

CCA coefficient 계산 → 채널의 중요도 결정

모든 자극 주파수에 대해 CCA coefficient 평균화, 가장 큰 coeff 가진 N개의 채널 선택

Fig 1: N=8, M=5

### Contrast Method

PSDA Method와 CCA method 비교

먼저, PSDA 채널 선택 → 높은 SNR 가진 최적 양극성 리드

→파워 스펙트럼

FFT 포인트 수를 256으로 설정, sampling rate 256 → 1초동안  256포인트

PSDA로 결정된 frequency

$$
f_s=\begin{cases}
f_{peak},&\text{when }f_{peak}\text{ is odd}\\
max_fP(f),\\&f=f_{peak}-1,f_{peak}+1,\\\text{ when}f_{peak}\text{ is even} 
\end{cases}
$$

$P(f)$는 Power Density value

### Evaluation Methods

cross-validation design 사용

training set(채널 선택) / test set(주파수 인식 성능)

$$
Accuracy=\frac{\text{N of samples}(f_s=f_{stimulus})}{\text{N of samples}}\times100\%
$$

$f_s$는 freq determined by recognition algorithm

$f_{stimulus}$는 real stimulus freq

N of samples=900 (9개 자극에 대해 100개씩 무작위로)

### Simulation

8개의 사인파 신호 생성, 9개 자극, 8개 채널에 대해 시뮬레이션

$$
SNR_{dB}=10log_{10}\frac{P_{signal}}{P_{noise}}=10log_{10}\frac{(A/\sqrt2)^2}{\sigma^2}
$$

A는 사인파 진폭,  $\sigma^2$는 noise의 분산

![image.png](/assets/posts/0711-2/image2.png)

$SNR_{dB}<0$: signal power가 noise보다 작다(신호 구분하기 어려움)

SNR 낮출 때(신호 품질 안 좋을수록) PSDA 정확도 급격히 낮아진 반면, CCA는 유지됨

더 많은 채널을 쓸 때 CCA 성능 좋아짐

## Result

![image.png](/assets/posts/0711-2/image3.png)

채널들은 대부분 occipital(후두부)에 위치함

SSVEP가 후두부에서 생성되는 것과 일치

### 핵심 result

- CCA approach can get higher recognition accuracy than the PSDA approach at various time window lengths for most subjects (except subject NTS)
- The result shows that the CCA approach is significantly better than the PSDA approach at most time window lengths

## Discussion

- subject NTS에 대한 해석

PSDA 신호가 너무 높은 SNR을 가졌다

SSVEP 생긴 영역이 너무 작았다

CCA 접근에서 넓은 영역의 신호를 사용하면, 노이즈가 많고 인식 정확도 낮아짐

---

- Harmonics

bandpass filter로 없앴지만, 보존하면 CCA 접근법이 더 큰 이점을 가질 수도 있음

CCA가 amplitude와 phase를 각 주파수 성분마다 고려할 수 있기 때문

---

- CCA 문제점
1. 가장 큰 coefficient만 사용함

그러나 노이즈 때문에 여러 계수에 정보가 분산될 수 있음

가장 큰 세개의 계수를 합산, 모든 계수의 곱을 사용하는 등 방법 고려

1. 사용자의 시각 경로가 선형적이라고 가정함

그러나 실제로는 비선형 처리로 구현함

1. 계수 외에도 projection을 어떻게 사용할지 고려해볼 만함