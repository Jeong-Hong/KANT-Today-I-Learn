오늘은 함수를 배웠다.
튜터님과의 면담도 있었다.
반복만이 답이다.

함수란 특정 목적을 가진 코드들을 하나의 독립된 상자처럼 묶어 이름을 붙여둔 재사용 가능한 코드 구조다. 입력, 처리, 출력으로 구성된다.

```
def 함수이름(매개변수, ...):
	# 처리 부분
	return 반환값 # 출력 부분
```

함수도 객체이기에 변수에 할당해도 같은 함수 객체를 가리킨다.

```
def calc(x):
	y = x * 2 + 1
	return y

result = calc(2) # 5
calc2 = calc
calc2(20) # 41
calc is calc2 # True
```

매개변수는 외부에서 입력 받는 값을 담는다.
인수는 매개변수에 입력 할 값
```
def welcome(name): # name이 매개변수
	print(f"{name}님, 환영합니다!")
	
welcome("민수") # "민수"는 인수
```

위치 인수는 매개변수의 순서대로 값을 지정한다.
키워드 인수는 매개변수명=값 형태로 지정한다.
```
def add(num1 , num2):
	return num1 + num2
	
add(10 , 20) # 10과 20이 위치인수
add(num1=10 , num2=20) # num1=10과 num2=20이 키워드 인수
```

위치 인수와 키워드 인수의 혼합 시 주의점
인터프리터가 인수를 앞에서부터 차례대로 매핑하기 때문에, 키워드 인수 뒤에 위치 인수가 오면 어느 매개변수에 넣어야 할지 알 수 없다.
```
def add(num1, num2, name, mobile):
	return f"{num1+num2}, {name=},{mobile=}"
	
# 위치 인수 + 키워드 인수 혼합 -> 정상
add(10, 20, mobile="010-0000-1000", name="김영희")

# 키워드 인수 뒤에 위치 인수 -> SyntaxError
add(mobile="010-0000-1000", name="김영희", 10, 20)
```

기본값 매개변수는 호출 시 인수를 입력하지 않으면 미리 설정된 기본 값이 자동 적용된다. 기본값이 있는 매개변수는 **오른쪽 끝**부터 차례대로 정의한다.
```
# 기본값 없는 매개변수가 기본값 뒤에 오면 SyntaxError
def add(num1, num2, name, mobile="010")
	return f"{num1+num2}, {name=},{mobile=}"
```
```
# 올바른 순서
def add(num1, num2, mobile, name=None):
	return f"{num1+num2}, {name=},{mobile=}"
	
add(10, 20, "010-1000-1000")
```

가변 인수는 개수를 고정하지 않고 유연하게 받을 때 쓴다.
Args는 Arguments , Kwargs는 Keyword arguments
```
# *args : 개수 무제한 '위치 인수' -> 튜플
def add(*nums):
	print(nums, type(nums))
	
add(10, 20)
```
```
# **kwargs : 개수 무제한 '키워드 인수' -> 딕셔너리
def print_user_info(**info):
	print(info)
	
print_user_info(name="김철수", age=20)
```

return은 값을 돌려주면서 함수를 끝낸다. 값이 없어도 return만으로 종료가 가능하다.
```
def add(num):
	if num == 999:
		print("종료")
		return     # 값 없이 return -> 함수 즉시 종료

	result = num ** 2
	return result
	
add(10)    # 100
add(999)   # 종료 (print 후 return으로 종료, 제곱은 실행되지 않음)
```

중요. 복수데이터 반환
여러 개를 반환한 것처럼 보이지만 실제로는 하나의 튜플로 묶어서 반환한다.
받는 쪽에서 a, b, c, d = ... 처럼 언패킹하면 각 변수에 분배된다.
```
def calc(num1, num2):
	return num1 + num2 , num1 * num2 , num1 - num2, num1 / num2

a, b, c, d = calc(10, 20)
print(a, b, c, d)     # 30 200 -10 0.5
```