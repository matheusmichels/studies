**Variables**
* var - mutable
* let - immutable

**Primitive Types**
- String, Int, Double, Float, Bool, Character

**Strings**
- Strings with multiple lines
```swift
let myString = """
  He is
  a good dev
"""
```
* Interpolate string values
```swift
print("I'm \(name)")
```

**Number**
* Int, Double, Float
```swift
let randomNumber = Int.random(in: 1...100)
```

**Array**
```swift
let list1: Array<String> = ["ma", "theus"]
let list2: [String] = ["theus", "ma"]
print(list1, list2)
```


**Dictionary**
```swift
let guiDict: Dictionary<String, Any> = [
	"name": "Guilherme",
	"age": 22
]
let myDict: [String: Any] = [
    "name": "Matheus",
    "age": 23
]

print("Dict - I'm \(myDict["name", default: "Unknown"])")
```

**Set**
Store unique values, will mess their order
```swift
let numbers: Set<Int> = Set([1, 1, 3, 5, 7, 9])
// 1, 5, 9, 7, 3
numbers.insert(11)

numbers.contains(3) -> O(1) complexity
// it's not append cause there's no order
```

**Enum**
```swift
enum Weekday {
    case monday, tuesday, wednesday, thursday, friday
}

var day = Weekday.friday
day = .monday

var otherDay: Weekday = .friday
```

```swift
enum Weather {
    case sun, rain, wind
}
let forecast: Weather = .wind
switch forecast {
case .sun:
    print("A nice day")
case .rain:
    print("Pack an umbrella")
default:
    print("Should be okay")
}
```

**For**
```swift
let languages = ["Javascript", "HTML", "CSS"]
for language in languages {
    print("Language: \(language)")
}
for i in 1...10 {
    print(i)
}
```

**Tuple**
- Can have as many elements as you want
- Can have named/unnamed parameters
```swift
let emptyTuple = ()
let namedTuple = (name: "Matheus", age: 23)
let unnamedTuple = ("Javascript", "HTML", "CSS") 
```

```swift
// Named parameters
func getUser() -> (firstName: String, lastName: String, age: Int) {
    return (firstName: "Matheus", lastName: "Michels", age: 23)
}

let user = getUser();
let (name, _, _) = user; // Destructuring
print("The user is \(name) \(user.lastName)")

// Unnamed parameters
func getUser() -> (String, String, Int) {
    return ("Matheus", "Michels", 23)
}
let user = getUser();
let (name, _, _) = user; // Destructuring
print("The user is \(name) \(user.1)")
```

**Function**
* Unnamed parameters (_ paramName: String)
- Named parameters - (paramName: String)
- 2 Named parameters (externalParamName internalParamName: String)
```swift
func isUppercased(_ string: String, foo: Int) -> Bool {
    string == string.uppercased()
}
let uppercased = isUppercased("HELLO WORLD", foo: 5)

func saySomething(foo bar: String) -> Void {
    print("Hello \(bar)")
}
saySomething(foo: "Matheus")
```

* Default parameters values
```swift
func saySomething(_ something: String = "World") -> Void {
    print("Hello \(something)")
}
saySomething() // Hello World
saySomething("Matheus") // Hello Matheus
```

**Error Handling**
```swift
enum PasswordError: Error {
	case short, obvious
}
 
 func checkPassword(_ password: String) throws -> String {
    if (password.count < 5) {
        throw PasswordError.short
    }
    if (password == "12356") {
       throw PasswordError.obvious
    }
    return "Strong!"
 }
 
 do {
    let passwordStrength = try checkPassword("123")
    print("Password strength: \(passwordStrength)")
 } catch PasswordError.short {
    print("Too short bruh")
 } catch {
    print("There was an error: \(error)")
 }
```

