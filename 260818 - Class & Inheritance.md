오늘은 클래스를 배웠다.

객체는 사물·대상처럼 "모든 것"을 표현하는 단위다.
객체는 '속성' 과 '행위'를 가진다.

| 구성            | 의미                 | 예시                  |
| ------------- | ------------------ | ------------------- |
| 속성(Attribute) | 객체가 가진 상태(데이터, 변수) | 버스의 승객 수, 계좌의 잔액    |
| 행위(Method)    | 객체가 할 수 있는 기능(함수)  | 버스에 승객이 탑승, 계좌에서 출금 |

클래스는 객체를 만들기 위해 속성과 메서드를 미리 정의해 둔 설계도 **(틀)**
인스턴스는 설계도를 바탕으로 메모리에 실제로 만들어진 구체적인 실체 **(객체)**

붕어빵 틀 비유
붕어빵 틀(클래스) 하나를 만들어두면, 서로 다른 재료를 넣은 붕어빵(인스턴스)을 원하는 만큼 찍어낼 수 있다. 틀은 그대로이고, 붕어빵은 각각 독립된 실물이다.

같은 클래스에서 만들어진 인스턴스여도 독립된 주소를 갖는다.

```
class Car:
	pass # 빈 설계도

car_a = Car()
car_b = Car()

print(tpye(car_a)) # <class '__main__.Car'>
print(car_a is car_b) # False -> 서로 다른 객체
```

생성자 init
객체가 생성되는 순간 가장 먼저 자동 호출하는 메서드다. 인스턴스가 가져야 할 속성에 최초 값을 할당(초기화)하는 역할을 한다.
```
class Charater:
	def __init__(self, nickname):
		self.nickname = nickname # 생성 시 값을 채움
		
player = Character("스파르타")
print(player.nickname) # 스파르타
```

self 키워드
클래스 내부에서 메서드를 정의할 때 첫 번째 매개변수로 오는 **자기 참조 변수**
객체가 생성되면 그 객체 **자신의 자원에 접근하기 위한 참조 변수** 역할을 한다.
클래스 내부에서만 사용하며, self.속성 형태로 인스턴스 고유 데이터에 접근·할당
```
class Monitor:
	def check_myself(self):
		print(f"메서드 안의 self 주소: {id(self)}")
		
screen = Monitor() # 객체 생성
print(f"실제 변수의 주소: {id(screen)}")
screen.check_myself() # 두 주소값이 같다
```

속성과 인스턴스 메서드

| 용어                        | 의미                                   |
| ------------------------- | ------------------------------------ |
| 속성(Attribute)             | 클래스 내부에 선언되어 **객체마다 정의된 인스턴스 변수**    |
| 인스턴스 메서드(Instance Method) | `self`를 첫 매개변수로 받아 **객체가 가지고 있는 함수** |
```
class Smartphone:
	def __init__(self, model):
		self.model = model    # 속성
		self.battery = 100    # 속성 기본값
		
	def charge(self):         # 인스턴스 메서드
		self.battery = 100
		print(f"{self.model} 충전 완료!")
		
phone = Smartphone("Galaxy")
phone.charge()
```
**self.속성 으로만 객체별 독립 공간에 기록된다.**

str과 repr
객체를 어떻게 "보여줄지" 결정하는 두 특수 메서드

| 메서드        | 호출 시점                         | 목적             | 관례적 형식                                   |
| ---------- | ----------------------------- | -------------- | ---------------------------------------- |
| `__str__`  | `print(객체)`                   | 사용자에게 보기 좋은 설명 | "김철수님의 계좌 (현재 잔액: 5000원)"                |
| `__repr__` | `repr(객체)`, 셀에서 객체 단독 조회, 디버거 | 개발자·로깅용 공식 명세  | `BankAccount(owner='김철수', balance=5000)` |
상속
상속은 이미 만들어진 클래스(부모 클래스)의 속성·메서드를 그대로 물려받아 새클래스(자식 클래스)를 정의하는 방식. 공통 코드를 중복 작성하지 않아 유지보수가 쉬워진다.
```
class 자식클래스(부모클래스):
	...
```

```
class Animal:
	def __init__(self, kind):
		self.kind = kind    # 동물 종류
	
	def move(self):
		print("동물이 움직인다.")
	
class Dog(Animal):
	def __init__(self):
		super().__init__("강아지")    # 부모의 __init__를 호출해 kind 초기화
		
class Cat(Animal):
	def __init__(self):
		super().__init__("고양이")

dog = Dog()
dog.move()                # 동물이 움직인다.
print(dog.kind, cat.kind) # 강아지 고양이
```

super()
super()는 부모 클래스를 가리키는 참조다.
- self -> 자식 객체(현재 객체) 자신
- super -> 부모 클래스의 자원에 접근
자식 클래스만의 새 속성을 추가하면서도 부모의 초기화 로직을 재사용하고 싶을 때
```
class Person:
	def __init__(self, name):
		self.name = name
		
class Student(Person):
	def __init__(self, name, major):
		super().__init__(name)    # 부모가 name을 세팅
		self.major = major        # 자식 고유 속성 추가
		
std = Student("김철수", "컴퓨터공학")
print(std.name)      # 김철수
print(std.major)     # 컴퓨터공학
```

