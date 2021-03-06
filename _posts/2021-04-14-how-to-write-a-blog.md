---
layout: post
title:  "넘파이 ndarray (ndarray)"
---

#1. 넘파이 ndarray (ndarray)

** 요약:
아래의 함수들을 외울 것
1) import numpy as np : 넘파이 라이브러리 호출, np는 코드짤때 쉬우라고 약어로
2) np.array(변수) : 넘파이 타입으로 변환
3) type(변수): 해당 변수의 타입 확인 
4) 변수.shape: 해당 변수의 형태((x,y,z,...)꼴로 나타남)
5) 변수.ndim: 해당 변수의 차원, 정수꼴로 나타남 
6) print할때 {:0} 쓰고 .format(변수1) 이런식으로 표기가능하다
7) 변수.dtype으로 데이터 타입 확인가능 
8) 넘파이 array에서 타입이 다른 경우 바이트가 큰걸로 변환됨을 알 수 있다. 
9) 변수.astype.('원하는 타입') 을 입력하면 ()로 타입이 변경됨. 
10) .sum(원하는 축)으로 합할수 있고, 축 안넣으면 전체합, 축 넣으면 축방향으로 합을 만들어준다. 

- ndarray: n차원 배열 객체
- ndarray 생성방법:
import numpy as np
array1 = np.array([1,2,3])
array2 = np.array([[1,2,3], 
                   [2,3,4]])
Numpy 모듈의 array() 함수로 생성, 인자로 주로 파이썬 단일/복합 list 또는 새로운 ndarray 입력

- ndarray 형태(shape)와 차원
ndarray의 shape는 ndarray.shape 속성으로, 차원은 ndarray.ndim 속성으로 알 수 있다. 
array1: 1차원, shape: (3,) //
array2: 2차원, shape: (2,3) // 행*열이라고 생각하면 된다. 

- ndarray 타입(type)
ndarray 내의 데이터값은 숫자, 문자열, bool 등 모두 가능함.
다만, ndarray내의 데이터 타입은 같은 데이터 타입만 가능함. (그냥 연산 특성상)
ndarray.dtype으로 확인할 수 있음

- ndarray 타입 변환
변경을 원하는 타입을 astype(인자)에 인자로 입력
대용량 데이터를 다룰 때 메모리 절약을 위해 형변환을 특히 고려해야 함 

- 넘파이 ndarray의 axis 축
ndarray의 shape는 axis0, axis1, axis2와 같이 axis 단위로 부여되고, 
axis0 == 행, axis1 == 열 인 것 뿐이다. 



- 실습
[1] 
import numpy as np  #넘파이를 np로 호출(이후 np.~~ 로 넘파이 기능 호출)

[2] 
list1 = [1,2,3]    #리스트를 넘파이 array에 넣으면, 실제로 넘파이 array 타입으로 변환됨
print("list1:", list1)
print("list1 type", type(list1))

array1 = np.array(list1)
print("array1:", array1)
print("array1 type", type(array1))

[2-결과]
list1: [1, 2, 3]
list1 type <class 'list'>
array1: [1 2 3]
array1 type <class 'numpy.ndarray'>


[3] 
array1 = np.array([1,2,3])      #shape을 통해 (x,y)를 확인할 수 있다. 1차원은 (x,) 형태로 표현되는 것에 유의할 것 
print("array1 type:", type(array1))
print("array1 array 형태:", array1.shape)

array2 = np.array([[1,2,3], [2,3,4]])   #[[ ]] 개수로 추론 가능, 2차원임
print("array2 type:", type(array2))
print("array2 array 형태:", array2.shape)

array3 = np.array([[1,2,3]])            #이 경우에도 [[ ]] 이므로 2차원임, 다만 행이 한줄이니까 (1,3)
print("array3 type:", type(array3))
print("array3 array 형태:", array3.shape)

[3-결과]
array1 type: <class 'numpy.ndarray'>
array1 array 형태: (3,)
array2 type: <class 'numpy.ndarray'>
array2 array 형태: (2, 3)
array3 type: <class 'numpy.ndarray'>
array3 array 형태: (1, 3)

[4] #{:0} 쓰고 .format(변수1) 이런식으로 표기가능
print("array1: {:0}차원, array2: {:1}차원, array3: {:2}차원".format(array1.ndim, array2.ndim, array3.ndim))   

[4-결과]
array1: 1차원, array2: 2차원, array3:  2차원

[5] # 변수.dtype으로 데이터 타입 확인가능 
list1 = [1,2,3]
array1 = np.array(list1)
print(array1.dtype)

[5-결과]
int32

[6] #타입이 다른 경우 바이트가 큰걸로 변환됨을 알 수 있다. 
list2 = [1,2, 'test']
array2 = np.array(list2)
print(array2, array2.dtype)

list3 = [1,2,3.0]
array3 = np.array(list3)
print(array3, array3.dtype)

[6-결과]
['1' '2' 'test'] <U11
[1. 2. 3.] float64

[7] #astype.('원하는 타입') 을 입력하면 ()로 타입이 변경됨. 
array_int = np.array([1,2,3])
array_float = array_int.astype('float64')
print(array_float, array_float.dtype)

[7-결과]
[1. 2. 3.] float64

[8] #.sum()으로 합할수 있고, 축 안넣으면 전체합, 축 넣으면 축방향으로 합을 만들어준다. 
array2 = np.array([[1,2,3], 
                   [2,3,4]])
print(array2.sum())
print(array2.sum(axis=0))
print(array2.sum(axis=1))

[8-결과]
15
[3 5 7]
[6 9]
