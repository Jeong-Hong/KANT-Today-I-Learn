오늘은 조건문과 반복문을 배웠다.

조건문 - 판별식의 값이 True이면 참일 때 실행할 코드, False이면 거짓일 때 실행할 코드를 정하는 문장.
```
if 판별식:
	판별식이 참일 때 실행되는 코드
```
- 판별식은 비교 연산자, 논리 연산자 또는 값 자체로 구성된다

단일 조건문: if
```
num = 10
if num > 5:
	print("5보다 크다")
```

if - else 조건문
```
num = 10
if num == 10:
	print("10 입니다.")
else:
	print("10이 아닙니다.")
```
> [!warning] elif는 앞선 조건이 False일 때만 평가된다. 큰 범위 -> 작은 범위 순서로 써야 모든 구간이 도달한다.

if - elif - else
```
age = int(input())
if age >= 20:
	print("성인")
elif age >= 17:
	print("고등학생")
elif age >= 14:
	print("중학생")
elif age >= 8:
	print("초등학생)
else:
	print("유치원생")
```

중첩 조건문과 논리 연산자 결합

"10 이상 100 미만"을 두 가지 방식으로 표현한다.
```
# 중첩 if
if number >= 10:
	if number < 100:
		print(f"{number}은(는) 10이상 100미만입니다.")

# 논리 연산자 and 결합 - 같은 조건을 한 줄로
if number >= 10 and number < 100:
	print(f"{number}은(는) 10이상 100미만입니다.")
```

input()과 형변환
```
age = int(input())
print(type(age), age)
```

반복문

for 문과 range( )

횟수가 정해져 있는 반복:
```
for num in range(반복횟수):
	# 반복 수행 되는 코드
```

range( )의 세가지 형태
1. range(n) - 0부터 n-1까지
2. range(시작, 종료) - 시작 이상, 종료 미만
3. range(시작, 종료, 증감) - 시작이상, 종료 미만, 증감 단위

반복 변수는 i(index) 관례, 중첩되면 i -> j -> k -> l 순서
반복 횟수만 필요하고 변수를 안 쓸 때는 __ 를 사용한다.
```
for _ in range(10):
	print("반복")
```

반복 가능한 요소의 반복
```
for 요소 in 반복 가능한 것들:
	# 반복 수행되는 코드
```

딕셔너리 순회 ㅡ items( ) + 언패킹
```
user = {"email": "user@test.org", "name" : "김철수", "age": 20}

for key, value in user.items():
	print(key, value)
```

while 문

조건식이 참인동안 반복
```
while 조건식:
	# 조건식이 참일 때 반복 수행되는 코드
```
```
total = 0
start = 1

while start <= 100:
	total += start
	start += 1     # <- 이 줄이 없으면 무한 루프

print("합계", total)
```

반복문 중간 제어

continue - 현재 반복만 중단하고 다음 반복을 시작
```
total = 0
for i in range(1,101):
	if i % 2 == 0:     # 짝수면
		continue
	total += i
print(f"합계: {total}")
```

break - 반복 전체를 중단하고 루프를 빠져나감
```
for _ in range(10):
	num = int(input())
	if num == 99:
		print("종료")
		break
	print("입력한 숫자", num)
```

이중 반복문
```
for i in range(2, 10):     # 단
	print("-" * 5, i, "단", "-" * 5)
	for j in range(1, 10):     # 곱하는 수
		print(f"{i}*{j} = {i*j}")
```

리스트 컴프리헨션
```
nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

result = []
for num in nums:
	result.append(num * num)

# 컴프리헨션	
result = [num **2 for num in nums]

# 조건 필터 (홀수만)
nums = [*range(11)] # [0~10]
result = [num for num in nums if num % 2 == 1]

# 이중 반복 (구구단 전체를 한 줄로)
result = [f"{i}*{j} = {i*j}" for i in range(2, 10)
		for j in range(1, 10)]
```
