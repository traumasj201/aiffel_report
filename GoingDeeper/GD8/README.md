아이펠캠퍼스 온라인4기 피어코드리뷰 [23.07.26]

- 코더 : 이성주
- 리뷰어 : 부석경

----------------------------------------------

**PRT(PeerReviewTemplate)**

** [⭕] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?    
simplebaseline을 10epoch 까지도 진행 해주었습니다.

* simplebaseline 5epoch

  ![image](https://github.com/traumasj201/aiffel_report/assets/71332005/6f7f56f9-ecd9-404a-a65d-e083150d30ee)

* stackhourgalss 5epoch
  
![image](https://github.com/traumasj201/aiffel_report/assets/71332005/4ffb4cd7-9533-47a2-8ca0-356ce3b0d51b)


> * 회고   
> add 오류로 너무 많은 시간을 보냈다...   
> 이걸 고치니 simplebase에서 오류가 또 발생했다...   
> 무슨 이유인지는 모르겠다........   
> ray는 싫다......   
> 학습이 똑바로 안된다...   
> loss가 계속 떨어지는 것으로 보아서 추가적으로 더 학습이 필요해보인다.


** [⭕] 주석을 보고 작성자의 코드가 이해되었나요?   

* 수정한 코드에 대해 설명이 되어있었습니다.
```python
# ADD에서 float int 형 오류로 인하여 아래와 같이 수정
    def compute_loss(self, labels, outputs):
        loss = 0
        weights = tf.cast(labels > 0, dtype=tf.float32) * 81 + 1
        if self.netname == 'Simplebaseline':
            loss = tf.math.reduce_mean(
                tf.math.square(labels - outputs) * weights) * (
                    1.0 / self.global_batch_size)
        else:
            for output in outputs:
                loss += tf.math.reduce_mean(
                    tf.math.square(labels - output) * weights) * (
                        1.0 / self.global_batch_size)
        return loss
```

** [❌] 코드가 에러를 유발할 가능성이 있나요?   
* 찾지 못했습니다.   

  
** [⭕] 코드 작성자가 코드를 제대로 이해하고 작성했나요? (직접 인터뷰해보기)   

네 여러 시도와 수정을 한 것으로 보아 이해하고 있습니다.   
또한 같이 오류를 수정하며 많은 도움을 받았기에 충분히 이해하고 작성한 것으로 보입니다.   
 
** [⭕] 코드가 간결한가요?   
네 복잡한 코드를 찾지 못했습니다.   


----------------------------------------------

참고 링크 및 코드 개선
* 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
* 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
