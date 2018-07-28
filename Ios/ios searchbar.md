​										 **ios searchbar**

------



**Concept**

Using a searchbar and core data, sort the datas 

**Method**

1. Attach the searchbar on the view controller

![image-20180727203442187](/var/folders/6h/d959ycy164x3_g0xg3j6p_440000gn/T/abnerworks.Typora/image-20180727203442187.png)

2. extends a UISearchBarDelegate in the viewcontroller and generate the function 

   *Item is custom class

```
extension TodoListViewController: UISearchBarDelegate {
    
    func searchBarSearchButtonClicked(_ searchBar: UISearchBar) {
        let request: NSFetchRequest<Item> = Item.fetchRequest()
        
        request.predicate = NSPredicate(format: "title CONTAINS[cd] %@", searchBar.text!)
        
        request.sortDescriptors = [NSSortDescriptor(key: "title", ascending: true)]
        
        loadItems(with: request)
        
    }
    
    func searchBar(_ searchBar: UISearchBar, textDidChange searchText: String) {
        if searchBar.text?.count == 0 {
            loadItems()
            
            DispatchQueue.main.async {
                searchBar.resignFirstResponder()
            }
            
        }
    }
    
}
```

