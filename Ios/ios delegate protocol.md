​											  **Delegate**

------



**Concept**

 Delegate means the representative or substitue 

Using when controll the  **view** **B** using the data in  **view** **A**.



**Using Method**

1. Declare protocol in on the top of a class which has role of server 

```
import UIKit


//Write the protocol declaration here:
protocol ChangeCityDelegate {
    func userEnteredANewCityName (city: String)
}

```

2. Delcare delegate variable as a global variable in the server class 

```
var delegate : ChangeCityDelegate?
```

3.  Make it work using button

```
@IBAction func getWeatherPressed(_ sender: AnyObject) {
        
        //1 Get the city name the user entered in the text field
        let cityName = changeCityTextField.text!
        
        //2 If we have a delegate set, call the method userEnteredANewCityName
        delegate?.userEnteredANewCityName(city: cityName)
        
        //3 dismiss the Change City View Controller to go back to the WeatherViewController
        self.dismiss(animated: true, completion: nil)
        
    }
```

4. Extends a protocol in the client class 

   ```
   class WeatherViewController: UIViewController, CLLocationManagerDelegate, ChangeCityDelegate
   ```

5. Define a function in a protocol in the client class

```
func userEnteredANewCityName(city: String) {
        print(city)
    }
```

6. Assign a delegate of server class to the client class 

7. ```
   override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
           if segue.identifier == "changeCityName" {
               let destinationVC = segue.destination as! ChangeCityViewController
               
               destinationVC.delegate = self
               
               
           }
       }
   ```

   