# Swift-learn

# 기본문법 둘러보기

### 파일 생성

> New > Playground


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

#### Function
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



# App 만들기


> New > Project


> stroyboard 에서 uitableView 추가


```
import UIKit

class ViewController: UIViewController, UITableViewDelegate, UITableViewDataSource {

    @IBOutlet var tableView: UITableView!

    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
        self.tableView.separatorInset = UIEdgeInsets.zero // cell 공백제거
        loadData()
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }
  
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 5
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell: UITableViewCell = UITableViewCell(style: UITableViewCellStyle.subtitle, reuseIdentifier: "Cell")
        cell.textLabel?.text = "test"
        return cell
    }
}
```


> json 데이터 로드

```
    func loadData() {
        let urlStr:String = "https://api-city.livere.com/livereDataLoad?refer=livere.com%2Fpremium%2Flivere&title=%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%A6%AC%20%ED%94%84%EB%A6%AC%EB%AF%B8%EC%97%84%20-%20%EA%B8%B0%EB%B3%B8&version=8&dummy=0.6175115388842263&livereCallback=&smartlogin_seq=2247&consumer_seq=5&livere_seq=26472&_=1493118713493"
        
        if let url = URL(string: urlStr) {
            do {
                let jsonString = try String(contentsOf: url)
                let data = jsonString.data(using: .utf8)!
                let json = try JSONSerialization.jsonObject(with: data) as? [String: Any]
                lists = (json?["RE_LIST"] as? [[String:Any]])!
                
            } catch {
            }
        } else {
            // bad url
        }
    }
```

### Custom Cell 만들기 

> Main.Stroyboard 에서 ReplyViewCell 만들기

```
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return lists.count
}

func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
    return 89.0
}
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        var cellData = lists[indexPath.row] as? [String:Any]
        let cell = tableView.dequeueReusableCell(withIdentifier: "ReplyViewCell", for: indexPath) as! ReplyViewCell
        cell.contentLabel.text = cellData?["content"] as! String?
        let memberIcon = cellData?["member_icon"] as! String!
        let catPictureURL = URL(string: memberIcon!)
        let imageData:NSData = NSData(contentsOf: catPictureURL!)!
        cell.profileImg.image = UIImage(data: imageData as Data)
        cell.usernameLabel.text = cellData?["name"] as! String?
        var snsicon = UIImage(named: "sns_livere_m")
        if cellData?["member_domain"] as! String? == "facebook" {
            snsicon = UIImage(named: "sns_facebook_m")
        }
        cell.snsIcon.image = snsicon
        
        return cell
    }
```


## NavigationController 추가

> 메뉴에서  Editor > Embed in Navigation Controller 추가

시작 Controller 변경 Attributes Inspector > Is Initial View Controller 체크


### TableViewController 생성

```
override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
        // Dispose of any resources that can be recreated.
    }


    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        // #warning Incomplete implementation, return the number of rows
        return 5
    }
    
    override func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        return 89
    }

    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
//        let cell: UITableViewCell = UITableViewCell(style: UITableViewCellStyle.subtitle, reuseIdentifier: "Cell") // 기본셀
//        cell.textLabel?.text = "test"
        let cell = tableView.dequeueReusableCell(withIdentifier: "ReplyViewCell", for: indexPath) as! ReplyViewCell
        return cell
    }
```
