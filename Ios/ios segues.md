​											  **Segues**

------



**Concept**

Move the app's view to next view or behind view.

**Using Method**

1. Connect Views using button.
2. Make a button object in controller and insert this code

```
@IBAction func buttonPressed(_ sender: Any) {
        performSegue(withIdentifier: "goToSecondScreen", sender: self) // this code
    }
```

**Transfer data between views**

```
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {

		//refer the different view and use the properities in that view.
        if segue.identifier == "goToSecondScreen" {
            
            let destinationVC = segue.destination as! ViewController2// refer and assign
            
            destinationVC.textPasswedOver = text.text!  //
        }
        
    }
```

