# 아이펠캠퍼스 온라인4기 피어코드리뷰[23.06.28]

- 코더 : 이성주
- 리뷰어 : 부석경

---------------------------------------------
## **PRT(PeerReviewTemplate)**

### **[⭕] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?**
|평가문항|상세기준|완료여부|
|-------|---------|--------|
|CutMix와 MixUp 기법을 ResNet50 분류기에 성공적으로 적용하였는가?|CutMix와 MixUp을 적용한 데이터셋으로 훈련한 각각의 ResNet 모델이 수렴하였다 | ![image](https://github.com/traumasj201/aiffel_report/assets/71332005/5e50e1c6-9dac-4fc9-8749-ab73425571fd) 이미지와 같이 학습중 검증 성능 그래프로 모델이 수렴하고 있다는 것을 확인했습니다.|
| 다양한 실험을 통해 태스크에 최적인 Augmentation 기법을 찾아내었는가?|각 Augmentation 기법을 적용하고, 그에 따른 성능 비교 분석 및 문제점을 서술하였음|  ![image](https://github.com/traumasj201/aiffel_report/assets/71332005/6f6e99f5-1c55-4210-a423-c7ad155fd2ee)  여러가지의 Augmentation기법을 합쳐서 데이터셋을 만들고 학습했습니다. |
| 여러가지 Augmentation 기법을 적용한 결과를 체계적으로 비교분석하였는가?|기본 Augmentation, CutMix, MixUp이 적용된 결과를 시각화와 함께 체계적으로 분석하였다.| ![image](https://github.com/traumasj201/aiffel_report/assets/71332005/45cb85ec-7246-40d4-801e-c052daa91563)

 |  

### **[⭕] 주석을 보고 작성자의 코드가 이해되었나요?**
```python
num_classes = ds_info.features["label"].num_classes
batch_size = 64

ds_train_no_aug = apply_normalize_on_dataset(ds_train, with_aug=False)
ds_train_aug = apply_normalize_on_dataset(ds_train, with_aug=True)
ds_train_mixup = apply_normalize_on_dataset(ds_train, with_aug=True, with_mixup=True)
ds_train_cutmix = apply_normalize_on_dataset(ds_train, with_aug=True, with_cutmix=True)
ds_test = apply_normalize_on_dataset(ds_test, is_test=True)

# Concatenate ds_train_cutmix and ds_train datasets
ds_train_combined_cut = ds_train_cutmix.concatenate(ds_train_no_aug)
ds_train_combined_mix = ds_train_mixup.concatenate(ds_train_no_aug)
ds_train_combined_aug = ds_train_aug.concatenate(ds_train_no_aug)

buffer_size = 128 # Adjust the buffer size as per your requirements

ds_train_combined_cut = ds_train_combined_cut.shuffle(buffer_size=buffer_size)
ds_train_combined_mix = ds_train_combined_mix.shuffle(buffer_size=buffer_size)
ds_train_combined_aug = ds_train_combined_aug.shuffle(buffer_size=buffer_size)
```
변경한 점에 대해 설명을 추가해주었습니다.

### **[⭕] 코드가 에러를 유발할 가능성이 있나요?**
> UserWarning: The `lr` argument is deprecated, use `learning_rate` instead.

위와 같은 경고를 따라
```python
cutmix_resnet50.compile(
    loss='categorical_crossentropy',

    optimizer=tf.keras.optimizers.SGD(lr=0.01),
    >>> optimizer=tf.keras.optimizers.SGD(learning_rate=0.01),

    metrics=['accuracy'],
)
```

### **[⭕] 코드 작성자가 코드를 제대로 이해하고 작성했나요?** (직접 인터뷰해보기)   
네 `fit()` 함수 내의 `steps_per_epoch`와 `validation_steps`를 설명을 부탁드렸고 자세히 알고 있었습니다.

### **[⭕] 코드가 간결한가요?**   
네 불필요한 코드를 보지 못했습니다.


----------------------------------------------
### **참고 링크 및 코드 개선**
* 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
* 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.

----------------------------------------------
