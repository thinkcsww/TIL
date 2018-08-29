					              **Ios Realm Set up**

------

**Concept**

Realm is the internal storage

**Method**

1. Using cocoa pods install **pod 'RealmSwift'**

2. Add code in the AppDelegate

3. ```
   import RealmSwift
   
   func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
           
           do {
               let realm = try Realm() 
           } catch {
               print("Error initializing new realm \(error)")
           }
           // Override point for customization after application launch.
           
           return true
       }
   ```

   3. Declare data model class

3. ```
   import Foundation
   import RealmSwift
   
   class Stuff: Object {
       @objc dynamic var name: String? = nil
       @objc dynamic var checked: Bool = false
   }
   ```

   4. Read

4. ```
   var stuffs: Results<Stuff>?
   stuffs = realm.objects(Stuff.self)
   ```

   5. Write

      ```
      do {
                      try self.realm.write {
                          let newStuff = Stuff()
                          
                          if textField.text! != "" {
                              newStuff.name = textField.text!
                              newStuff.checked = false
                              self.realm.add(newStuff)
                          }
                          
                      }
                  } catch {
                      print("Error saving new stuff \(error)")
                  }
      ```

      6. Delete

      ```
      let stuff = stuffs![indexPath.row]
                  do {
                      try realm.write {
                          realm.delete(stuff)
                      }
                  } catch {
                      print("Error saving checked status \(error)")
                  }
                  tableView.reloadData()
                  
      ```


