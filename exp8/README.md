아이펠캠퍼스 온라인4기 피어코드리뷰 []

- 코더 : 이성주
- 리뷰어 : 장승우

----------------------------------------------

**PRT(PeerReviewTemplate)**

** [⭕] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?   
```python
sentence_generation("너 바보야?")
입력 : 너 바보야?
출력 : 힘내세요 .
'힘내세요 .'
sentence_generation("나 너무 피곤한데 어떻게해?")
입력 : 나 너무 피곤한데 어떻게해?
출력 : 푹 쉬세요 .
'푹 쉬세요 .'

위와 같이 주어진 문제를 해결하는 Output이 나왔습니다.
```
** [⭕] 주석을 보고 작성자의 코드가 이해되었나요?
```python
def preprocess_sentence(sentence):
    # 입력받은 sentence를 소문자로 변경하고 양쪽 공백을 제거
    sentence = sentence.strip()

    # 단어와 구두점(punctuation) 사이의 거리를 만듭니다.
    # 예를 들어서 "나는 학생입니다." => "나는 학생 입니다 ."와 같이
    # 학생과 마침표 사이에 거리를 만듭니다.
    sentence = re.sub(r"([?.!,])", r" \1 ", sentence)
    sentence = re.sub(r'[" "]+', " ", sentence)

    # (ㄱㅎ가-힣, ".", "?", "!", ",")를 제외한 모든 문자를 공백인 ' '로 대체합니다.
#     sentence = re.sub(r"[^ㄱ-ㅎ가-힣?.!,]+", " ", sentence)
    sentence = re.sub(r"[^0-9ㄱ-ㅎ가-힣?.!,]+", " ", sentence)
    sentence = sentence.strip()
    return sentence
    
위와 같이 전처리에도 주석이 자세하게 달려있어서 코드 이해가 쉬웠습니다.
```
** [❌] 코드가 에러를 유발할 가능성이 있나요?
```python
new_model = tf.keras.models.load_model('comfort_bot1')

위와 같이 새로운 모델로 테스트할 경우 변수를 다르게 주어 에러를 방지했습니다.
```
** [⭕] 코드 작성자가 코드를 제대로 이해하고 작성했나요? (직접 인터뷰해보기)
```python
BATCH_SIZE = 64
BUFFER_SIZE = 10000
def __init__(self, d_model, warmup_steps=2500):

하이퍼파라미터 값들을 변경해보면서 다른 결과들도 있고 
버퍼 사이즈도 데이터 사이즈에 따라 변경한 것을 보니 이해하고 진행하였습니다.
```
** [⭕] 코드가 간결한가요?
```python
def load_conversations(_data):
    Q = _data['Q']
    A = _data['A']
    Label = _data['label']


    Q = [preprocess_sentence(q) for q in _data['Q']]
    A = [preprocess_sentence(a) for a in _data['A']]
    return Q, A, Label
    
전처리하는 변수가 무엇을 의미하는지 명확하게 알 수 있을 정도로 설정해놔서 간결했습니다.
본인은 input,output으로 해서 가독성이 떨어졌네요
```

----------------------------------------------

참고 링크 및 코드 개선
* 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
* 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
