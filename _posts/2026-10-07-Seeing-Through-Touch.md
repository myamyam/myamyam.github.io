---
layout: post
title:  "📝 Seeing Through Touch"
date:   2026-10-07
categories: Tactile Multimodal localization
---
Paper Review : Seeing Through Touch : Tactile-Driven Visual Localization of Material Regions

[Seeing_Through_Touch.pdf](/assets/posts/1007/(CVPR_2026)_Seeing_Through_Touch.pdf)

-CVPR, 2026

## Contribution

- local visuo-tactile alignment model (produces dense tactile saliency map)

- a material-diversity pairing strategy from in-the-wild, scene-level multi-material images
  -> local visuo-tactile correspondence &uarr;, robustness to weak tactile signals &uarr;

- new tactile-grounded material segmentation datasets

## Keyword $ Concept

**dense tactile saliency map**
주어진 tactile input과 촉감이 비슷할 것 같은 이미지영역 heatmap
값이 높을수록 image 위치의 local visuo-tactile correspondence 높다

$$f_t\in \mathbb{R}^{C\times{H}\times{W}}$$
$$\bar{f_t}=avg_{h,w}(f_t[h,w])$$
$$f_v\in \mathbb{R}^{C\times{H}\times{W}}$$
$$M[h,w]=\bar{f_t} \cdot f_v[h,w]$$

cf)visual saliency map
이미지에서 시각적으로 중요한 부분
<-> tactil map은 tactile input을 기준으로, 이미지에서 어느 영역이 대응되는가

**dense cross-modal feature interaction**

image spatial location과 tactile feature를 위치 별로 비교
→ dense similarity map

기존 global alignment 방식의 similarity는 비슷하다/ 안 비슷하다로 나누는 한계가 있다.

## Conclusion

- The tactile localization framework (fine-grained alignment between tactile and visual scene) overcomes the limitations of existing visuo-tactile methods (global-alignment objectives)

## Introduction
