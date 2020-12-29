---
title: "DewarpNet Paper 공부"
date: 2020-12-29 14:33:41
categories: Deep-Learning
---


# DewarpNet paper

## 0. Abstract

모바일 장치로 문서 이미지를 촬영하여 자동으로 정보를 추출하는 것은 효율적이지 않다. 

조명, 상태, 왜곡 등에 영향을 많이 받기 때문이다.

DewarpNet은 single image에서 딥러닝을 이용해 문서를 unwarp 할 수 있다. 

Our insight : 

3D geometry of the document determines..

- warping of its texture
- illumination effects

end-to-end pipeline을 통해 document paper의 3D shape을 modeling 한다. 

## 1. Introduction

    

이미지를 캡쳐(사진)하는 경우에도 그 퀄리티가 일반적인 문서 스캔 결과와 비슷하기를 바란다. 하지만 uncontrollable 한 factor들 (실제 문서의 변형, 카메라 포지션, 조명 등) 때문에 결과가 좋지 않은 경우가 많다. 

기존 방법은 종이의 3D shape을 추측하고, flat 한 이미지를 계산하는 방식을 사용했다. 

결과적으로, raw image들은 automatic information extraction에 적합하지 않은 경우가 많다. 

이 방법의 문제점은 계산이 상당히 비싸며 느리다는 것이다. 

다른 lab에서 deep learning을 이용한 방식을  개발했지만, training dataset이 2D image에서 부터 생성되기 때문에, 비현실적인 테스트 결과를 생성 했다. 

Paper folding은 3D 에서 발생하는 일이다 : 3D shape은 같고 different texture를 가진 종이들은 같은 변형으로 unwarped 될 수 있다. 따라서, 3D shape은 unwarped paper를 복구하는데 가장 중요한 단서이다. 

이러한 아이디어에 기반을 두고, 우리는 unwarping operation을 위한 명시적인 3차원 shape 표현을 활용하는 unwarping framework, DewarpNet을 제안한다. 

DewaprNet은 두 개의 sub-network들을 가지고 두 개의 stage에서 동작한다. 

1. **Shape Network**

    Shape Network는 변형된 문서 이미지를 input으로 받아들이고, unwarping task에 사용하기 적합한 3차원 좌표계 map을 출력한다. 

2. **Texture Mapping Network**

    Texture Mapping Network는 변형된 문서 이미지를 평평한 문서 이미지로 backward map 한다. 

    (backward map : 결과물에서 다시 input을 추측하는 것?)

우리는 두 개의 sub network를 즉각적인 (우리가 추측한) 3D shape 에서의 regression loss와 final unwarping result 를 통해 학습시킨다. 

regression loss : 데이터를 선형적으로 표현할 수 있는 하나의 직선을 찾는 것

이후, 우리는 refinement network를 통해 flat한 rectified 된 image의 shading effect를 제거한다. 

Training을 위해서, 우리는 DOC3D dataset을 생성했다. 

우리는 Doc3D를 다음과 같은 방법으로 생성했다. 

1. 자연적으로 warp 된 paper들의 3D mesh를 capture 한다. 
2. 광범위하고 사실적인 문서 texture를 생성한다. 
3. 둘을 합친다. 

각 데이터는 풍부한 정보들과 함께 제공된다. 

- 3D coordinate maps
- surface normals
- UV texture maps
- Albedo maps

방대한 dataset으로 학습된 DewarpNet은 다른 모델들과 비교해 최고의 성능을 보여 준다. 

실제로 스캔한 문서들과 비교했을 때, 우리는 약 15%의 MS-SSIM를 개선하고 Local Distortion을 36% 감소시킬 수 있었다. 

(MS-SSIM : Multi Scale Structural Similarity, 유사도)

더 나아가, 우리는 OCR 에서  에러 발생률을 42%  낮출 수 있었다. 

## 2. Previous Work

1. **Parametric shape-based methods**

    Parametric shape-based method는 문서의 변형이 저차원의 parametric model들에 의해 표현되었다고 가정하며, 이러한 모델들의 parameter는 시각적으로 유추가 가능하다. 

    모델의 변형 parameter를 유추하기 위해 사용된 시각적 단서는 

    - Text line
    - document boundaries(문서 외곽선)
    - 외부 장치로부터의 laser beam (?)

    하지만, 이런 저차원 모델들은 복잡하게 변형된 모델을 유추하기는 쉽지 않다. 

