​									  **UINavigationBar UIColor** 

------



**Concept**

UiNavigation Bar's UI Colors

**Method**

1. How to change the ui of the navigation bar, implement in viewWillApear

![image-20180729130846682](/var/folders/6h/d959ycy164x3_g0xg3j6p_440000gn/T/abnerworks.Typora/image-20180729130846682.png)



```
override func viewWillAppear(_ animated: Bool) {
        
        
        if let colourHex = selectedCategory?.colour {
            
            title = selectedCategory!.name
            guard let navBar = navigationController?.navigationBar else {fatalError("Navigation controller does not exist")}
            
            if let navBarColour = UIColor(hexString: colourHex) {
                
                navBar.barTintColor = navBarColour
                navBar.largeTitleTextAttributes = [NSAttributedStringKey.foregroundColor: ContrastColorOf(navBarColour, returnFlat: true)]
                navBar.tintColor = ContrastColorOf(navBarColour, returnFlat: true)
                searchBar.barTintColor = navBarColour
            }
            
            
        }
    }
```

