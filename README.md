# Swift-learn

# 기본문법 둘러보기

### 파일 생성
```
New > Playground
```

### 기본 문법들
```
var str = "Hello, playground"
let appleCount = 3
let appleSummary = "나는 사과를 \(appleCount)개 가지고 있다."
print(appleSummary)
```
> 나는 사과를 3개 가지고있다.

### Array
```
var shoppingList = ["shoes", "water", "coffe", "cake"]

shoppingList[1] = "spakling water"


for item in shoppingList {
    print(item)
}
```

### Dictionary
```
var dics: Dictionary = [
    "keroro": 2000,
    "onpice": 3000
]

print(dics["keroro"]!)
```

```
var email: String?
print(email as Any) // nil

email = "devxoul@gmail.com"
print(email!) // !를 써서 경고 벗어나기 nil일 경우 오류가 나니 조심.

func test() -> String {
    
    return "tesT"
}

print(test())
```

#### function
```
func hello(name: String, time: Int) -> String {
    
    var str = ""
    
    for _ in 0..<time {
        str = "hello \(name)"
    }
    
    return str
}

hello(name: "Keroro", time: 2)
```

```
func hello2(to name: String, numberOfTime time: Int) {
    for _ in 0..<time {
        print("\(name)")
    }
}

hello2(to: "keroro", numberOfTime: 3)
```

```
func hello4(message: String) -> (String, String) -> String {
    return { $0 + $1 + message }
}

var testcloser = hello4(message: " - test")
print(testcloser("ke", "roro"))
```

### Class
```
class Dog {
    var name: String?
    var age: Int?
    
    func simple() -> String {
        if let name = self.name {
            return "🐶 \(name)"
        } else {
            return "No name"
        }
    }
}

var myDog = Dog()
myDog.name = "puppy"
myDog.age = 3
print(myDog.simple())
```
