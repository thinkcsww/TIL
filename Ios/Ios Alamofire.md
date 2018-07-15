​              							 		 **Alamofire**

------



**How to use**

1. Cocoa pod's library -> Init the pod and insert pod 'Alamofire' in podfile

2. Prepare url, paramters before using below function. This function is to request something to server.

3. ```
   Alamofire.request(url, method: .get, parameters: paramters).responseJSON {
               response in
               if response.result.isSuccess {
                   print("Success! Got the weather data")
                   
               } else {
                   print("Error \(response.result.error)")
                   self.cityLabel.text = "Connection Issues"
               }
           }
   ```

   





