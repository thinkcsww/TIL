​                                  						 **CoCoaPod**

------

CocoaPod:   Xcode library dependency manager



**Install** 

1. sudo gem install cocoapods

2. pod setup --verbose

**Usage**

1. Enter the folder

2. pod init

3. Open the pod file and add like this 

   ```
   platform :ios, '9.0'
   
   target 'Clima' do
     # Comment the next line if you're not using Swift and don't want to use dynamic frameworks
     use_frameworks!
   
     # Pods for Clima
   
       pod 'SwiftyJSON'
       pod 'Alamofire'
       pod 'SVProgressHUD'
   
   end
   
   ```

   4. pod install 





