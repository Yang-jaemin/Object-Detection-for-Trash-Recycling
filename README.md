# 🚯 Trash Recycling Object Detection


## 🔎 Project Overview

<img width="824" alt="스크린샷 2023-08-18 오후 7 09 19" src="https://github.com/Yang-jaemin/Object-Detection-for-Trash-Recycling/assets/108872973/e6503db7-71b1-491f-bad1-c40eb5280d9c">



대량 생산, 대량 소비의 시대. 우리는 많은 물건이 대량으로 생산되고, 소비되는 시대를 살고 있습니다. 하지만 이러한 문화는 '쓰레기 대란', '매립지 부족'과 같은 여러 사회 문제를 낳고 있습니다.분리수거는 이러한 환경 부담을 줄일 수 있는 방법 중 하나입니다. 문제 해결을 위한 데이터셋으로는 일반 쓰레기, 플라스틱, 종이, 유리 등 10 종류의 쓰레기가 찍힌 사진 데이터셋이 제공됩니다.이를 이용하여 사진에서 쓰레기를 Detection 하는 모델을 만들어 이러한 문제점을 해결해보고자합니다

<br/>

## 👨‍👨‍👧‍👦 Members


| 이름          | github                                    | 맡은 역할                                                    |
| ------------- | ----------------------------------------- | ------------------------------------------------------------ |
| 김보경 &nbsp; | [github](https://github.com/bogeoung)     | Baseline Code 리팩토링, wandb 연동, AI 모델 리서치           |
| 김정주        | [github](https://github.com/Kim-Jeong-Ju) | YOLO v8 실험, YOLO 전용 SKF 구현, Augmentation 실험          |
| 양재민        | [github](https://github.com/Yang-jaemin)  | Baseline with Stratified K-Fold 리팩토링, Ensemble 적용, AI 모델 리서치 |
| 임준표        | [github](https://github.com/anonlim)      | Augmentation 실험 및 적용, AI 모델 리서치 및 실험            |
| 정남교        | [github](https://github.com/jnamq97)      | SKF를 활용한 Data Split 구현, AI 모델 리서치 및 실험 설계    |

## 📷 Dataset


- Image Data

  - 크기: (1024, 1024)
  - Train: 4883장의 Training용 train image
  - Test: 4871장의 Validation용 test image 
- Annotation Data

  - train.json: train image에 대한 annotation file (COCO format)
  - Test.json: test image에 대한 annotation file (COCO format)

    - Id: 파일 안에 annotation 고유 index, ex) 1
    - bbox: 객체가 존재하는 박스의 좌표 (xmin, ymin, width, height)
    - area: 객체가 존재하는 박스의 크기
    - category_id: 객체가 해당하는 Class의 id
    - image_id: annotation이 표시된 이미지 고유 index


- 10 classes: 0-General trash, 1-Paper, 2-Paper pack, 3-Metal, 4-Glass, 5-Plastic, 6-Styrofoam, 7-Plastic bag,8-Battery, 9-Clothing

<br/>

## 📎 Experiment

실험 관련 세부사항은 [랩업리포트](Lv2_Object_Detection_WrapUp_jaemin.pdf) 참고.

<br/>

## 💡 Result

| Model                                                        | mAP    |
| ------------------------------------------------------------ | ------ |
| YOLO v8 + RetinaNet                                          | 0.4556 |
| YOLO v8 + RetinaNet + Faster R-CNN + Cascade R-CNN (iou_thresh=0.5) | 0.4663 |
| Swin Transformer KFold(split 0~3) + Faster R-CNN+ DetectoRS  | 0.5222 |
| Swin Mask R-CNN + DetectoRS(iou_thresh=0.6)                  | 0.5255 |
| Swin Transformer (split 0,1,3) + Faster R-CNN +DetectoRS     | 0.5270 |

