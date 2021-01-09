#2. 변수와 자료형
- 자바와 달리 끝에 세미콜론 붙이지 않아도 된다.
- var : 언제든지 읽기 쓰기가 가능한 일반적인 변수
- val : 선언시에만 초기화 가능, 중간에 값을 변경할 수 없음
- Property(속성) : 클래스에 선언된 변수
- Local Variable(지역변수) : Scope내에 선언된 변수
- """ 여러 줄의 문자열 """

#3. 형변환
- 하나의 변수에 지정된 자료형을 호환되는 다른 자료형으로 변경하는 기능
- 명시적 형변환 : 변환될 자료형을 직접 지정함
- 암시적 형변환 : 변수를 할당할 시 자료형을 지정하지 않아도 자동으로 형변환 됨
- 배열 : 한번 지정하면 변경할 수 없으나 빠른 입출력 가능
   
   var intArr = arrayOf(1, 2, 3, 4, 5) // 일반적인 배열 생성
   
   var nullArr = arrayOfNulls<Int>(5) // 비어 있는 배열 생성
   
   intArr[2] = 8

#4. 타입추론과 함수
- 타입추론 : 해당 변수가 어떤 자료형을 가지는지 추론 가능, 코드량 줄일 수 있음
- 함수 : 함수는 특정한 동작을 하거나 원하는 결과값을 연산하는데 사용

fun main() {
    
	println(add(5, 6, 7))
   
}

fun add(a: Int, b: Int, c: Int): Int {
    return a + b + c
}

fun add(a: Int, b: Int, c: Int) = a + b + c

#5. 조건문과 비교연산자
- if문 : 참과 거짓을 조건문에 따라 판단하여 반환
fun main() {
    var a = 11
    
    if(a > 10) {
        println("a는 10보다 크다.")
    } else {
        println("a는 10보다 작거나 같다.")
    }
}
- When문 : 등호, 부등호의 사용은 불가. 
<조건문으로 이용하는 예제>

fun main() {
	
    doWhen(1)
    doWhen("When")
    doWhen(12L)
    doWhen(3.141592)
    doWhen("Kotlin")
}

fun doWhen (a: Any) {
    when(a) {
        1 -> println("정수 1입니다")
        "Dimo" -> println("디모의 코틀린 강좌입니다.")
        is Long -> println("Long타입 입니다.")
        !is String -> println("String타입이 아닙니다.")
        else -> println("어떤 조건도 만족하지 않습니다")
    }
}

#6. 반복문과 증감연산자
- 조건형 반복문 : 조건이 참인 경우 반복
- 범위형 반복문 : 반복 범위를 정해놓고 반복 수행
- do-while : 조건과 관계없이 반드시 한 번 실행
- for
fun main() {
	
    for(i in 0..9 step 3) {
        print(i)
    }
}

fun main() {
	
    for(i in 9 downTo 0) {
        print(i)
    }
}

fun main() {
	
    for(i in 'a'..'e') {
        print(i)
    }
}

#7. 흐름제어와 논리연산자
- break : 반복문 즉시 종료
- continue : 조건문을 제외한 값들 출력
- lable을 이용한 이중 for문
fun main() {
	
    loop@for(i in 1..10) {
       for (j in 1..10) {
           if (i==1 && j==2) break@loop
           println("i : $i , j : $j")
       }
	}
}
- 논리연산자 : &&, ||, !

#8. 클래스의 기본 구조
fun main() {
	var a = Person("박보영", 1990)
    var b = Person("전정국", 1997)
    var c = Person("장원영", 2004)
    
    a.introduce()
    b.introduce()
    c.introduce()
}

class Person (var name:String, val birthYear:Int) {
    fun introduce() {
        println("안녕하세요, ${birthYear}년생 ${name}입니다.")
    }
}
#9. 생성자
- 새로운 인스턴스를 만들기 위해 호출하는 특수한 함수
- 인스턴스의 속성을 초기화, 인스턴스 생성시 구문을 수행
- this : 인스턴스 자신의 속성이 함수를 호출하기 위해 클래스 내부에서 사용되는 키워드
- 기본 생성자 : 클래스를 마들 때 기본으로 선언
- 보조 생성자 : 필요에 따라 추가적으로 선언
fun main() {
	
    var a = Person("박보영", 1990)
    var b = Person("차은우", 1997)
    var c = Person("류수정", 2004)
    
    var d = Person("이루다")
    var e = Person("전정국")
    var f = Person("장원영")
    
}

class Person (var name:String, val birthYear:Int) {
   init {
       println("${this.birthYear}년생 ${this.name}님이 생성되었습니다.")
   }
   
   constructor(name:String) : this(name, 1997) {
       println("보조 생성자가 사용되었습니다.")
   }
}

#10. 클래스의 상속
- open : 클래스가 상속될 수 있도록 클래스 선언 시 붙이는 키워드
- 자식 클래스는 부모 클래스의 존재하는 속성과 같은 이름의 속성을 가질 수 없다.
- 자식 클래스가 생성될 때에는 반드시 부모클래스의 생성자까지 호출되어야 한다.
fun main() {
	var a = Animal("별이", 5, "개")
    var b = Dog("별이", 5)
    var c = Cat("루이", 1)
    
    a.introduce()
    b.introduce()
    c.introduce()
    
    b.bark()
    c.meow()
    
}

open class Animal (var name:String, var age:Int, var type:String) {
  fun introduce() {
      println("저는 ${type} ${name}이고, ${age}살 입니다.")
  }
}

class Dog (name:String, age:Int) : Animal(name, age, "개") {
    fun bark() {
        println("멍멍")
    }
}

class Cat (name:String, age:Int) : Animal(name, age, "고양이") {
    fun meow() {
        println("야옹")
    }