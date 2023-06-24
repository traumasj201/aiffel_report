아이펠캠퍼스 온라인4기 피어코드리뷰 [23.05.18]

- 코더 : 이성주
- 리뷰어 : 부석경

----------------------------------------------

**PRT(PeerReviewTemplate)**

* [o] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?   
**Projet01** 
```python
prediction = model(X_test, W, b)
mse = loss(X_test, W, b, y_test)
mse
```
위 결과 mse : 2886.579... 로 확인 했습니다.   
**Projet02**
```python
y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
rmse = mean_squared_error(y_test, y_pred, squared=False)
print('Mean Squared Error (MSE):', mse)
print('Root Mean Squared Error (RMSE):', rmse)
```
위 결과 RMSE :141.228... 으로 확인 했습니다.
* [o] 주석을 보고 작성자의 코드가 이해되었나요?
  + 저는 mse의 `**0.5` 를 이용해 RMSE를 구현했으나 위와같은 인수로 구현한 것을 주석과 함께 보니 좋았습니다.
```python
rmse = mean_squared_error(y_test, y_pred, squared=False) #m ean_squared_error 함수에 squared=False 옵션을 넣어 RMSE 구현
```
* [v] 코드가 에러를 유발할 가능성이 있나요?
  + 없습니다.
* [v] 코드 작성자가 코드를 제대로 이해하고 작성했나요? (직접 인터뷰해보기)
  + 'minute'와, 'second'컬럼은 데이터들이 모두 0인 컬럼이나 drop을 하지 못하여 아쉬웠습니다. 
```python
# X = train[['year', 'month', 'day', 'hour', 'minute', 'second', 'temp', 'humidity']]
y = train['count']
X = train.drop(['datetime', 'casual', 'registered', 'count'], axis=1)
```

* [o] 코드가 간결한가요?

  + 위 문항에서 저는 하나의 컬럼씩 drop을 진행하여 코드 길이가 길어졌으나 drop을 한번에 하신것이 간결해 보였습니다.

  + 저는 subplot(231)과 같이 plot 각각 위에 달아주어 2배 가량의 줄이 길었으나 위와같이 작성해주어 6개의 subplot이 하나가 되어 매우 간결해짐.
```python
fig, axes = plt.subplots(nrows=2, ncols=3, figsize=(15, 10)) # 2, 3 배열로 그래프 배치 
sns.countplot(data=train, x='year', ax=axes[0, 0])
sns.countplot(data=train, x='month', ax=axes[0, 1])
sns.countplot(data=train, x='day', ax=axes[0, 2])
sns.countplot(data=train, x='hour', ax=axes[1, 0])
sns.countplot(data=train, x='minute', ax=axes[1, 1])
sns.countplot(data=train, x='second', ax=axes[1, 2])
```

----------------------------------------------

참고 링크 및 코드 개선
* 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
* 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
