​	 								          **LocationManager**

------



**Concept**

Using GPS or Wifi to locate the user.

**Using Method**



1. Import and extends

```
import CoreLocation

class WeatherViewController: UIViewController, CLLocationManagerDelegate, ChangeCityDelegate
```

2. Declare new object as global

```
let locationManager = CLLocationManager()
```

3. Make a self as a delegate of locationManager and setup the accuracy and authority permission

```
locationManager.delegate = self
locationManager.desiredAccuracy = kCLLocationAccuracyHundredMeters
locationManager.requestWhenInUseAuthorization()
locationManager.startUpdatingLocation()
```

4. Get a latitude and longitude and other values by defining didUpdateLocation call back function

```
func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
        let location = locations[locations.count - 1]
        if location.horizontalAccuracy > 0 {
            locationManager.stopUpdatingLocation()
            locationManager.delegate = nil
            print("longitude = \(location.coordinate.longitude), latitude = \(location.coordinate.latitude)" )
            
            let latitude = String(location.coordinate.latitude)
            let longitude = String(location.coordinate.longitude)
            
            let params : [String : String] = ["lat" : latitude, "lon" : longitude, "appid" : APP_ID]
            
            getWeatherData(url: WEATHER_URL, parameters: params)
        }
    }
```

5. Define a error callback function 

```
//Write the didFailWithError method here:
    func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
        print(error)
        cityLabel.text = "Location Unavailable"
    }
```

