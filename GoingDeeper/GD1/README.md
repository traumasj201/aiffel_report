아이펠캠퍼스 온라인4기 피어코드리뷰 [23.06.26]

- 코더 : 이성주
- 리뷰어 : 부석경

----------------------------------------------

**PRT(PeerReviewTemplate)**

** [$O$] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?   
> ResNet-34, ResNet-50 모델 구현이 정상적으로 진행되었는가?    
> * 네 노드에 제시된 summary를 비교하고, 총 파라미터수를 비교하며 잘 구현된 것을확인했습니다.

> 구현한 ResNet 모델을 활용하여 Image Classification 모델 훈련이 가능한가?	
> * 네. 훈련을 진행했습니다.

> Ablation Study 결과가 바른 포맷으로 제출되었는가?
![image](https://github.com/JeJuBOO/Aiffel_Nodes/assets/71332005/8cc12b2c-02f1-43ba-ab9d-d13079bfccbe)
> * 네 위 그래프와 같이 그래프를 모아서 보여주니 보기 쉬웠습니다.
   

** [$O$] 주석을 보고 작성자의 코드가 이해되었나요?   
```python
# 데이터 경로 설정
train_dir = './data/PetImages/'

# 데이터 전처리 및 증강
image_size = (224, 224)  # 이미지 크기 설정
batch_size = 32

# 데이터 증강 설정
datagen = ImageDataGenerator(
    rescale=1./255,  # 이미지 스케일 조정
    validation_split=0.2  # 검증 데이터셋 분할 비율 설정
)

# 훈련 데이터셋 및 검증 데이터셋 생성
train_dataset = datagen.flow_from_directory(
    train_dir,
    target_size=image_size,
    batch_size=batch_size,
    class_mode='binary',
    subset='training',  # 훈련 데이터셋 설정
    shuffle=True
)

validation_dataset = datagen.flow_from_directory(
    train_dir,
    target_size=image_size,
    batch_size=batch_size,
    class_mode='binary',
    subset='validation',  # 검증 데이터셋 설정
    shuffle=True
)
```
> 네. 코드를 보며 제 코드의 문제점또한 찾을 수 있을 정도로 이해되기 쉽게 작성되어 있습니다.   


** [$X$] 코드가 에러를 유발할 가능성이 있나요?   
> 에러를 유발할 코드는 찾지 못했습니다.   


** [$O$] 코드 작성자가 코드를 제대로 이해하고 작성했나요? (직접 인터뷰해보기)   
> residual connection을 코드 내에서 어떻게 진행하고 있는지 질문 했고 자세히 답해주었습니다.

** [$O$] 코드가 간결한가요?
> 네, 함수를 사용하며 간결히 모델을 설계했습니다.

----------------------------------------------

참고 링크 및 코드 개선
* 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
* 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.ResNet-34, ResNet-50 모델 구현이 정상적으로 진행되었는가?
