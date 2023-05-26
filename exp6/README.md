아이펠캠퍼스 온라인4기 피어코드리뷰 []

- 코더 : 이성주
- 리뷰어 : 장승우

----------------------------------------------

**PRT(PeerReviewTemplate)**

** [⭕] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?   

** [⭕] 주석을 보고 작성자의 코드가 이해되었나요?

** [❌] 코드가 에러를 유발할 가능성이 있나요?

** [⭕] 코드 작성자가 코드를 제대로 이해하고 작성했나요? (직접 인터뷰해보기)

** [⭕] 코드가 간결한가요?


----------------------------------------------

참고 링크 및 코드 개선
* 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
* 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```python
data = data[data.apply(lambda x: len(x['text'].split()) <= text_max_len and len(x['headlines'].split()) <= headlines_max_len , axis=1)]
data = data[data.apply(lambda x: len(x['text'].split()) >= text_min_len and len(x['headlines'].split()) >= headlines_min_len , axis=1)]
학습 코드에선 별도로 작업하지 않아서 headlines를 따로 작업하지 않았으나 해당 건은 작업을 한 코더분이 맞았던 것 같습니다.
```

```python
원문으로 했을때 ratio를 변경해도 빈값으로 나왔었는데 3~5 사이값으로 해서 해결하신 것을 보고 참고할 수 있었습니다.
data_org = pd.read_csv('news_summary_more.csv', encoding='iso-8859-1')
for i in range(50, 100):
#     _text = seq2text(encoder_input_test[i])
    _text = data_org.iloc[i,1]
    print("원문 :", _text)
    print("실제 요약 : ", data_org.iloc[i,0])
    print("예측 요약 : ", summarize(_text, ratio=0.35)) # ratio안달면 결과 안나옴...
    print("\n")
    

```