메서드 오버라이딩
메서드 오버라이딩은 부모 클래스와 동일한 이름의 메서드를 자식 클래스에서 재정의하는 것이다. 자식 객체에서 호출하면 자식 클래스에 정의된 메서드가 최우선 실행된다.
```
class Animal:
	def __init__(self, kind):
		self.kind = kind
		
	def move(self):
		print("동물이 움직인다")
		
class Dog(Animal):
	def __init__(self):
		super().__init__("강아지")
	
	def move(self):
		super().move()             # 부모의 move() 먼저 실행
		print(self.kind + "걸음으로 움직인다.")
		
class Cat(Animal):
	def __init__(self):
		super().__init__("고양이")
		
	def move(self):
		print(self.kind + "걸음으로 움직인다.") # 부모 move를 호출하지 않고 완전 재정의
		
dog = Dog()
dog.move()

cat = Cat()
cat.move()
```

isinstance()는 객체가 특정 클래스(또는 그자손)로부터 생성되었는지 True/False로 알려주는 함수다.
```
class Human:
	def move(self):
		print("두발로 직립보행한다.")
		
human = Human()

print(isinstance(human, Animal))  # False -> Human은 Animal의 자식이 아님
print(isinstance(human, Human))   # True
print(isinstance(dog, Animal))    # True -> Dog는 Animal의 자식이므로 True

s = 'ABC'
isinstance(s, str)     # True
```

다중 상속과 MRO(Method Resolution Order)
MRO는 같은 이름의 메서드가 여러 부모에 있을 때 어느 것을 호출할지 정하는 우선순위다.
파이썬은 여러 부모 클래스를 상속할 수 있다.
```
class ParentA:
	def a(self):
		print("ParentA - a()")
	
	def b(self):
		print("ParentB - b()")
		
class ParentB:
	def a(self):
		print("ParentB - a()")
	
	def c(self):
		print("ParentB - c()")
		
class Child(ParentB, ParentA):   # 괄호 안 순서가 중요
	pass
	
c = Child()
c.b()   # ParentA - b()  -> ParentB에 b가 없어서 ParentA에서 찾음
c.c()   # ParentB - c()
c.a()   # ParentB - a()  -> 둘 다 a가 있으면 왼쪽(ParentB)이 우선선
```

캡슐화(Encapsulation): 관련 있는 '속성'과 '메서드'를 하나의 클래스에 모으는 것
정보 은닉(Information Hiding): 외부에서 객체 내부의 민감한 데이터를 함부로 보거나 수정하지 못하도록 차단하는 개념
```
class Schedule:
	def __init__(self, year, month, day):
		self.year = year
		self.month = month
		self. day = day
		
	def __str__(self):
		return f"year={self.year}, month={self.month}, day={self.day}"

s1 = Schedule(2026, 8, 18)
print(s1)    # year=2026, month=8, day=18

s1.year = 2026
s1.month = 2
s1.day = 28
print(s1)     # year = 2026, month = 2, day = 28 -> 외부에서 마음대로 변경됨
```

프라이빗 변수는 변수 이름 앞에 언더바 두개를 붙여 이름 변형 규칙을 적용시켜, 원래 이름으로는 외부에서 접근 할 수 없게 이름이 바뀐다. 클래스 내부에서만 접근 가능한 인스턴스 변수가 됨
```
class Schedule:
	def __init__(self, year, month, day):
		self.__year = year
		self.__month = month
		self.__day = day
		
	def __str__(self):
		return f"year={self.__year}, month={self.__month}, day={self.__day}"
		
s1 = schedule(2026, 8, 18)
print(s1)    # year=2026, month=8, day,18

s1.__year = 2026
s1.__month = 2
s1.__day = 31
print(s1)    # year=2026, month=8, day=18
```
내부적으로 `_클래스명__변수명`으로 이름이 바뀐다. (예:`__year`->`Schedule__year`)
보안 차단 기능은 아니다. 변형된 이름을 알면 접근 가능하다.

Getter/Setter은 비공개 속성을 안전하게 조회·수정하도록 중간에서 매개하는 메서드다.
Python이 제공하는 공식 문법이나 키워드가 아닌 개발자가 관례적으로 get_x, set_x 라는 이름을 붙여 직접 정의하는 메서드다.
```
class Schedule:
	def __init__(self, year, month, day):
		self.__year = year
		self.__month = month
		self.__day = day
		
	def get_year(self):
		return self.__year
		
	def get_month(self):
		return self.__month
		
	def get_day(self):
		return self.__day
		
	def set_year(self):
		self.year = year
	
	def set_month(self):
		self.month = month
		
	def set_day(self, day):
		if self.__month == 2 and day >28:   # 값에 대한 통제 가능
			day = 28
		self.__day = day
	
	def __str__(self):
		return f"year={self.__year}, month={self.__month}, day={self.__day}"
		
s1 = Schedule(2026, 8, 18)
s1.set_month(2)     # 2월로 변경
s1.set_day(31)      # 2월 31일은 불가능 -> 28로 통제
print(s1)           # year = 2026, month = 2, day = 28
```