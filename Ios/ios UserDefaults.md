​										 **UserDefault**

------



**Concept**

Using local database to keep datas



**Using Method**



1. Declare it as a global

```
var itemArray = ["Find Mike", "Buy Eggos", "Destroy Demogorgon"]
let defaults = UserDefaults.standard
```

2. Save it in the user default

```
self.defaults.set(self.itemArray, forKey: "TodoListArray")
```



3. Call it in viewDidLoad()

```
if let items = defaults.array(forKey: "TodoListArray") as? [String] {
            itemArray = items
        }
```