2. **Non-parametric shape-based methods**

    Non-parametric shape-based methods는 반대로, 저차원 parametric 모델들에 의존하지 않는다. 

    이 방법은 주로 변형된 document paper의 mesh representation을 가정하고, 즉각적으로 mesh의 모든 point의 좌표를 추측한다. Mesh 내의 모든 point의 좌표를 추측하기 위해 사용된 방법은 

    - reference images
    - text lines
    - CNN (Convolutional Neural Network)

    이다. 

    많은 방법들이 capture 되거나 추측되어진 3D paper shape information으로부터 mesh를 재건해낸다. 

    주목할만한 예시는, 

    - 전통적인 vision으로부터 추측된 point cloud
    - multi-view images
    - structured light
    - laser range scanners

    등이 있다. 

    하지만, 위와 같은 방법들은 때때로 실용적이지 못하며 시간을 낭비하는 경우가 있다. 

    최근에, Ma et al. 에서 DocUNet을 제안했는데, DocUNet은 딥러닝으로 문서를 반전(?) 시킬 수 있는 최초의 데이터 기반 방법이다. 

    기존의 접근 방법과 비교하면, DocUNet은 inference가 빠르지만 실제 이미지에는 좋지 못한 성능을 보였는데, 이는 기존의 데이터셋들은 2D 변형만 포함하고 있었기 때문이다. 

    ## 3. Doc3D Dataset

    따라서 우리는 실제 문서 데이터와 rendering software(Blender)를 사용해  Doc3D dataset을 창조했다. 

    우리는 우선 자연적으로 변형된 실제 문서 종이의 3D shape을 확보한다. 

    그리고, 우리는 Blender에서 path tracing을 사용해 실제 문서 texture를 렌더링하였다. 

    우리는 다양한 camera position과 illumination condition들을 적용했다. 

    우리의 이러한 접근 방법의 가장 중요한 이익은, 사실적인 렌더링을 적용한 dataset이 대규모로 생성될 수 있다는 것이다. 

    또한, 우리의 방법은 다양한 타입의 ground truth를 생성한다. 타입은

    - 3D coordinate map
    - albedo map
    - normals
    - depth maps
    - UV maps

    기존의 데이터셋은 2D에서만 이루어졌기 때문에, 3D 를 활용한 우리의 dataset으로 학습시킨 딥러닝 모델이 실제 이미지로 테스트를 진행하였을 때 더 좋은 결과를 낼 것이라는 점을 쉽게 추측할 수 있다. 
    
    
    ![Doc3D dataset에서 2 개의 mesh를 이용해 생성된 이미지들](../img/dewarpNet/dewarpNet_1.png)

   ![기존의 데이터셋](../img/dewarpNet/dewarpNet_2.png)


    ### Capturing Deformed Document 3D Shape

    3D point cloud capture를 사용해 변형된 문서의 3D shape을 확보한다. 

    우리의 workstation은 

    - tabletop
    - gantry
    - depth camera level
    - relief stand

    등이 필요하다. 

 ![How to get mesh with depth camera](../img/dewarpNet/dewarpNet_3.png)

    (사용된 카메라 모델 : Intel RealSense D415 Depth Camera)

     카메라 가격
 ![ 카메라 가격](../img/dewarpNet/dewarpNet_camera.png)
         
         
    Depth 카메라를 통해, 우리는 다음과 같은 형태로 변형된 문서의 point cloud를 획득할 수 있다. 

 ![doc3d dataset 획득 과정](../img/dewarpNet/dewarpNet_4.png)

Point Cloud로부터 우리는 ball pivoting algorithm을 통해 mesh를 생성할 수 있다. 

Mesh는 ~130,000 개의 vertice들을 가지고 있으며,  270,000 개의 vertice들을 cover하는 face들을 가지고 있다. 

우리는 각 mesh를 100*100 의 균일한 mesh grid로 subsample 하여 mesh augmentation, alignment, rendering 등을 가능하게 하였다. 

각 vertex는 rendering step에서 texture mapping에 사용하기 위한 UV position을 가진다. 

Mesh의 네 개 코너에 각각 {(0,0), (0,1), (1,0), (1,1) } 를 할당하고, 모든 vertice들에 UV 값을 interpolate 하였다. 

mesh를 추가 활용하기 위해 우리는 x,y,z 축을 따라 뒤집어 결과적으로 8 개의 mesh를 생성하였다. 

또한, 65*65 ~ 95*95 크기의 다양한 view에서 random 하게 crop 된 4 개의 small mesh를 생성하였다. 

그리고 small mesh를 100*100 크기로 interpolate 하였다. 이런 추가적인 mesh들은 데이터셋의 다양성을 분명히 증가시켰다. 모든 mesh들은 절대 방향 문제 (Scale, rotation, traslation)의 문제를 해결하기 위해 정렬되었다. 

