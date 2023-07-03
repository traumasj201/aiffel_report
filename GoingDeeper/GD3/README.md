# 아이펠캠퍼스 온라인4기 피어코드리뷰

- 코더 : 이성주
- 리뷰어 : 심재형

PRT(PeerReviewTemplate)
----------------------------------------------

### 코드가 정상적으로 동작하고 주어진 문제를 해결했나요? (O)
시각화를 잘 진행하였고 주어진 문제를 전부 해결했네요 멋져요!
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/624f8bd6-ca8d-4dd9-b5ea-e09ac15fb9d2)
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/11985d4a-098f-4a39-a6bf-7b315f9aacdf)

### 주석을 보고 작성자의 코드가 이해되었나요? (O)
```python
# iou 구하기
def getGrad_CAM_Iou(base_model, layer_name, item, alpha=0.5, box_th=0.25):
    fig, axes = plt.subplots(2, 2, figsize=(8, 8)) # 2 x 2 이미지 틀 생성
    axes = axes.ravel() # 2차원 배열을 1차원으로 변환
    origin_image = item['image'].astype(np.uint8) # org_img
    
    axes[0].imshow(origin_image) # img 설정
    axes[0].axis('off') # 축 제거
    axes[0].set_title('org_img') # title 설정
    
    grad_cam_image = generate_grad_cam(base_model, layer_name, item) # grad_cam 이미지 
    
    axes[1].imshow(grad_cam_image) # img 설정
    axes[1].axis('off') # 축 제거
    axes[1].set_title('grad_cam_img') # title 설정
    
    
    grad_cam_image_3channel = np.stack([grad_cam_image*255]*3, axis=-1).astype(np.uint8) # Grad-CAM 이미지를 3채널로 변환하고 0~255 범위로 스케일링
    blended_image = visualize_cam_on_image(grad_cam_image_3channel, origin_image, alpha) # org img랑 grad_cam 합성
    
    axes[2].imshow(blended_image) # img 설정
    axes[2].axis('off') # 축 제거
    axes[2].set_title('blended_img') # title 설정
    
    grad_cam_rect = get_bbox(grad_cam_image, score_thresh=box_th)
    box_image = cv2.drawContours(origin_image, [grad_cam_rect], 0, (0,0,255), 2)
    
    axes[3].imshow(box_image) # img 설정
    axes[3].axis('off') # 축 제거
    axes[3].set_title('box_img') # title 설정
    
    plt.tight_layout()
    plt.show()
    
    grad_cam_pred_bbox = rect_to_minmax(grad_cam_rect, item['image'])
    
    return  get_iou(grad_cam_pred_bbox, item['objects']['bbox'][0])
```
<br> IOU를 각 항목별로 주석을 잘 적어주셔서 이해가 빨랐습니다

### 코드가 에러를 유발할 가능성이 있나요? (X)
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/5e471b9e-fa0b-4af0-a38a-dcf439bea686)

<br> 각각 실행이 완벽하게 되었기 떄문에 에러는 없습니다!
### 코드 작성자가 코드를 제대로 이해하고 작성했나요? (O)
![image](https://github.com/traumasj201/aiffel_report/assets/65104209/9d011fe9-c4a8-4ed1-983c-c960235555d6)

<br> 평가문항에 대한 문제 정의와 해결을 잘 해놓으셧네요 GOOD!!

### 코드가 간결한가요? (O)
```python
layer_name = 'conv5_block3_out'
box_th = 0.25
alpha = 0.7
iou = getGrad_CAM_Iou(base_model, layer_name, item, alpha, box_th)
print('iou = ', iou)
```
<br> 대부분의 작업들을 함수처리를 통해 매우 간결합니다 GOOD! **ꉂꉂ(ᵔᗜᵔ*)**

----------------------------------------------
