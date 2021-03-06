# datetime 형식 마스타하기





### 부분만 datetime이 안되있는 경우

3월부터 10월까지 데이터셋을 통합했는데  나머지는 모두 datetime 형식으로 깔끔하게 ('2018-03-01 00:42:10')

나눠져있는데, 5월만 '20190510121322' 형태로 되어있다면?

해당 데이터만 `pd.to_datetime(해당시간데이터, format='%Y%m%d%H%M%S')` 로 변환한다음에,

이걸 `df.loc[ 해당인덱스, 해당시간변수] = 변환한 데이터` 코드를 통해 넣으려 했다.

하지만, 데이터 타입 에러인지 넣기만하면 괴상한 숫자로 변형되어 들어가길래 포기..

 `df['해당시간변수'] = pd.to_datetime(해당시간데이터, format='%Y%m%d%H%M%S')` 를 통해

전체 컬럼을 싹다 바꿔보려했지만, 이미 포맷에 맞게 변형되어있는 기존 데이터 때문에 에러가 발생했다.

결국 apply 함수를 통해 해결했다. 이미 변환된데이터는 str형태로 글자수를 세었을때 19개, 

변환되지 않은 데이터는 14개인점에 착안했다.

```python
df['해당시간변수'] = df['해당시간변수'].apply(lambda x : pd.to_datetime(x , 
                                                           format  ='%Y%m%d%H%M%S'),
                                 if len(x)==14 else x)
```







### datetime64 형식에서 시간 연산하기

시간형식의 데이터를 다뤄야할 때가 있다. 예를 들면 전체 데이터의 시간을 30분 전으로 수정한다던가

특정 시간과 특정시간을 비교연산하여 더 빠르고 느린것을 구별해야 한다던가

그럴때 연산할 수 있도록 datetime 형식을 알아보자



```python
from datetime import timedelta
import datetime
```



우선 데이터형식을 `datetime64`에 맞게 변경해야한다



```python
data['시간']  = data['시간'].astype('datetime64')
```



datetime64 형식으로 변경했으면, 그 다음부턴 시간을 자유롭게 잘라서 쓰거나 비교할 수 있다.

```python
data['시간_월'] = data['시간'].apply(lambda x : x.month)
data['시간_일'] = data['시간'].apply(lambda x : x.day)
data['시간_시'] = data['시간'].apply(lambda x : x.hour)
data['시간_분'] = data['시간'].apply(lambda x : x.minute)
data['시간_초'] = data['시간'].apply(lambda x : x.second)
```



datetime64형식으로 바뀐데이터의 각각 인스턴스는 `Timestamp`가 되어 서로간 시간계산이 편해진다.



#### 요일 알아내기

`datetime64`형식으로 바꾼 뒤, 간단하게 모두 확인할 수 있다.



```python
data['시간'].astype('datetime64').dt.day_name() #요일로 변경된값 return
```



