# 아이펠캠퍼스 온라인4기 피어코드리뷰

- 코더 : 이성주
- 리뷰어 : 심재형

PRT(PeerReviewTemplate)
----------------------------------------------

### 코드가 정상적으로 동작하고 주어진 문제를 해결했나요? (O)
```python
model_dir = os.getenv('HOME') + '/aiffel/object_detection/data/checkpoints_train/'
if is_train:
    callbacks_list = [
        tf.keras.callbacks.ModelCheckpoint( 
            filepath=os.path.join(model_dir, "weights" + "_epoch_{epoch}"),
            monitor="loss",
            save_best_only=False,
            save_weights_only=True,
            verbose=1,
        )  # 에폭당 체크포인트 저장
    ]

    epochs = 10

    history = model.fit(
        train_dataset,
        validation_data=val_dataset,
        epochs=epochs,
        callbacks=callbacks_list
    ) # 메트릭 없이 학습 (loss만 확인)
    import matplotlib.pyplot as plt

    plt.figure(figsize=(12, 6))
    plt.plot(history.history['loss'], 'r', label='Train Loss')
    plt.plot(history.history['val_loss'], 'g', label='Validation Loss')
    plt.title('Model Loss')
    plt.ylabel('Loss')
    plt.xlabel('Epoch')
    plt.legend()
    plt.savefig('./loss_graph.png') # 그래프 이미지로 저장
    plt.show()
else:
    latest_checkpoint = tf.train.latest_checkpoint(model_dir) # 새로 학습한 모델의 마지막 epoch의 체크포인트 가져옴
    model.load_weights(latest_checkpoint)
```
전부 정상적으로 진행되었습니다!
### 주석을 보고 작성자의 코드가 이해되었나요? (O)
```python
model_dir = os.getenv('HOME') + '/aiffel/object_detection/data/checkpoints/' # 기존 제공한 모델 path
latest_checkpoint = tf.train.latest_checkpoint(model_dir) # 가장 마지막 체크포인트 
model.load_weights(latest_checkpoint) #모델로드

image = tf.keras.Input(shape=[None, None, 3], name="image") 
predictions = model(image, training=False)
detections = DecodePredictions(nms_iou_threshold=0.2, confidence_threshold=0.42)(image, predictions) # nms_th = 0.2, cinf_th = 0.42
inference_model = tf.keras.Model(inputs=image, outputs=detections) # inference 모델 생성

        
test_system(self_drive_assist, inference_model)
```
각 항목별로 주석을 잘 달아주셔서 이해가 굉장히 빨랐습니다!

### 코드가 에러를 유발할 가능성이 있나요? (X)
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/00754eec-3591-4f23-bf88-aede92abaf20)

<br>나올 수 있는 경우의수에대한 if처리를 잘 해놓으셔서 오류는 없습니다 GGOOODDD!!
### 코드 작성자가 코드를 제대로 이해하고 작성했나요? (O)
```python
for box, _cls, score in zip(boxes, class_names, scores):
        if _cls == 'Pedestrian': 
            print('사람을 찾았습니다.')
            return "Stop"
        if _cls == 'Car' or _cls == 'Van' or _cls == 'Truck' :
            x1, y1, x2, y2 = box
            width = x2 - x1
            height = y2 - y1
            if width >= size_limit or height >= size_limit:
                print('큰 차량을 찾았습니다.')
                return "Stop"
    
    return 'Go'
```
모델의 동작방식을 이해하시고 x축 그리고 y축까지 전부 처리했기에 정말 좋은거같습니다!

### 코드가 간결한가요? (O)
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/6a1f7012-17be-44bd-9780-da7a6ce65f59)

<br> 깔끔한 함수처리로 코드가 매우 간결해보입니다! **ꉂꉂ(ᵔᗜᵔ*)**

----------------------------------------------
