# 아이펠캠퍼스 온라인4기 피어코드리뷰

- 코더 : 이성주
- 리뷰어 : 심재형

PRT(PeerReviewTemplate)
----------------------------------------------

### 코드가 정상적으로 동작하고 주어진 문제를 해결했나요? (O)
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/f2f99bf6-efd6-4ffe-b49b-5edf1d7ee426)
<br> 코드가 정상적으로 동작합니다.<br>
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/ca4a52bf-5c31-4377-865a-84b0a0f6a061)
<br> 총정리 설명을 통해 코드의 직관적인 이해가 빨랐고 주어진 문제를 완벽히 해결해냈습니다!
### 주석을 보고 작성자의 코드가 이해되었나요? (O)
```python
...
  # __getitem__은 약속되어있는 메서드입니다
    # 이 부분을 작성하면 slice할 수 있습니다
    # 자세히 알고 싶다면 아래 문서를 참고하세요
    # https://docs.python.org/3/reference/datamodel.html#object.__getitem__
    # 
    # 1. idx에 해당하는 index_list만큼 데이터를 불러
    # 2. image와 label을 불러오고 
    # 3. 사용하기 좋은 inputs과 outputs형태로 반환합니다
    def __getitem__(self, idx):
        # 1.
        batch_indicies = self.index_list[
            idx*self.batch_size:
            (idx+1)*self.batch_size
        ]
        input_images = np.zeros([self.batch_size, *self.img_size, 3])
        labels = np.zeros([self.batch_size, self.max_text_len], dtype='int64')

        input_length = np.ones([self.batch_size], dtype='int64') * self.max_text_len
        label_length = np.ones([self.batch_size], dtype='int64')
...
```
주석을 자세하게 달아주셔서 이해가 빨랐습니다 GOOD!!

### 코드가 에러를 유발할 가능성이 있나요? (X)
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/79013f67-df1d-4c2a-b965-d7c2eff3f7f8)


<br>에러 유발 가능성은 없습니다. GGOOODDD!!
### 코드 작성자가 코드를 제대로 이해하고 작성했나요? (O)
```python
def detect_text(img_path):
    # TODO

    # 배치 크기를 위해서 dimension을 확장해주고 kera-ocr의 입력 차원에 맞게 H,W,C로 변경합니다.
    image = keras_ocr.tools.read(img_path)
    
    ocr_result = detector.detect([image])
    
    # 배치의 첫 번째 결과만 가져옵니다.
    ocr_result = ocr_result[0]
    
    # 시각화를 위해서 x와 y좌표를 변경해줍니다. (앞선 h dimension으로 인해 y,x로 표기됨)
    
    img_pil = Image.fromarray(image)
    result_img = img_pil.copy()
    img_draw = ImageDraw.Draw(result_img)

    cropped_imgs = []
    for text_result in ocr_result:
        img_draw.polygon(text_result, outline='red')
        x_min = text_result[:,0].min() - 5
        x_max = text_result[:,0].max() + 5
        y_min = text_result[:,1].min() - 5
        y_max = text_result[:,1].max() + 5
        word_box = [x_min, y_min, x_max, y_max]
        cropped_imgs.append(img_pil.crop(word_box))


    return result_img, cropped_imgs
```
detect_text 부분을 잘 작성해주신 바 제대로 이해하셨습니다..!

### 코드가 간결한가요? (O)
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/a6b89365-147d-4b7c-bdaf-f6c68bec34b3)

<br> 함수처리를 통해 많은 테스트를 시각화하는 부분에대해 매우 간결하네요! GOOD!

----------------------------------------------
