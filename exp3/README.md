아이펠캠퍼스 온라인4기 피어코드리뷰 [23.05.23]

- 코더 : 이성주
- 리뷰어 : 부석경

----------------------------------------------

**PRT(PeerReviewTemplate)**

* [o] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?   
![image](https://github.com/traumasj201/aiffel_report/assets/71332005/2448eb13-207b-4fd1-b36d-0b50f8477ae7)
![image](https://github.com/traumasj201/aiffel_report/assets/71332005/be17e84c-06e8-41d9-859c-dbcdb889e116)   
위와 같은 오류들을 잘 해결하였다.

![image](https://github.com/traumasj201/aiffel_report/assets/71332005/65457add-8152-4e84-9be9-f89e2fb94f34)
![image](https://github.com/traumasj201/aiffel_report/assets/71332005/2f53d670-59a8-4c36-93dd-8129c15f48c3)   
각도를 변환하는 것 또한 매우 자연스럽게 해결하였다.

* [o] 주석을 보고 작성자의 코드가 이해되었나요?
```python
if img.shape[1] > 360:
    img = cv2.resize(img, (360, int(360 * img.shape[0]/img.shape[1]) )) # 얼굴이 너무 커서 이미지 축소 진행
```
코드 작성의 이유들을 잘 적어주어 문제해결을 위한 추가및 변경사항이 쉽게 이해되었습니다.

* [v] 코드가 에러를 유발할 가능성이 있나요?

코드가 매우 짜임새있고 문제점과 해결과저을 상세히 담고 있습니다.
에러 유발 가능성을 찾지 못하였습니다

* [o] 코드 작성자가 코드를 제대로 이해하고 작성했나요? (직접 인터뷰해보기)
```python
import math
def get_angle(landmark):
    dy = landmark[57][1] - landmark[27][1]
    dx = landmark[57][0] - landmark[27][0]
    return math.atan2(dx, dy) * (180.0 / math.pi)
```
수염의 각도를 조절할 때 atan2가 쓰여, atan와 atan2의 차이점과 각도 조절 방식을 질문했고 자세히 답변해주었습니다.

* [o] 코드가 간결한가요?
```python
my_image_path = './IU_2.jpg' 
img = cv2.imread(my_image_path) 

my_sticker_path = './cat_whiskers.jpg' 
img_sticker = cv2.imread(my_sticker_path) 

scicker_add_img = add_sticker_to_face(img, face_detector, landmark_predictor, img_sticker)

imshow(scicker_add_img)
```
코드를 함수화 했다.
불필요한 코드 없이 간결하게 작성되었다.

----------------------------------------------

참고 링크 및 코드 개선
* [atan와 atan2](https://spiralmoon.tistory.com/entry/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%9D%B4%EB%A1%A0-%EB%91%90-%EC%A0%90-%EC%82%AC%EC%9D%B4%EC%9D%98-%EC%A0%88%EB%8C%80%EA%B0%81%EB%8F%84%EB%A5%BC-%EC%9E%AC%EB%8A%94-atan2)

