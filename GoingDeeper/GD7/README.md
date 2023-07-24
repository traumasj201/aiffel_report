아이펠캠퍼스 온라인4기 피어코드리뷰 []

- 코더 : 이성주
- 리뷰어 : 이효준

----------------------------------------------

**PRT(PeerReviewTemplate)**

** [⭕] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?   
> 네, 얼굴 검출 이후 스티커(왕관) 합성까지 잘 작동함을 보았습니다.

** [⭕] 주석을 보고 작성자의 코드가 이해되었나요?
```python
def add_sticker(img, boxes, box_index, img_sticker):
    img_show = img.copy()
    img_height = img_show.shape[0]
    img_width = img_show.shape[1]

    x_min = int(boxes[box_index][0] * img_width)
    y_min = int(boxes[box_index][1] * img_height)
    x_max = int(boxes[box_index][2] * img_width)
    y_max = int(boxes[box_index][3] * img_height)

    # 스티커 얼굴 크기로 resize
    w = x_max - x_min
    w_sticker = w
    h_sticker = w
    img_sticker = cv2.resize(img_sticker, (w_sticker,h_sticker))

    # 스티커 좌표
    refined_x = x_min
    refined_y = y_min - 4*h_sticker//5

    # 스티커가 영역 밖으로 나가는 경우 crop
    if refined_x < 0: 
        img_sticker = img_sticker[:, -refined_x:]
        refined_x = 0

    if refined_y < 0:
        img_sticker = img_sticker[-refined_y:, :]
        refined_y = 0
    
    # 스티커 적용
    sticker_area = img_show[refined_y:refined_y+img_sticker.shape[0], refined_x:refined_x+img_sticker.shape[1],:] 

    img_show[refined_y:refined_y + img_sticker.shape[0], refined_x:refined_x + img_sticker.shape[1],:] \
    = cv2.addWeighted(sticker_area, 1, img_sticker, 2, 0)
        
    return img_show
```
> 네, 스티커 사진 합성 하는 과정에 주석을 잘 작성하시어 금방 이해가 되었습니다.

** [❌] 코드가 에러를 유발할 가능성이 있나요?
> 없습니다.

** [⭕] 코드 작성자가 코드를 제대로 이해하고 작성했나요? (직접 인터뷰해보기)
```python
# filepath = os.path.join(PROJECT_PATH, 'checkpoints', 'weights_epoch_119.h5')
filepath = './checkpoints/weights_epoch_119.h5'
# filepath = './checkpoints/weights_epoch_199.h5'
model.load_weights(filepath)

def show_box(TEST_IMAGE_PATH):
    img_raw = cv2.imread(TEST_IMAGE_PATH)
    img_raw = cv2.resize(img_raw, (IMAGE_WIDTH, IMAGE_HEIGHT))
    img = np.float32(img_raw.copy())

    img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    img, pad_params = pad_input_image(img, max_steps=max(BOX_STEPS))
    img = img / 255.0

    boxes = default_box()
    boxes = tf.cast(boxes, tf.float32)

    predictions = model.predict(img[np.newaxis, ...])

    pred_boxes, labels, scores = parse_predict(predictions, boxes)
    pred_boxes = recover_pad(pred_boxes, pad_params)

    for box_index in range(len(pred_boxes)):
        draw_box_on_face(img_raw, pred_boxes, labels, scores, box_index, IMAGE_LABELS)

    plt.imshow(cv2.cvtColor(img_raw, cv2.COLOR_BGR2RGB))
    plt.show()
```
> 모델 weight 파일을 불러와 image에 bbox 확인 및 score까지 표시하는 함수를 잘 구현하였습니다.

** [⭕] 코드가 간결한가요?
```python
TEST_IMAGE_PATH = os.path.join(PROJECT_PATH, 'image_people.png')
STICKER_PATH = './king.png'
inference_test(TEST_IMAGE_PATH, STICKER_PATH, is_bbox=False, is_sticker=True)
```
![](https://velog.velcdn.com/images/joonlaxy/post/2c825aac-9b74-41df-8932-e20b7418d0ed/image.png)
> 네, 이미지에 스티커(합성)하는 함수를 잘 구현하여 불필요한 반복 없이 쉽게 시각화 하였습니다.

----------------------------------------------

참고 링크 및 코드 개선
* 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
* 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