이 단계는 하나의 unique한 변형이 하나의 unique한 3D 좌표계로 표현되는 것을 확인하기 위한 것이다. 

결과적으로, 우리는 40,000개의 서로 다른 mesh를 생성하였다. 

### Document Image Rendering

Dataset의 다양성을 증가시키기 위해, rendering process에서 우리는 camera, 조명, 그리고 texture를 변경하였다. 각 이미지에서 카메라는 원형 cap에서 무작위로 놓여졌고, 이 때 "up" 방향은 -30~30도 범위 안에 있었다. 

카메라 방향은 가상 세계의 원점 주변의 작은 영역으로 제한되었다. 

우리는 70%의 이미지를 Laval Indoor HDR dataset에서 무작위로 sample 된 2100개의  lightening environment를 사용해 렌더링하였다. 

나머지 30%의 이미지는 간단한 조명 조건 하에 렌더링 되었고, 조명의 위치는 무작위로 결정되었다. 

Mesh 에 적용된 Texture는 실제 세계의 document image를 통해 획득되었다. 우리는 7,200개의 image를 사용하였다. 

각 이미지에 대해, 우리는 다음과 같은 데이터들을 생성하였다. 

- 3D coordinate map
- depth map
- normals
- UV map
- albedo map

## DewarpNet

 ![DewarpNet Framework](../img/dewarpNet/dewarpNet_5.png)

DewarpNet은 두 개의 sub-network로 구성되어 있다. 

추가적으로, 우리는 illumination effect를 조정하는 unwarped image를 시각적으로 개선하는 후처리 refinement module을 제안한다.

DewarpNet은 변형된 이미지를 input으로 받아들이고, backward mapping B를 예측한다. 

B 는 이미지 변형를 표현하는 flow field이다 : B의 각 픽셀은 입력 이미지에서 픽셀의 위치를 표현한다. 

우리는 bilinear sampling을 사용해 입력 이미지의 픽셀 값에서 final unwarped document image를 생성한다. 

### Shape Network

DewarpNet은 입력된 문서 이미지의 3D shape을 생성한다. 

우리는 이 과정을 image-to-image translation problem으로 공식화 하였다. 

Shape network는 입력 이미지 I를 3차원 좌표계 map으로 translate 한다. 

우리는 U-Net style encoder-decoder architecture를 사용해 shape network의 connection을 skip 한다 (?)

========================================================================

### U-net

U-Net은 Biomedical 분야에서 이미지 분할(Image Segmentation)을 목적으로 제안된 End-to-End 방식의 Fully-Convolutional Network 기반 모델이다. 

U-Net은 이미지의 전반적인 컨텍스트 정보를 얻기 위한 네트워크와 정확한 지역화(Localization)를 위한 네트워크가 대칭 형태로 구성되어 있다. 

 ![Unet](../img/dewarpNet/dewarpNet_6.png)

