----  
## **Code Peer Review**
------------------
- 코더 : 이성주
- 리뷰어 : 정연준

## **PRT(PeerReviewTemplate)**  
------------------  
- [x] **1. 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?**
 ```python
image = pipeline(
    prompt="Master works, high quality, film quality, a dog, a poodle, a smiling face, beach background,MG keji,solo,",
    negative_prompt="easynegative,(((pubic))), ((((pubic_hair)))),sketch, duplicate, ugly, huge eyes, text, logo, monochrome, worst face, (bad and mutated hands:1.3), (worst quality:2.0), (low quality:2.0), (blurry:2.0), horror, geometry, (bad hands), (missing fingers), multiple limbs, bad anatomy, (interlocked fingers:1.2), Ugly Fingers, (extra digit and hands and fingers and legs and arms:1.4), crown braid, ((2girl)), (deformed fingers:1.2), (long fingers:1.2),succubus wings,horn,succubus horn,succubus hairstyle,girl,",
    num_inference_steps=10,
    guidance_scale=7,
).images[0]
 ```
프롬프트를 수정하여 결과물을 출력하였다.

- [x] **2. 주석을 보고 작성자의 코드가 이해되었나요?**  

스스로 내용이해가 안되서 코드부분 이해가 잘 안되었습니다.

- [x] **3. 코드가 에러를 유발할 가능성이 있나요?**
 ```python
 ```

- [x] **4. 코드 작성자가 코드를 제대로 이해하고 작성했나요?**  

 ```python
 ```
 작성자가 결과를 출력한것으로 봐서 잘 작성된것 같습니다.

- [x] **5. 코드가 간결한가요?**  

 ```python
 ```
더 간결하게 할 수 있는 것이 보이지 않습니다.

## **참고링크 및 코드 개선 여부**  
------------------  