- Don't wanna know the error, just if it succeeded
```swift
enum PasswordError: Error {
    case weak, obvious
}

func hashPassword() throws -> String {
    throw PasswordError.weak
}

// try? will default to nil if it throws an error
let passwordHash = try? hashPassword()
print("Hash \(passwordHash)") // Hash nil
```

**Closure**
```swift
let filterLargeNames = { (name: String) -> Bool in
    return name.count > 5
}

let names = ["Matheus", "Guilherme", "Fred"]
print("Large names", names.filter(filterLargeNames))
print("Short names", names.filter({ (name: String) -> Bool in
	name.count < 5
}))

// Shorter syntax
let largeNames = names.filter { name in
    name.count > 5
}
let largeNames = names.filter {
    $0.count > 5
}
```

**Struct**
```swift
struct Album {
    let title: String
    let artist: String
    var isReleased = false
    
    mutating func release() {
        self.isReleased = true
    }
}

var album = Album(title: "Summer", artist: "Khalid")
print(album) // ... isReleased: false
album.release()
print(album) // ... isReleased: true

struct Employee {
    private(set) var vacationAllowed = 14; // Cannot be written directly
    private(set) var vacationTaken = 0;
    // Computed value - calculated every time it's called
    var vacationRemaining: Int {
        return vacationAllowed - vacationTaken;
    }
}
let employee = Employee()
print(employee.vacationRemaining)

struct AppData {
    static var version = 1.0
}
print(AppData.version)
```

- They don't share their data
```swift
struct Actor {
    var name = "Unknown"
}

var actor1 = Actor()
actor1.name = "Liam Neeson"
var actor2 = actor1;
actor2.name = "Vin Diesel"

print(actor1.name) // Liam Neeson
print(actor2.name) // Vin Diesel
```

**Class**
```swift
class Person {
    let name: String;
    let age: Int;
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age;
    }
    deinit { // Called when the ref gets destroyed
	    print("I've been destroyed")
    }
    func greet() {
        print("Hello people!")
    }
}

class Employee: Person {
    private (set) var salary: Int = 0;
    
    func promote(salary: Int) {
        self.salary = salary;
    }  
    override func greet() {
        print("Hello world!")
    }
}

let emp = Employee(name: "Matheus", age: 23)
emp.promote(salary: 3000)
emp.greet()
```

**Protocol (interface)**
```swift
protocol Vehicle {
    var price: Int { get set }
    var year: Int { get set }
    func turnOn() -> Void;
}

class Car: Vehicle {
    var price = 10000;
    var year = 2023;
    func turnOn() {
        print("Vruum")
    }
}

// Functions can receive the protocol type
func getVehiclePrice(vehicle: Vehicle) -> Int {
    return vehicle.price;
} 

let car = Car()
car.turnOn()
print(getVehiclePrice(vehicle: car))
```

**Extension**
- Let's you add new features (extend) to existing data types
```swift
extension String {
  // Returns a new String, doesn't mutate the existing one
  func spaced() -> String {
    return "-\(self)-"
  }
    
  // Mutates the string and returns it
  mutating func space() -> String {
    self = self.spaced()
    return self;
  }
}

var foo = "teste";
foo.space()
print(foo)
```

**if let, guard let**
- if let - lets you use the variable inside the brackets
- guard let - lets you use the variable outside the brackets
```swift
let peopleAges = [
    "matheus": 23,
    "guilherme": 22
]

func getAge(from person: String) -> Int? {
    guard let age = peopleAges[person] else {
        return nil
    }
    // Used outside the check (guard let)
    return age;
}

if let matheusAge = getAge(from: "matheus") {    
    // Used inside the check (if let)
    print("Matheus age is \(matheusAge)")
} else {
    print("Matheus age was not found")
}
```

**Nullish coalescing**
```swift
let input = ""
let number = Int(input) ?? 0
print(number) // 0
```

**Optional chaining**
```swift
let names = ["Matheus", "Guilherme", "Fred"]
let chosen = names.randomElement()?.uppercased()
print(chosen ?? "Not found")
```