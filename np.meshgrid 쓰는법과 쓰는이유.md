## np.meshgrid 쓰는법과 쓰는이유



np.meshgrid는 두 벡터를 통해 매트릭스로 변환시켜주는 함수다.

두 벡터기 때문에 만들어지는 매트릭스도 두 가지 방식으로 나타난다.

```python
x = np.arange(10) # 10, 사이즈의 벡터 (0,1,2,3,4,5,6,7,8,9)
y = np.arange(10) # 10, 사이즈의 벡터 (0,1,2,3,4,5,6,7,8,9)
# 두 벡터를 통해 매트릭스를 만들어보자
np.meshgrid(x,y)
#output 
>>[array([[0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]]),
 array([[0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [1, 1, 1, 1, 1, 1, 1, 1, 1, 1],
        [2, 2, 2, 2, 2, 2, 2, 2, 2, 2],
        [3, 3, 3, 3, 3, 3, 3, 3, 3, 3],
        [4, 4, 4, 4, 4, 4, 4, 4, 4, 4],
        [5, 5, 5, 5, 5, 5, 5, 5, 5, 5],
        [6, 6, 6, 6, 6, 6, 6, 6, 6, 6],
        [7, 7, 7, 7, 7, 7, 7, 7, 7, 7],
        [8, 8, 8, 8, 8, 8, 8, 8, 8, 8],
        [9, 9, 9, 9, 9, 9, 9, 9, 9, 9]])]
```



매트릭스를 만들어주는데 특징이있다. 

1. 두 매트릭스 모두 shape는 (y,x) 로 고정되어있다(x,y 아님 주의!! )
2. output의 첫번째 매트릭스는 (y,x) 사이즈에 row를 x로 반복하여 채운 매트릭스다
3. output의 두번째 매트릭스는 (y,x) 사이즈에 column을 y로 반복하여 채운 매트릭스다



그냥 봤을땐 쓸모가 없는듯하나 이미지의 좌표를 만들어야할때 숨겨놓은 빛을 발한다

```python
x_matrix, y_matrix = np.meshgrid(x,y)
coordinate = np.stack((x_matrix, y_matrix), axis=2).reshape(-1, 2)
print(coordinate)
#output
>>
array([[0, 0],
       [1, 0],
       [2, 0],
       [3, 0],
       [4, 0],
       [5, 0],
       [6, 0],
       [7, 0],
       [8, 0],
       [9, 0],
       [0, 1],
       [1, 1],
       [2, 1],
       [3, 1],
       [4, 1],
       [5, 1],
       [6, 1],
       [7, 1],
       [8, 1],
       [9, 1],
       [0, 2],
       [1, 2],
       [2, 2],
       [3, 2],
       [4, 2],
       [5, 2],
       [6, 2],
       [7, 2],
       [8, 2],
       [9, 2],
       [0, 3],
       [1, 3],
       [2, 3],
       [3, 3],
       [4, 3],
       [5, 3],
       [6, 3],
       [7, 3],
       [8, 3],
       [9, 3],
       [0, 4],
       [1, 4],
       [2, 4],
       [3, 4],
       [4, 4],
       [5, 4],
       [6, 4],
       [7, 4],
       [8, 4],
       [9, 4],
       [0, 5],
       [1, 5],
       [2, 5],
       [3, 5],
       [4, 5],
       [5, 5],
       [6, 5],
       [7, 5],
       [8, 5],
       [9, 5],
       [0, 6],
       [1, 6],
       [2, 6],
       [3, 6],
       [4, 6],
       [5, 6],
       [6, 6],
       [7, 6],
       [8, 6],
       [9, 6],
       [0, 7],
       [1, 7],
       [2, 7],
       [3, 7],
       [4, 7],
       [5, 7],
       [6, 7],
       [7, 7],
       [8, 7],
       [9, 7],
       [0, 8],
       [1, 8],
       [2, 8],
       [3, 8],
       [4, 8],
       [5, 8],
       [6, 8],
       [7, 8],
       [8, 8],
       [9, 8],
       [0, 9],
       [1, 9],
       [2, 9],
       [3, 9],
       [4, 9],
       [5, 9],
       [6, 9],
       [7, 9],
       [8, 9],
       [9, 9]])
```



아직까지는 이게 meshgrid 의 best 존재이유다!