출처 : [https://medium.com/@msmapark2/u-net-논문-리뷰-u-net-convolutional-networks-for-biomedical-image-segmentation-456d6901b28a](https://medium.com/@msmapark2/u-net-%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0-u-net-convolutional-networks-for-biomedical-image-segmentation-456d6901b28a)

**Contracting Path**

 ![UNet Contracting Path](../img/dewarpNet/dewarpNet_7.png)

출처 : [https://medium.com/@msmapark2/u-net-논문-리뷰-u-net-convolutional-networks-for-biomedical-image-segmentation-456d6901b28a](https://medium.com/@msmapark2/u-net-%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0-u-net-convolutional-networks-for-biomedical-image-segmentation-456d6901b28a)

Contracting Path는 일반적인 CNN을 따르며, Downsampling을 위한 

**Expanding Path**


 ![UNet Expanding Path](../img/dewarpNet/dewarpNet_8.png)

출처: [https://medium.com/@msmapark2/u-net-논문-리뷰-u-net-convolutional-networks-for-biomedical-image-segmentation-456d6901b28a](https://medium.com/@msmapark2/u-net-%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0-u-net-convolutional-networks-for-biomedical-image-segmentation-456d6901b28a)

U-Net은 슬라이딩 윈도우 방식을 사용하는 기존의 방식과 다르게, patch 방식을 이용하기 때문에 훨씬 빠르다. 

또한, context 탐지와 localization을 동시에 잘 해낼 수 있다. ⇒ 여러 layer의 output을 동시에 검증하기 때문이다. 

Sematic Segmentation : [https://medium.com/hyunjulie/1편-semantic-segmentation-첫걸음-4180367ec9cb](https://medium.com/hyunjulie/1%ED%8E%B8-semantic-segmentation-%EC%B2%AB%EA%B1%B8%EC%9D%8C-4180367ec9cb)

========================================================================

**Texture Mapping Network.**

Texture Mapping Network는 3D coordinate map을 입력으로 하고 backward mapping 을 결과물로 출력한다. 

Texutre mapping network에서, 우리는 DenseNet encoder-decoder architecture를 사용했다. 

이 과정은, 3D coordinate 좌표계를 texture coordinate 로 변환하는 과정이다. 

**Refinement Network**

Refinement Network는 후처리 과정으로, 결과물의 illumination effect를 조정한다. 

이 Network는 인지할 수 있는 수준의 결과물의 개선을 가져오고, OCR 성능을 개선한다. 

우리는 추가적인 GT 정보를 이용해 (surface map & albedo map) refineNetwork를 학습시킨다. 

Refinement network는 두 개의 U-Net encoder/decoder로 구성되어 있다. 

U-Net 1 : surface normal 예측

U-Net 2 : 입력 이미지와 U-Net1의 결과물인 surface normal을 가지고 shading map 예측.

shading map은 shading intensity 와 color를 표현한다. 

이 결과물을 통해 우리는 shading free image를 생성한다. 

 

### Training Loss Functions

The training process 는 두 개의 양상으로 진행된다. 

Phase 1 에서, shape network와 texture mapping network는 각각 독립적으로 train 된다. 

Phase 2 에서, 두 sub network는 unwarping result를 개선하기 위해 함께 train 된다. 

Shape Network는 추측한 3D coordinate map C를 이용해 loss function을 optimize 한다. 

where ∇C = ∥(∇xC,∇yC)∥2, ∇xC and ∇yC are the horizontal and vertical image gradients of C, and λ con- trols the gradient term’s influence. The image gradient helps learn high-frequency details such as ridges and valleys of C.

 ![](../img/dewarpNet/dewarpNet_9.png)

 ![](../img/dewarpNet/dewarpNet_10.png)
Texture mapping network 는 3D coordinate map에서 backward mapping 을 추측한다. 

(Deformed document paper to flat document image) 

 ![](../img/dewarpNet/dewarpNet_11.png)

B : The mapping B is a flow field representing an image deformation: each pixel (x, y) in B represents a pixel position in the input image I.

D : Final unwarped document image D. (Backward mapping ⇒ Bilinear sampling?)

학습 중에,  각 입력 이미지 I 에 대해 GT deformation을 통해 체커보드 이미지를 얻는다. 

우리는 예측한 backward mapping B를 사용해 체커보드 이미지를 unwarp 하여 unwarped 된 체커보드 이미지 D 를 얻고, 체커보드 이미지 D를 이용해 Ld를 계산한다. 

 ![](../img/dewarpNet/dewarpNet_12.png)

체커보드 이미지의 목표는 document의 texture에 상관없이 Ld를 계산하기 위함이다. 

즉, 같은 변형이 가해진 다른 contents의 이미지들은, 동일한 방법으로 unwarp되어야 한다. 

Second phase에서, shape & texture mapping은 동시에 end-to-end로 학습된다.

Joint training은 backward mapping loss가 shape network의 부족한 부분을 보완하게 한다. 

### Training Details

모델은 Doc3D dataset으로 학습되며, 100,000 장 이상의 이미지로 테스트된다. 

이 때 학습의 성능을 더 끌어올리기 위해서는 training과 validation data끼리는 서로 같은 mesh를 가지고 있으면 안된다. 

1차 학습 (서로 분리하여 학습) 에서는 texture mapping network는 GT 3D coordinate map을 입력으로 가진다. 

2차 학습에서는 shape network를 통해 얻은 추측된 3D coordinate map을 입력으로 사용한다. 

We apply multiple ways of data augmentation: We re- place the background of our training data with images from the Describable Texture Dataset (DTD) [7] and the KTH2b- tips dataset [6] actively during training. The intensity and color of each training image are also randomly jittered.

 ![](../img/dewarpNet/dewarpNet_13.png)

Some limitations exist in our work: First, the inexpen- sive depth sensor cannot capture fine details of deforma- tion like subtle creases on a paper crumple. Thus our data lacks samples with highly complex paper crumple. In fu- ture work, we plan to construct a dataset with better details and more complex structures. Second, DewarpNet is relatively sensitive to occlusion: results degrade when parts of the imaged document are occluded. In future work, we plan to address this difficulty via data augmentation and adver- sarial training.
