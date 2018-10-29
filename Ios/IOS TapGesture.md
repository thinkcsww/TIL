​								**IOS tapGesture**

------

**Concept**

TapGesture

**Method**

1. Declare tapGesture

```
let tapGesture = UITapGestureRecognizer(target: self, action: #selector(tableViewTapped))
```

2. Add gesture recognizer to the view

```
tableView.addGestureRecognizer(tapGesture)
```

3. Declare function to control when gesture is catched 

```
@objc func tableViewTapped() {
        contentTextField.endEditing(true)
    }
```

